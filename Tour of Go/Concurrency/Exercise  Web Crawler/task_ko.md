# 연습: 웹 크롤러

이 연습에서는 Go의 동시성 기능을 사용하여 웹 크롤러를 병렬화할 것입니다.

`Crawl` 함수를 수정하여 동일한 URL을 두 번 가져오지 않으면서 URL을 병렬로 가져오세요.

_힌트_: 이미 가져온 URL을 추적하는 캐시를 맵(map)으로 유지할 수 있지만, 맵만으로는 동시 사용에 안전하지 않습니다!

<div class="hint" title="가능한 솔루션 보기">

    package main
    
    import (
    	"errors"
    	"fmt"
    	"sync"
    )
    
    type Fetcher interface {
    	// Fetch는 URL의 본문과
    	// 해당 페이지에서 발견된 URL의 슬라이스를 반환합니다.
    	Fetch(url string) (body string, urls []string, err error)
    }
    
    // fetched는 가져온(또는 가져오는 중인) URL을 추적합니다.
    // 맵에서 읽거나 쓸 때는 락을 걸어야 합니다.
    // 임베디드 타입에 대한 설명은 https://golang.org/ref/spec#Struct_types 섹션을 참조하세요.
    var fetched = struct {
    	m map[string]error
    	sync.Mutex
    }{m: make(map[string]error)}
    
    var loading = errors.New("url 로드 중") // 센티널 값
    
    // Crawl은 fetcher를 사용하여 URL을 시작점으로 해서 재귀적으로 페이지를 크롤링하며,
    // 최대 depth까지 진행합니다.
    func Crawl(url string, depth int, fetcher Fetcher) {
    	if depth <= 0 {
    		fmt.Printf("<- %v 완료, depth 0입니다.\n", url)
    		return
    	}
    
    	fetched.Lock()
    	if _, ok := fetched.m[url]; ok {
    		fetched.Unlock()
    		fmt.Printf("<- %v 완료, 이미 가져왔습니다.\n", url)
    		return
    	}
    	// URL을 로딩 중으로 표시하여 다른 요청이 동시에 로드하지 않도록 합니다.
    	fetched.m[url] = loading
    	fetched.Unlock()
    
    	// URL을 동시적으로 로드합니다.
    	body, urls, err := fetcher.Fetch(url)
    
    	// 동기화된 구역에서 상태를 업데이트합니다.
    	fetched.Lock()
    	fetched.m[url] = err
    	fetched.Unlock()
    
    	if err != nil {
    		fmt.Printf("<- %v 오류: %v\n", url, err)
    		return
    	}
    	fmt.Printf("발견됨: %s %q\n", url, body)
    	done := make(chan bool)
    	for i, u := range urls {
    		fmt.Printf("-> %v의 %v/%v번째 하위 URL 크롤링 중: %v.\n", url, i, len(urls), u)
    		go func(url string) {
    			Crawl(url, depth-1, fetcher)
    			done <- true
    		}(u)
    	}
    	for i, u := range urls {
    		fmt.Printf("<- [%v] %v/%v번째 하위 URL 대기 중: %v.\n", url, i, len(urls), u)
    		<-done
    	}
    	fmt.Printf("<- %v 완료\n", url)
    }
    
    func main() {
    	Crawl("https://golang.org/", 4, fetcher)
    
    	fmt.Println("가져오기 통계\n--------------")
    	for url, err := range fetched.m {
    		if err != nil {
    			fmt.Printf("%v 실패: %v\n", url, err)
    		} else {
    			fmt.Printf("%v 가져오기 성공\n", url)
    		}
    	}
    }
    
    // fakeFetcher는 미리 정의된 결과를 반환하는 Fetcher입니다.
    type fakeFetcher map[string]*fakeResult
    
    type fakeResult struct {
    	body string
    	urls []string
    }
    
    func (f *fakeFetcher) Fetch(url string) (string, []string, error) {
    	if res, ok := (*f)[url]; ok {
    		return res.body, res.urls, nil
    	}
    	return "", nil, fmt.Errorf("not found: %s", url)
    }
    
    // fetcher는 데이터가 채워진 fakeFetcher입니다.
    var fetcher = &fakeFetcher{
    	"https://golang.org/": &fakeResult{
    		"The Go Programming Language",
    		[]string{
    			"https://golang.org/pkg/",
    			"https://golang.org/cmd/",
    		},
    	},
    	"https://golang.org/pkg/": &fakeResult{
    		"패키지",
    		[]string{
    			"https://golang.org/",
    			"https://golang.org/cmd/",
    			"https://golang.org/pkg/fmt/",
    			"https://golang.org/pkg/os/",
    		},
    	},
    	"https://golang.org/pkg/fmt/": &fakeResult{
    		"패키지 fmt",
    		[]string{
    			"https://golang.org/",
    			"https://golang.org/pkg/",
    		},
    	},
    	"https://golang.org/pkg/os/": &fakeResult{
    		"패키지 os",
    		[]string{
    			"https://golang.org/",
    			"https://golang.org/pkg/",
    		},
    	},
    }
    
</div>
# 연습: 맵 (Maps)

`WordCount`를 구현하세요. 이 함수는 문자열 `s`에서 각 "단어"의 개수를 나타내는 맵을 반환해야 합니다. `wc.Test` 함수는 제공된 함수에 대해 테스트 스위트를 실행하며 성공 또는 실패를 출력합니다.

[strings.Fields](https://go.dev/pkg/strings/#Fields)를 유용하게 사용할 수 있습니다.

<sub>**참고:** _import_ 섹션에 있는 의존성이 빨간색으로 강조 표시되면, 해당 의존성을 클릭하고, <span class="shortcut">&shortcut:ShowIntentionActions;</span>를 누른 후 **Sync dependencies of main**을 선택하세요.</sub>

<div class="hint" title="가능한 해결책 보기">

    package main
    
    import (
    	"strings"
    
    	"golang.org/x/tour/wc"
    )
    
    // WordCount 함수는 입력 문자열에서 각 단어의 빈도를 계산합니다.
    func WordCount(s string) map[string]int {
    	m := make(map[string]int)
    	for _, f := range strings.Fields(s) {
    		m[f]++
    	}
    	return m
    }
    
    func main() {
    	wc.Test(WordCount)
    }
    
</div>
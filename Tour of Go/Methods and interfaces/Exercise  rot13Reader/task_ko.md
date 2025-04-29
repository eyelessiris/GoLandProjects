# 연습: rot13Reader

일반적인 패턴은 다른 `io.Reader`를 감싸서 스트림을 어떤 방식으로든 수정하는 [io.Reader](https://go.dev/pkg/io/#Reader)입니다.

예를 들어, [gzip.NewReader](https://go.dev/pkg/compress/gzip/#NewReader) 함수는 `io.Reader`(압축된 데이터 스트림)를 받아들이고, `*gzip.Reader`(압축 해제된 데이터 스트림)를 반환하며, 이것 역시 `io.Reader`를 구현합니다.

`rot13Reader`를 구현하여 `io.Reader`를 구현하고, `io.Reader`에서 읽으며 모든 알파벳 문자를 [rot13](https://en.wikipedia.org/wiki/ROT13) 치환 암호를 적용하여 스트림을 수정하세요.

`rot13Reader` 타입은 이미 제공되었습니다.  
`Read` 메서드를 구현하여 이를 `io.Reader`로 만드세요.

<div class="hint" title="가능한 해결책 보기">

    package main
    
    import (
    	"io"
    	"os"
    	"strings"
    )
    
    // rot13 암호화 함수
    func rot13(b byte) byte {
    	var a, z byte
    	switch {
    	case 'a' <= b && b <= 'z': // 소문자 처리
    		a, z = 'a', 'z'
    	case 'A' <= b && b <= 'Z': // 대문자 처리
    		a, z = 'A', 'Z'
    	default:
    		return b // 알파벳이 아닌 경우 그대로 반환
    	}
    	return (b-a+13)%(z-a+1) + a
    }
    
    // rot13Reader 타입 정의
    type rot13Reader struct {
    	r io.Reader // 내부 Reader 필드
    }
    
    // Read 메서드 구현
    func (r rot13Reader) Read(p []byte) (n int, err error) {
    	n, err = r.r.Read(p) // Reader에서 데이터 읽기
    	for i := 0; i < n; i++ {
    		p[i] = rot13(p[i]) // 각 바이트에 rot13 적용
    	}
    	return
    }
    
    func main() {
    	s := strings.NewReader(
    		"Lbh penpxrq gur pbqr!") // 테스트 문자열
    	r := rot13Reader{s}
    	io.Copy(os.Stdout, &r) // 결과 출력
    }
    
</div>
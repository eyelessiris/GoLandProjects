# 연습: Readers

ASCII 문자 `'A'`의 무한 스트림을 출력하는 `Reader` 타입을 구현하세요.

<sub>**참고:** _import_ 섹션의 종속성이 빨간색으로 강조 표시되면, 해당 종속성을 클릭하고, <span class="shortcut">&shortcut:ShowIntentionActions;</span>를 누른 후 **Sync dependencies of main**을 선택하세요.</sub>

<div class="hint" title="가능한 해결 방법을 보려면 클릭하세요">

    package main
    
    import "golang.org/x/tour/reader"
    
    type MyReader struct{}
    
    // Read 메서드는 'A' 문자를 버퍼에 채웁니다.
    func (r MyReader) Read(b []byte) (int, error) {
    	for i := range b {
    		b[i] = 'A'
    	}
    	return len(b), nil
    }
    
    func main() {
    	reader.Validate(MyReader{})
    }
    
</div>
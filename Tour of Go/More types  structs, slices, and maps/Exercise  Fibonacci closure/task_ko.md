# 연습: 피보나치 클로저

함수로 재미있게 놀아봅시다.

`fibonacci` 함수를 구현하여 해당 함수가 [피보나치 수](https://en.wikipedia.org/wiki/Fibonacci_number)
(0, 1, 1, 2, 3, 5, ...)의 순차적인 값을 반환하는 함수(클로저)를 반환하도록 하세요.

<div class="hint" title="Click to see possible solution">

    package main
    
    import "fmt"
    
    // fibonacci는 정수를 반환하는
    // 함수를 반환하는 함수입니다.
    func fibonacci() func() int {
    	f, g := 1, 0
    	return func() int {
    		f, g = g, f+g
    		return f
    	}
    }
    
    func main() {
    	f := fibonacci()
    	for i := 0; i < 10; i++ {
    		fmt.Println(f())
    	}
    }
    
</div>
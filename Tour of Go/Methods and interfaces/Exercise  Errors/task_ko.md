# 연습: Errors

이전 연습의 `Sqrt` 함수를 [여기에서 가져오기](course://%20Flow%20control%20statements%3A%20for%2C%20if%2C%20else%2C%20switch%20and%20defer/Exercise%3A%20Loops%20and%20Functions/taks.go)하여 수정하고 `error` 값을 반환하도록 수정하세요.

`Sqrt` 함수는 복소수를 지원하지 않으므로, 음수 입력 시 nil이 아닌 오류 값을 반환해야 합니다.

새로운 타입을 생성하세요.

```go
type ErrNegativeSqrt float64
```

그리고 아래와 같이 메서드를 추가하여 이를 `error`로 만드세요.

```go
func (e ErrNegativeSqrt) Error() string
```

위 메서드는 `ErrNegativeSqrt(-2).Error()` 호출 시 `"cannot Sqrt negative number: -2"`라는 문자열을 반환해야 합니다.

*참고:* `Error` 메서드 내부에서 `fmt.Sprint(e)`를 호출하면 프로그램이 무한 루프에 빠질 수 있습니다. 이를 피하려면 먼저 `e`를 변환하세요: `fmt.Sprint(float64(e))`. 왜 그럴까요?

`Sqrt` 함수를 수정하여 음수 입력 시 `ErrNegativeSqrt` 값을 반환하도록 만드세요.

<div class="hint" title="해결 방안 보기">

```go
package main

import (
	"fmt"
	"math"
)

type ErrNegativeSqrt float64

func (e ErrNegativeSqrt) Error() string {
	return fmt.Sprintf("Sqrt: negative number %g", e)
}

const delta = 1e-10

func Sqrt(f float64) (float64, error) {
	if f < 0 {
		return 0, ErrNegativeSqrt(f)
	}
	z := f
	for {
		n := z - (z*z-f)/(2*z)
		if math.Abs(n-z) < delta {
			break
		}
		z = n
	}
	return z, nil
}

func main() {
	fmt.Println(Sqrt(2))
	fmt.Println(Sqrt(-2))
}
```

</div>
# 문자열 변환기(Stringers)

가장 널리 쓰이는 인터페이스 중 하나는 [`fmt`](https://go.dev/pkg/fmt/) 패키지에서 정의된 [`Stringer`](https://go.dev/pkg/fmt/#Stringer)입니다.

	type Stringer interface {
		String() string
	}

`Stringer`는 자신의 값을 문자열로 표현할 수 있는 타입입니다. `fmt` 패키지(그리고 여러 다른 패키지들)는 값을 출력하기 위해 이 인터페이스를 찾습니다.
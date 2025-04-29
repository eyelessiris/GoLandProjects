# 에러

Go 프로그램은 `error` 값을 사용하여 에러 상태를 표현합니다.

`error` 타입은 `fmt.Stringer`와 유사한 내장 인터페이스입니다:

	type error interface {
		Error() string
	}

(`fmt.Stringer`와 마찬가지로, `fmt` 패키지는 값을 출력할 때 `error` 인터페이스를 찾습니다.)

함수는 종종 `error` 값을 반환하며, 호출하는 코드는 에러가 `nil`과 동일한지 테스트하여 에러를 처리해야 합니다.

	i, err := strconv.Atoi("42")
	if err != nil {
		fmt.Printf("숫자를 변환할 수 없습니다: %v\n", err)
		return
	}
	fmt.Println("변환된 정수:", i)

`error`가 nil이면 성공을 나타내고, nil이 아닌 경우는 실패를 나타냅니다.
# 기본 타입

Go의 기본 타입은 다음과 같습니다:

	bool

	string

	int  int8  int16  int32  int64  
	uint uint8 uint16 uint32 uint64 uintptr  

	byte // uint8의 별칭

	rune // int32의 별칭  
	     // 유니코드 코드 포인트를 나타냄

	float32 float64  

	complex64 complex128  

다음 예제는 여러 타입의 변수를 보여줍니다.  
또한, 변수 선언이 `import` 문과 같이 블록으로 "구성"될 수 있다는 것을 나타냅니다.

`int`, `uint`, 그리고 `uintptr` 타입은 보통 32비트 시스템에서는 32비트, 64비트 시스템에서는 64비트로 할당됩니다.  
정수 값이 필요할 때는 특별히 크기나 부호가 없는 정수 타입을 사용할 이유가 없다면 `int`를 사용하는 것이 좋습니다.
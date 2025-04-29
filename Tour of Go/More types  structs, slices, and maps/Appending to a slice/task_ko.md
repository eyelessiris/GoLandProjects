# 슬라이스에 요소 추가하기

슬라이스에 새 요소를 추가하는 것은 흔한 작업이며, Go는 이를 위해 내장된 `append` 함수를 제공합니다. 내장 패키지의 [문서](https://go.dev/pkg/builtin/#append)는 `append`에 대해 설명하고 있습니다.

	func append(s []T, vs ...T) []T

`append`의 첫 번째 매개변수 `s`는 타입 `T`의 슬라이스이고, 나머지는 슬라이스에 추가할 `T` 값들입니다.

`append`의 결과 값은 원래 슬라이스의 모든 요소와 제공된 값들을 포함하는 새로운 슬라이스입니다.

만약 `s`의 기본 배열이 제공된 값을 모두 담기에는 너무 작다면, 더 큰 배열이 할당됩니다. 반환된 슬라이스는 새로 할당된 배열을 가리키게 됩니다.

(슬라이스에 대해 더 알아보려면 [Slices: usage and internals](https://go.dev/blog/go-slices-usage-and-internals) 글을 참고하세요.)
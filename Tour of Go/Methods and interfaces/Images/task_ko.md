# 이미지


[패키지 image](https://go.dev/pkg/image/#Image)는 `Image` 인터페이스를 정의합니다:

	package image

	type Image interface {
		ColorModel() color.Model
		Bounds() Rectangle
		At(x, y int) color.Color
	}

*참고*: `Bounds` 메서드의 `Rectangle` 반환값은 실제로 [`image.Rectangle`](https://go.dev/pkg/image/#Rectangle)입니다. 이는 선언이 `image` 패키지 내부에 있기 때문입니다.

(모든 세부 사항은 [문서](https://go.dev/pkg/image/#Image)를 참조하십시오.)

`color.Color`와 `color.Model` 타입도 인터페이스이지만, 여기서는 미리 정의된 구현체인 `color.RGBA`와 `color.RGBAModel`을 사용하여 이를 무시하겠습니다. 이 인터페이스와 타입은 [image/color 패키지](https://go.dev/pkg/image/color/)에 의해 정의됩니다.
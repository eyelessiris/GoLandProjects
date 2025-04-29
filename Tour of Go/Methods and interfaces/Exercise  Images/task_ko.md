# 연습 문제: 이미지

이전에 작성한 [그림 생성기](course://%20Methods%20and%20interfaces/Exercise%3A%20Images/task.go)를 기억하시나요? 이번에는 데이터를 담은 슬라이스 대신 `image.Image` 인터페이스를 구현하도록 반환하는 또 다른 생성기를 작성해 봅시다.

자신만의 `Image` 타입을 정의하고, [필수 메서드들](https://go.dev/pkg/image/#Image)을 구현한 뒤 `pic.ShowImage`를 호출하세요.

`Bounds`는 `image.Rect(0, 0, w, h)`와 같은 `image.Rectangle`을 반환해야 합니다.

`ColorModel`은 `color.RGBAModel`을 반환해야 합니다.

`At` 메서드는 색상을 반환해야 하며, 이전 그림 생성기의 값 `v`는 이번에는 `color.RGBA{v, v, 255, 255}`에 해당합니다.

<sub>**참고:** _import_ 섹션의 의존성이 빨간색으로 강조 표시되면, 해당 의존성을 클릭한 뒤 <span class="shortcut">&shortcut:ShowIntentionActions;</span>을 눌러 **main의 의존성 동기화**를 선택하세요.</sub>

<div class="hint" title="가능한 해결 방법 보기">

    package main
    
    import (
    	"image"
    	"image/color"
    
    	"golang.org/x/tour/pic"
    )
    
    type Image struct {
    	Height, Width int
    }
    
    func (m Image) ColorModel() color.Model {
    	return color.RGBAModel
    }
    
    func (m Image) Bounds() image.Rectangle {
    	return image.Rect(0, 0, m.Height, m.Width)
    }
    
    func (m Image) At(x, y int) color.Color {
    	c := uint8(x ^ y)
    	return color.RGBA{c, c, 255, 255}
    }
    
    func main() {
    	m := Image{256, 256}
    	pic.ShowImage(m)
    }
    
</div>
# 연습: 슬라이스

`Pic`을(를) 구현하십시오. 이 함수는 길이가 `dy`인 슬라이스를 반환해야 하며, 각 요소는 길이가 `dx`인 8비트 부호 없는 정수(`uint8`)로 이루어진 슬라이스입니다. 프로그램을 실행하면, 정수를 그레이스케일(정확히는 블루스케일) 값으로 해석하여 그림을 표시합니다.

이미지는 여러분의 선택에 달려 있습니다. 흥미로운 함수의 예로는 `(x+y)/2`, `x*y`, 그리고 `x^y` 등이 있습니다.

(`[][]uint8` 내부에 각 `[]uint8`을 할당하려면 반복문을 사용해야 합니다.)

(유형 간 변환을 위해서는 `uint8(intValue)`를 사용하십시오.)

<sub>**참고:** _import_ 섹션의 의존성이 빨간색으로 강조 표시된다면, 의존성을 클릭하고, <span class="shortcut">&shortcut:ShowIntentionActions;</span>를 누른 후 **Sync dependencies of main**을 선택하십시오.</sub>

<div class="hint" title="해결 방안을 보려면 클릭">

    package main
    
    import "golang.org/x/tour/pic"
    
    func Pic(dx, dy int) [][]uint8 {
    	p := make([][]uint8, dy)
    	for i := range p {
    		p[i] = make([]uint8, dx)
    	}
    
    	for y, row := range p {
    		for x := range row {
    			row[x] = uint8(x * y)
    		}
    	}
    
    	return p
    }
    
    func main() {
    	pic.Show(Pic)
    }
    
</div>
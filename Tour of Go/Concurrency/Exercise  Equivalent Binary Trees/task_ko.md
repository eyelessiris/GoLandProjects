# 연습문제: 동일한 이진 트리

같은 값의 순서를 저장하는 여러 가지 다양한 이진 트리가 있을 수 있습니다. 예를 들어, 아래의 이진 트리 두 개는 순서 1, 1, 2, 3, 5, 8, 13을 저장하고 있습니다.

![Tree Image](tree.png)

두 이진 트리가 동일한 순서를 저장하는지 확인하는 함수는 대부분의 언어에서 꽤 복잡합니다. 우리는 Go의 동시성(concurrency)과 채널을 사용해 간단한 해결책을 작성할 것입니다.

이 예제는 `tree` 패키지를 사용하며, 이 패키지는 다음과 같은 타입을 정의합니다:

```go
type Tree struct {
	Left  *Tree
	Value int
	Right *Tree
}
```

**1.** `Walk` 함수를 구현하세요.

**2.** `Walk` 함수를 테스트하세요.

`tree.New(k)` 함수는 값 `k`, `2k`, `3k`, ..., `10k`를 항상 정렬된 상태로나타내는 무작위 구조의 이진 트리를 생성합니다.

새 채널 `ch`를 만들고 walker를 시작하세요:

```go
go Walk(tree.New(1), ch)
```

그 후 채널에서 10개의 값을 읽고 출력하세요. 1, 2, 3, ..., 10 숫자가 출력되어야 합니다.

**3.** `t1`과 `t2`가 동일한 값을 저장하는지 확인하기 위해 `Walk`를 사용하여 `Same` 함수를 구현하세요.

**4.** `Same` 함수를 테스트하세요.

`Same(tree.New(1), tree.New(1))`는 true를 반환해야 하고, `Same(tree.New(1), tree.New(2))`는 false를 반환해야 합니다.

`Tree`에 대한 문서는 [여기](https://godoc.org/golang.org/x/tour/tree#Tree)에서 찾을 수 있습니다.

<sub>**참고:** _import_ 섹션의 의존성이 빨간색으로 표시되면, 의존성을 클릭하고, <span class="shortcut">&shortcut:ShowIntentionActions;</span>를 누른 후 **Sync dependencies of main**을 선택하세요.</sub>

<div class="hint" title="가능한 해결책을 보려면 클릭하세요">

```go
package main

import (
	"fmt"
	"golang.org/x/tour/tree"
)

func walkImpl(t *tree.Tree, ch chan int) {
	if t == nil {
		return
	}
	walkImpl(t.Left, ch)
	ch <- t.Value
	walkImpl(t.Right, ch)
}

// Walk 함수는 트리 t를 순회하며
// 모든 값을 채널 ch에 보냅니다.
func Walk(t *tree.Tree, ch chan int) {
	walkImpl(t, ch)
	// 여기서 채널을 닫아야 합니다.
	close(ch)
}

// Same 함수는 트리 t1과 t2가
// 동일한 값을 포함하는지 확인합니다.
// 참고: 트리가 다를 경우 이 구현은 고루틴을 누출합니다.
// 더 나은 해결책은 binarytrees_quit.go를 참조하세요.
func Same(t1, t2 *tree.Tree) bool {
	w1, w2 := make(chan int), make(chan int)

	go Walk(t1, w1)
	go Walk(t2, w2)

	for {
		v1, ok1 := <-w1
		v2, ok2 := <-w2
		if !ok1 || !ok2 {
			return ok1 == ok2
		}
		if v1 != v2 {
			return false
		}
	}
}

func main() {
	fmt.Print("tree.New(1) == tree.New(1): ")
	if Same(tree.New(1), tree.New(1)) {
		fmt.Println("PASSED")
	} else {
		fmt.Println("FAILED")
	}

	fmt.Print("tree.New(1) != tree.New(2): ")
	if !Same(tree.New(1), tree.New(2)) {
		fmt.Println("PASSED")
	} else {
		fmt.Println("FAILED")
	}
}
```

</div>
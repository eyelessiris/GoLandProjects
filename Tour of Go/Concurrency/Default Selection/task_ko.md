# 기본 선택

`select`에서 `default` 케이스는 다른 케이스가 준비되지 않은 경우 실행됩니다.

`default` 케이스를 사용하여 블로킹 없이 송수신을 시도할 수 있습니다:

	select {
	case i := <-c:
		// i 사용
	default:
		// c에서 수신하면 블로킹됩니다
	}
# 맵 수정하기

맵 `m`에 요소를 삽입하거나 업데이트하기:

	m[key] = elem

요소를 가져오기:

	elem = m[key]

요소 삭제하기:

	delete(m, key)

두 값 할당으로 키가 존재하는지 확인하기:

	elem, ok = m[key]

`key`가 `m`에 있으면 `ok`는 `true`입니다. 그렇지 않으면 `ok`는 `false`입니다.

`key`가 맵에 없으면, `elem`은 맵 요소 타입의 기본값이 됩니다.

*참고:* `elem`이나 `ok`가 아직 선언되지 않았다면 짧은 선언 형식을 사용할 수 있습니다:

	elem, ok := m[key]
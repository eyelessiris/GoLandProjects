# range 계속

인덱스나 값을 생략하려면 `_`에 할당하세요.

    for i, _ := range pow
    for _, value := range pow

인덱스만 필요하다면 두 번째 변수를 생략할 수 있습니다.

    for i := range pow
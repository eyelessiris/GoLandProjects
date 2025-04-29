# defer의 스택 사용

지연(defer)된 함수 호출은 스택에 쌓입니다. 함수가 반환될 때, 지연 호출된 함수들은 후입선출(LIFO, Last-In-First-Out) 순서로 실행됩니다.

defer 문에 대해 더 알고 싶다면, 이 [블로그 게시물](https://go.dev/blog/defer-panic-and-recover)을 읽어보세요.
# 리더(Readers)

`io` 패키지는 `io.Reader` 인터페이스를 정의하며, 이는 데이터 스트림의 읽기 끝 부분을 나타냅니다.

Go 표준 라이브러리에는 이 인터페이스를 구현한 [다양한 구현체들](https://cs.opensource.google/search?q=Read%5C(%5Cw%2B%5Cs%5C%5B%5C%5Dbyte%5C)&ss=go%2Fgo)이 포함되어 있으며, 여기에는 파일, 네트워크 연결, 압축기, 암호화기 등이 있습니다.

`io.Reader` 인터페이스는 `Read` 메서드를 가지고 있습니다:

	func (T) Read(b []byte) (n int, err error)

`Read` 메서드는 주어진 바이트 배열을 데이터로 채우고, 채워진 바이트 수와 오류 값을 반환합니다. 스트림이 끝날 때는 `io.EOF` 오류를 반환합니다.

다음 예제 코드는 [`strings.Reader`](https://go.dev/pkg/strings/#Reader)를 생성하고, 그 출력을 8 바이트씩 읽어서 소비합니다.
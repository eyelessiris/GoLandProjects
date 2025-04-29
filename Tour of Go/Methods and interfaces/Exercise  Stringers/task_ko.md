# 연습: Stringers

`IPAddr` 타입이 `fmt.Stringer`를 구현하여 주소를 점으로 구분된 쿼드 형식으로 출력하도록 만드세요.

예를 들어, `IPAddr{1, 2, 3, 4}`는 `"1.2.3.4"`로 출력되어야 합니다.

<div class="hint" title="해결 방법 보기 클릭">

    package main
    
    import "fmt"
    
    type IPAddr [4]byte
    
    // IPAddr 타입의 String 메서드를 구현합니다.
    func (ip IPAddr) String() string {
    	return fmt.Sprintf("%d.%d.%d.%d", ip[0], ip[1], ip[2], ip[3])
    }
    
    func main() {
    	addrs := map[string]IPAddr{
    		"loopback":  {127, 0, 0, 1},   // 루프백 주소
    		"googleDNS": {8, 8, 8, 8},    // 구글 DNS 주소
    	}
    	for n, a := range addrs {
    		fmt.Printf("%v: %v\n", n, a)  // 이름과 주소를 출력합니다.
    	}
    }
    
</div>
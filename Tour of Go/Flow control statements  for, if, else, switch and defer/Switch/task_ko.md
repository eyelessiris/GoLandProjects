# 스위치

`switch` 문은 `if`-`else` 문을 더 간결하게 작성할 수 있는 방법입니다.  
조건 표현식과 값이 같은 첫 번째 case를 실행합니다.

Go의 switch는 C, C++, Java, JavaScript, PHP의 switch와 비슷하지만,  
Go는 선택된 case만 실행하며 뒤따르는 다른 case는 실행하지 않습니다.  
즉, 이러한 언어들에서 각 case의 끝에 필요했던 `break` 문이 Go에서는 자동으로 제공됩니다.  
또 다른 중요한 차이점은, Go의 switch case는 반드시 상수일 필요가 없으며,  
사용되는 값이 반드시 정수일 필요도 없습니다.
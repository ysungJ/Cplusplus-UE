## 3장. 표현식과 문장 
--------------------

### 3.1 표현식의 개요 
---------------------
표현식은 특정 값을 가진 엔티티이며, 메모리의 상태를 변경할 수 있음. 

메모리의 상태를 조작하는 행위를 **Side-Effect**라고한다.

표현식은 단순한 값을 만들거나 연산자를 사용해 값들을 결합해서 또 다른 새로운 값을 만드는 식

즉, 표현식과 표현식을 사용해서 새로운 표현식을 만들 수 있음 


### lvalue와 rvalue 

할당 연산자 왼쪽에 놓는 엔티티는 lvalue<br>
오른쪽 엔티티는 rvalue <br>
즉 값의 목적지는 lvalue, 값의 소스는 rvalue <br>

### 3.2 암묵적 자료형 변환과 명시적 자료형 변환
---------------------------------------------
### 암묵적 자료형 변환 

서로 다른 자료형을 연산시, C++ 컴파일러는 연산 전에 암묵적 자료형 변환을 실행 <br>
즉, 피연산자의 자료형을 적용할 수 있는 다른 자료형으로 자동으로 변환 하는것을 의미 <br>

### 명시적 자료형 변환 (캐스팅)

피연산자의 자료형을 원하는 형태로 강제로 변환하는 것을 명시적 자료형 변환 또는 캐스팅이라고함 <br>


### 3.3 오버플로우와 언더플로우
--------------------
자료형의 최대 값보다 크거나 최소값 보다 작은 값을 저장하려고 하면 문제가 발생 <br>
오버플로우와 언더플로우는 간단한 경고 메세지를 출력해 줄 떄가 있긴하지만 **오류 메세지**를 생성하지 않음 <br>

## 3.4 조정자 (mainpulator)
-----------------------
### 숫자 진법 변경 
dec -> 10진수, oct -> 8진수 hex ->16진수 변환 출력<br>
* 진법의 접두사를 붙이는 조정자 : noshowbase, showbase<br> 
8진수는 0, 16진수는 0x가 접두사로 붙여서 각각의 진법으로 표현<br>
* 고정 소수점 출력 조정자와 과학 표기법 출력 조정자 <br>
고정 소수점 출력 : fixed <br>
고정 소수점 형식 : 부호, 정수 부분 . 소수점 아래 부분<br>
과학 표기법 출력 : scientific <br>
과학 표기법 형식 : 부호, 정수 부분이 한 자리로 고정, e or E, 지수 부호, 지수<br>

* 소수점 아래 부분을 출력하는 조정자 showpoint <br> 
소수점 아래부분이 0일 때, 소수점 아래부분을 출력하지않지만 showpoint를 사용하면 소수점 아래부분이 0일 때도 출력

* 양수 부호를 붙이는 조정자 showpos <br>
부호가 양수가 일 때  +는  출력 하지 않지만  - 음수 부호만 출력 됨<br> 
showpos를 사용시 양수부호 일 때도 + 부호를 출력 가능

* 숫자 관련 문자를 대문자로 출력하는 조정자  uppercase <br>
16진수를 정수를 출력 할 때, 알파벳이 출력되고, 부동 소수점의 과학 표기법 때도 알파벳 e가 출력됨<br>
기본적으로 소문자로 출력함으로, 대문자 변경시에 사용

* 숫자 배치를 조정하는 조정자 left, internal, right <br>
정해진 크기의 영역을 잡고나면 left, internal, right 조정자를 사용해서<br> 
숫자 배치를 조정 할 수 있음 

left 형식은 숫자를 왼쪽에 붙이고 오른쪽 부분은 패딩으로 남김 <br> 
internal 형식은 부호를 왼쪽에 붙이고 숫자는 오른쪽에 붙인 뒤 중간에 남은 부분을 패딩으로 둠 <br> 
right 형식은 부호와 숫자를 오른쪽에 붙이고 왼쪽 부분을 패딩으로 둠 <br> 
이들은 스트림의 상태를 변경하지 않음

* 매개변수 조정자 <br> 
매개변수가 있는 조정가는 헤더파일 <iomanip>를 사용해야함 <br> 
setprecision(n), setw(n), setfill(ch)이 있음 <br> 

+ setprecision(n) <br> 
고정 소수점 출력 방식에서만 사용, 괄호 안의 정수 (n)로 소수점 뒤의 몇 자리 까지 출력할지 정함

+ setw(n) <br> 
고정 소수점 출력 방식에서만 사용, 괄호 안의 정수(n)은 전체 필드 크기를 의미 <br> 
이 때 필드 크기는 정수 부분, 소수점, 소수점 아래부분을 모두 합친 길이 <br> 
setw조정자는 출력 스트림의 상태를 변경하지 않아, 필요할 때 마다 사용 <br> 
setw조정자를 제외하고 매개변수가 있는 조정자는 출력스트림의 형태를 변경  <br> 

+ setfill(ch) <br> 
필드의 크기가 실제 출력되는 내용보다 클 때, 발생하는 패딩을 어떤 문자로 채울지 지정할 때 사용 <br> 
괄호 안에는 리터럴 문자를 넣고 left, center, right, setw등과 조합하여 사용 

* 입력 조정자 
출력할 때 사용하는 조정자 처럼, 입력할 때 사용할 수 있는 조정자가 있음 <br> 
ex) noboolalpha, boolalpha <br> 
dec, oct, hex 등... 

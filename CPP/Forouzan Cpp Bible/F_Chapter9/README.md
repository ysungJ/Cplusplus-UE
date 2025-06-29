## Chapter9 참조, 포인터, 메모리 관리 

-----------------------------------
### 9-1 참조

* #### 참조 변수와 참조 자료형
  참조(Reference)는 객체의 또 다른 이름 <br>
  C++에서 추가된 기능으로, 함수 등의 엔티티끼리 커뮤니케이션하는걸 쉽게 만들어줌 <br>

+ ##### 참조 변수 (reference variable)
 reference variable는 일반적인 변수와 다르게 메모리 위에 새로운 영역을 잡지 않음<br>
 단순하게 기준에 있던 변수와 바인드해서 기존에 있던 변수에 새로운 이름을 붙여 주기에, **원본 변수**가 있어야만 생성할 수 있음. <br>
 
+ ##### 참조 자료형
  원본 변수와 참조 변수가 같은 메모리 위치를 가리키므로 **값**은 같지만, **자료형**은 다르다. <br>
  참조 변수는 참조 자료형이라는 새로운 자료형을 뜻함. <br>
  참조 자료형은 복합 자료형으로 자료형 + & 형식으로 이루어짐. <br>
  변수를 참조 변수와 연결할 때는 반드시 **변수의 자료형과 참조 변수가 나타내는 자료형**이 일치해야한다.

  ```cpp
  int num = 100;
  doulbe& rNum = num; //자료형이 다르므로 컴파일 오류 발생.
  ```

* ##### 참조 관계
  참조가 선언되고 어떤 변수와 연결되면 참조 관계는 스코프를 벗어나서 변수가 파괴되기 전까지는 계속해서 유지 됨.<br>
  즉 **참조 관계는 한 번 정의되면 변경 불가** <br>
  C++에서는 변수와 참조 변수가 연결된 관계를 **constant relation**이라고 표현

  ```cpp
  int score = 92;
  int& rScore = socre;
  int num = 80;
  int* rScore = num; // 컴파일 오류 - 참조 관계를 깨버림
  ```
  
  ```cpp
  int score = 92;
  int& rScore = socre;
  int num = 80;
  rScore = num; // 정상 작동
  ```

  2번째 코드에서 rScore = num;는 참조 관계를 깨버린 것이 아니다. **공유하고 있는 메모리 위치에 num의 값을 넣은 것이지**, 참조 연결을 하는 문장이 아님<br>
  참고로 rScore는 score의 별칭이므로 rScore = num은 score = num과 같은 기능을 한다.

  * ##### 참조 다중성
    하나의 변수를 기반으로 여러 개의 참조 변수를 만들 수 있지만 반대는 불가능 <br>
    즉, 참조 변수 하나를 여러 변수에 연결할 수 없음.<br>
    
```cpp
int num = 100;
int& rNum1 = num;
int& rNum2 = num;
int& rNum3 = num;
int& rNum4 = num;
```
위의 코드는 num 변수를 기반으로 4개의 참조 변수를 만드는 예시

하지만, 참조 변수 하나를 여러 변수와 연결하려고 하면 컴파일 오류가 발생<br>
같은 이름으로 변수를 생성하는 것도 불가능하고 constant relation을 끊는 것도 불가능하기 때문<br>

```cpp
int num1 = 100;
int num2 = 200;
int& rNum = num1;
int& rNum = num2;
```

위의 코드에서, 마지막 코드는 컴파일 오류가 발생한다. 즉 rNum은 num1와 연결되어 있어 num2와 연결을 할 수 없기 때문이다. <br>
참고로 **참조 변수에 단순한 값을 연결하는 것**은 불가능하다.  

```cpp
int& a = 200;
```

즉, 위의 코드는 불가능하다. 

  * #### 값 추출
    참조 관계가 만들어지면, 원본 변수와 참조 변수 중에 아무 것이나 사용해도 값에 접근하여 값을 추출할 수 있음. <br>
    [9-1 값에 접근하기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-1.cpp)
    
  * #### 값 변경
    참조 관계가 만들어지면, 데이터 변수 또는 참조 변수를 사용해서 원본 값을 변경할 수 있다. <br>
    그런데, 원본 변수에 **const 한정자**가 붙으면 값을 변경할 수 없다<br>
    const는 원본 변수 또는 참조 변수의 앞에 올 수 있다. 이때 **원본 변수에 const변수가 붙였다면, 참조 변수도 같이 const 한정자를 붙여야 한다.** <br>

 ```cpp
  int name = value;
  int &rName = name; // 가능
 ```
원본 변수와 참조 변수 중에 아무 것이나 사용해도 메모리 위치의 값을 변경할 수 있음. 

```cpp
 int name =value; 
 const int &rName = name; //가능 
```
원본 변수를 사용해서 값을 변경할 수 있음, 하지만 참조 변수를 사용해서는 값을 변경할 수 없음.

```cpp
 const int name = value; 
 const int &rName = name; //가능
```
원본 변수와 참조 변수 모두 값을 확인할 때만 사용할 수 있고, 값을 변경할 수 없음. <br>
이를 활용해서 프로그램을 만드는 경우는 거의 없음. 

```cpp
 const int name =value; 
 int &rName = name; // 불가능
```
오류가 발생함. <br>
const 한정자가 붙지 않은 참조 변수에 const 한정자가 붙은 변수를 바인드하면 컴파일 오류가 발생. 원본 변수가 const  한정자로 고정되어 있으므로  참조 변수를 사용해서 값을 변경할 수 있는 방법이 없음. 


* #### 참조의 활용

하나의 함수 내부에서 어떤 메모리 위치에 대한 참조 변수를 모두 만드는 경우는 없음<br>
원본 데이터 변수만 활용해도 값을 확인하고 변경하는 작업이 모두 가능하기 때문 <br> 
주로, 참조 변수는 일반저긍로 함수를 만들 때 처럼 서로 다른 스코프를 갖는 경우에 활용 <br>

두 함수의 커뮤니케이션에서 참조를 활용하는 방법을 알아보자 <br>
**함수의 커뮤니케이션이란 데이터를 전달하고 리턴하는 것을 의미** <br>
**참조를 활용해서 데이터를 전달하는 것을 참조로 전달 (Pass-by-reference)**, **데이터를 리턴하는 것을 참조로 리턴 (Retrun-by-reference)** 이라고 부름 <br>

* ##### 참조로 전달 (Pass by Reference)
  참조로 전달 (Pass by Reference)은 호출하는 함수 쪽에서 호출되는 함수 쪽으로 객체(1 or 그 이상)를 전달하는 것을 의미
  6장에서 값으로 전달(Pass by Value)을 알아봤었고, 이번에는 참조로 전달(Pass by Reference)에 알아본다.
   이 둘의 차이점은 Pass by Value는 모든 바이트를 복사하는 것이고, Pass by Reference은 메모리 위치를 공유하는 것이다.

```cpp
  #include <iostream>
  using namespace std;

  void doIt(int); //프로토타입 - 함수 선언

  int main(void){
   int num = 10;
   doIt(num);
   return 0; 
  }
  void doIt(int num){
//코드
}

```

Pass by Value는 **호출하는 함수 쪽 값(argument)이 호출되는 쪽의 변수(parameter)로 복사 됨**

```cpp
int num2 = num1; 
```
내부적으로는 위의 코드처럼 실행된다고 볼수 있음 

**값으로 전달되는 인수(argumnet)와 매개변수(paramter)가 독립적으로 존재하기 때문에, 매개변수를 변경하는 일이 인수를 변경하는 일에 영향을 주지 않는다.** <br>
이는 상황에 따라 장단점이 발생 <br>
값으로 전달에서 문제가 되는 또 다른 부분은 **복사 비용**인데, 복사 대상 객체가 크다면, 인수를 매개변수로 복사할 때, 많은 복사 비용이 들어감.<br>
즉, 크기가 작은 자료형은 문제가 없지만 클래스처럼 크기가 큰 자료형은 복사할 때는 다른 방법을 고려하는 것이 좋음. 

  ```cpp
  #include <iostream>
  using namespace std;

  void doIt(int&); //프로토타입 - 함수 선언

  int main(void){
   int num = 10;
   doIt(num);
   return 0; 
  }

  void doIt(int& rNum){
//코드 
  }
  ```

```cpp
int& rNum = num;
```
pass by reference에서는 내부적으로 위의 코드처럼 바인드가 됨. <br>
**pass by reference에서 argument와 parameter는 동일한 객체** 그렇기 때문에, 메모리를 추가로 할당하지 않는다. <br>
const한정자를 붙이지 않았다면, parameter를 조작하는 행위가 argument를 조작하는 행위를 함께 동반한다 <br> 
또한, 인수와 매개변수가 동일한 객체이기 때문에 따로 복사할 필요가 없어 복사 비용이 발생하지 않는다. 그래서 클래스처럼 큰 객체를 전달할 때 우선적으로 고려하는 것이 좋다. 

Pass by reference를 장단점을 간단히 정리하자면 <br>
1. 변경을 막아야한다면 작은 객체는 pass by value를 하고 큰 객체는 cosnt 한정자를 붙인 pass by reference를 사용한다 <br> 
2. 변경을 해야한다면 pass by reference를 사용한다.

다만 pass by reference를 사용할 때는 매개변수에 값을 지정할 수 없다 <br>

```cpp
void fun(int& rX){....}
fun(5); // 컴파일 오류 
```
위의 코드에서, rX가 참조 매개변수로, 함수를 호출할 때는 변수를 매개변수로 넣어야한다. 

클래스의 복사 생성자를 만드는 경우에는? <br>
객체를 전달해야 하기때문에 비용이 많이 들 수 있고, pass by value자체가 복사 생성자를 활용하는 것이므로 **복사 생성자에서는 pass value를 사용할 수 없다 (무한 반복에 빠지기 때문에)** <br>
따라서 const 한정자를 붙인 참조를 사용해야한다. 

```cpp
Circle::Circle(const Circle& circle)
: radius(circle.radius){.... }
```

[9-2 pass by reference를 사용해서 스왑함수 만들기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-2.cpp)

* ##### 참조로 리턴 (Retrun by Reference)
  Return by Reference는 호출된 함수에서 호출한 함수쪽으로 객체를 리턴할 때 사용한다.

  * ##### 값으로 리턴(Return by value)의 특징
    Return by value에서 호출된 함수는 다음과 같이 프로타입을 갖고 원하는 자료형의 객체를 리턴한다.

    ```cpp
    type function(....);
    ```
return by value는 간단하게 매개변수 또는 지역 변수의 값을 리턴할 수 있다. 하지만 유일한 단점은 복사 비용임 <br>
리턴 해야하는 객체가 기본형이면 괜찮지만 클래스라면 복사 생성자가 호출될 것이며, 일반적으로 높은 복사 비용이 들어갈 것이다 <br>

  * #### 참조로 리턴(Return by Reference)의 특징
    return by reference에서 호출된 함수는 다음과 같은 프로토 타입을 가지고 원하는 자료형에 대한 참조 리턴을 한다 <br>
    ```cpp
    type& function(....);
    ```
    return by reference는 복사 비용이 없지만, **일반적으로 매개변수와 지역 변수의 값을 리턴할 수 없다** <br>
    **함수가 종료될 때 모든 매개변수와 지역 변수의 값이 파괴되기 때문에**, 객체가 파괴되면 원본 변수가 파괴되므로, 참조 변수가 가리키는 메모리 위치 자체가 사라진다. <br>
    **반대로 말하면 참조 매개변수와 정적 지역변수는 함수가 종료되어도 파괴되지 않아 리턴할 수 있다** <br>

```cpp
  #include <iostream>
  using namespace std;
//return by value
int larger(int x, int y); 

  int main(void){
    int x, y, z;
    x = 10;
    y = 20;
    z = larger(x,y);
    cout << z << "\n";
    return 0;
  }

int larger(int x, int y){

if(x > y) {
return x;
}
return y;
}
```

```cpp
  #include <iostream>
  using namespace std;
//return by reference
  int& larger(int& x, int& y); 

  int main(void){
    int x, y, z;
    x = 10;
    y = 20;
    z = larger(x,y);
    cout << z << "\n";
    return 0;
  }

int& larger(int& x, int& y){

if(x > y) {
return x;
}
return y;
}
```

위의 두 코드는 두 정수 중에 더 큰 정수를 찾는 함수를 만드는 예시 코드이다. <br>
pass by value와 return by value 조합을 사용할 수 있고, pass by reference와 return by reference를 조합해서 사용할 수 있다. 

[9-3. pass by referance를 사용해서 둘 중에 큰 분수 찾기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-3/9-3.cpp)

--------------------------------------------------
* ### 9-2 Pointer 

 * #### 주소
   포인터 - 메모리 위치의 주소를 나타내는 복합자료형, **포인터 변수는 포인터 자료를 갖는 변수** <br>
   주소 - 크게 메모리 주소와 변수의 주소로 구분 가능

+ ##### 메모리 주소 
   컴퓨터의 메모리는 바이트의 연속, 메모리에 접근 가능한 가장 단위는 바이트. <br>
  각각의 바이트에는 주소가 존재하며, 일반적으로 16진수 형식으로 표현함.

  + ##### 변수의 주소
    다양한 자료형(불, 문자, 정수, 부동 소수점, 클래스)등을 사용함 <br>
    이러한 변수는 1바이트 이상의 메모리를 가짐 (bool, char = 1 byte, int, double = 4 byte or 그 이상) <br>
    sizeof를 통해 몇 byte인지 확인할 수 있음. <br>
    변수의 주소는 변수가 차지하는 **첫 번째 바이트의 주소**를 의미.
    변수의 주소를 추출하려면 &연산자를 사용

    [9-4. 변수의 크기, 값, 주소 출력하기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-4.cpp)
    
 * #### 포인터 자료형과 포인터 변수
   + ##### 포인터 자료형
     리터럴 값이 주소인 복합 자료형 <br>
     
   + ##### 포인터 변수
     포인터 자료의 값을 저장할 수 있음<br>
     어떤 자료형의 포인터라도 포인터 자료형은 4 byte 이기에 포인터 변수는 0x00000000 ~ 0xFFFFFFFF까지의 주소 저장이 가능 <br>
     참고로 포인터 자료형 크기는 시스템에 따라 다를 수 있음, 예를 들어 OS가 64비트이고 컴파일러를 64비트 설정으로 변경한 뒤 컴파일하면 포인터 자료형은 8byte가 됨. <br>
     포인터 선언하려면 어떤 자료형의 포인터를 선언할 것인지 지정하고 다른 변수와 마찬가지로 변수를 사용하기 전에 초기화 해야함 <br>
     이때 **리터럴 주소는 초기화 하지않고**, 반드시 기존에 있는 변수의 주소로 초기화해야한다

     ```cpp
     bool* pFlag;
     int* pScore;
     double* pAverage;
     pFlag = &flag;
     pScore = &score;
     pAverage = &average;
     ```

     다음은 포인터 변수가 초기화 할때 발생하는 예시코드 이다.

 ```cpp
  double* pAverage = 0x1234567; // 리터럴 주소 할당 불가 -> 컴파일 오류 
 int num;
 double *p = &num; //int 자로형 변수의 주소 할당 불가 -> 컴파일 오류 
 ```

     
    첫 번째 오류는 포인터 변수에 포인터 리터럴을 직접 할당할 수 없으므로 컴파일 오류가 발생하며, <br>
    두 번째 오류는 double 자료형에 대한 포인터 변수 int자료형의 주소를 할당할 수 없어 컴파일 오류가 발생한다.

 + ##### 간접참조
   포인터 변수를 선언하고 초기화 했다면 **포인터 변수에 저장된 주소를 활용해서 포인트된 변수의 값에 접근할 수 있음** <br>

+ ##### 연산자 정리
  주소 연산자와 간접 참조 연산자 이 두 개의 연산자들은 단항 연산자이다. <br>
  주소 연산자(&)는 피연산자로 변수를 하나 받고 주소를 리턴하고 간접 참조 연산자(*)는 피연산자로 주소를 하나 받고, 포인트되어 있는 변수의 값을 리턴한다. <br>
  &기호는 참조 자료형을 정의할 때 사용하거나 변수의 주소를 얻기 위한 단항 연산자로 사용할 수 도 있고 또한 비트 AND 연산자라는 이항 연산자로 사용 될 수 있다. <br>
  자료형&, &변수, X&Y <br>
  *기호도 포인터 자료형을 정의할 때, 포인트 되어있는 변수의 값에 접근할 때, 또는 곱셈 연산자로도 사용된다.
  
   
 * #### 값 추출
   포인터 관계가 되면, 데이터 변수 또는 포인터 변수를 사용해서 메모리 위치에 저장된 값에 접근할 수 있음.

   [9-5. 직접 참조와 간접참조](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-5.cpp)
 
 * #### const 한정자
 const 한정자를 사용하는 경우는 3가지 경우 <br>
 1. 직접 참조 변경 불가  const int a = 100; <br>
 2. 간접 참조 변경 불가 const int* pAb = &a; <br>
 3. 주소를 변경 할 수 없음 int* const pAb = &a; <br>
1번과 2번은 데이터 변경과 관련 있음. <br>
3번은 데이터 변수와 포인터 변수 사이의 관계를 변경하는 것과 관련됨. <br>

```cpp
int a = 100;
int* pA = &a;
a = 80; // 데이터 변수로 변경
*pA = 90; // 포인터 변수로 변경 
```
const 한정자가 붙지 않아, 데이터 변수와 포인터 변수를 통해서 값을 변경하는 데 어떠한 제한이 없음 <br>

```cpp
const int a = 100;
int* pA = &a; //오류 발생 
```
이 경우 데이터 변수에 바인딩하려고 할 때 컴파일 오류가 발생함. 즉, 포인터 변수는 변수의 주소를 저장할 수 있지만 상수의 주소는 저장할 수 없음 <<br>

```cpp
int a = 100;
const int* pA = &a;
a = 80; // 데이터 변수로 변경
*pA = 90; // 오류 발생 
```
위의 코드에서 데이터 변수로 값을 변경할 수 있지만, 포인터 변수로는 값을 변경할 수 없음. <br>
포인터 변수를 사용해서 값을 변경하려면 오류가 발생 <br>

```cpp
const int a = 100;
const int* pA = &a;
a = 80; // 오류
*pA = 90; // 오류
```

데이터 변수와, 포인터 변수로 값을 모두 변경할 수 없음. 이런 경우는 거의 사용하지 않음 <br>
const는 바인드를 고정할지 안할지 또는 변강할 수 있게 할지 안할지에 따라 달라진다.  <br> 

 * #### 이중 포인터
   포인터 변수는 메모리의 위치를 나타냄. 이러한 포인터 변수도 메모리 위에 위치를 잡고 있음 그러므로 포인터 변수의 포인터 변수가 가능하다  <br>

   ```cpp
   int a = 100;
   const int* pA = &a;
   int** pPA = &pA; //이중 포인터, pPA를 pA에 연결 
   ```
   
 * #### 특수한 포인터
   아무 것도 가리키지 않은 포인터인 NULL Pointer, 모든 것을 가리키는 generic pointer가 존재  <br>

   널 포인터는 C언어에서는 NULL를 사용해서 정의하는 것이 일반적, C++에서는 리터럴 0을 사용해서 하는 것이 일반적 <br>

   ```cpp
   int* p1 = 0;
   int* p2 = 0;
   ```

  이처럼 포인터에 0을 할당해서 포인터가 사용할 수 없다는 걸 나타내는데, 이는 스코프를 벗어나기 전까지 사용할 수 있지만 포인터가 가리키는 데이터에 접근하려고할 때 오류가 발생해서 프로그램이 중단된다는 의미  <br>
  즉 포인터는 널 포인터일 때 False로 반환되고 이 외에는 True로 반환됨.  <br>

 **void pointer는 generic pointer로 모든 자료형의 객체를 가르킬 수 있음.**   <br>
  
  ```cpp
void *p;
int x = 10;
p = &x;
double y =24.6;
p = &y;
```

void 포인터는 적절한 자료형으로 자료형 반환이 일어나기전 까지 간접 참조를 할 수 없음. 

 * #### 포인터의 활용

포인터도 함수 사이의 통신에 활용할 수 있음  <br>
즉, 매개변수로 포인터를 전달하는 포인터 (pass-by-pointer)과 포인터를 리턴하는 포인터 (return by pointer)로 구분함. 

passByPointer는 call by reference와 다르게 메모리 위치를 공유하지 않음 <br>
또한 포인터를 복사하는 과정은 필요하고 pass by value와 다르게 복사 비용이 크지 않음 <br> 

포인터 전달에서 parameter는 arugment의 주소로 서로 바인드된다. const 한정자를 사용하지 않으면 parameter를 변경했을 때 arugment도 함꼐 변경된다. 

변경을 하면 안되는 경우에 작은 객체라면 pass by value를 사용하고, 큰 객체라면 const한정자를 붙여서 pass by refenrece 또는 pass by pointer를 사용함 

[9-6. 포인터 전달](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-6.cpp)

returnByPointer는 호출된 함수에서 호출한 함수쪽으로 포인터를 리턴할 때 사용  <br>
return by reference와 마찬가지로 값 매개변수와 지역 변수의 포인터를 리턴할 수없는 단점이 있음  <br>
함수가 종료될 떄 모든 값 매개변수와 지역 변수가 파괴되어 포인터가 가리킬 대상이 사라지기 때문에  <br>

[9-7. 두 객체 중에 더 큰 값 찾기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-7.cpp)

------------------------------------------------
* ### 9-3 Array & Pointer

* #### 1차원 배열과 포인터 
[9-8. 배열 요소들의 주소를 확인하는 프로그램](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-8.cpp)

[9-9. 인덱스와 포인터를 사용해서 배열의 요소에 접근하기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-9.cpp)

[9-10. 배열 요소의 합 구하기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-10.cpp)

[9-11. 배열의 요소를 거꾸로 만들기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-11.cpp)

* #### 2차원 배열과 포인터

[9-12. 2차원 배열을 함수에 전달하기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-12.cpp)

------------------------------
* #### 9-4 메모리 관리
  메모리는 여러 영억으로 나뉘는데, 크게 코드 메모리, 정적 메모리, 스택 메모리, 힙 메모리로 나뉨 <br>

* ##### Code memory
  프로그램 코드를 보유하는 영역으로, 이 메모리 영역에서는 다른 객체를 선언할 수 없음. <br>
  프로그램 종료시 해제됨 <br>

  * ##### Static memory
    Global object (어떤 함수에도 속하지 않은 함수 외부에 있는 객체)와 Static object를 보유한 영역<br>
    프로그램이 종료되면 모든 객체들을 정리하고 메모리 위에서 해제함. <br>
    
  [9-13. 배열 요소들의 주소를 확인하는 프로그램](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-13.cpp)

* ##### Stack memory
  함수의 지역 변수와 매개변수를 보유, LIFO 구조

**장점**
시스템은 모든 프로그램에 스택 메모리를 사용함. LIFO는 효율적으로 작동 <br>
객체는 함수 스코프 내부에 있을 때 스택 메모리에 유지되고, 함수의 스코프 벗어나면 삭제되어 더이상 접근이 불가능 함<br>

**단점**
스택 메모리는 효율적이지만 2가지 제한이 있음. <br>
1. 컴파일 시점에 객체의 이름을 정의해야함. 즉, 이름이 없는 객체는 스택에 저장할 수 없음 <br>
2. 컴파일 시점에 객체의 크기를 정의해야함. 시스템이 객체의 크기를 모르면 메모리 영역에 할당 훌 수 없기 때문<br>

다른 말로 stack memory는 compile time memory라고도 함. <br>
저장할 모든 객체는 컴파일 시점에 확실하게 이름과 크기가 정의되어 있어야하기 때문임 <br>

```cpp
int main(void){
int size;
cin >> size;
doulbe array[size]; // 컴파일 오류 발생
....
return 0;
}
```

지역 변수 array를 stack memory에 저장할려면 컴파일 시점에 배열의크기를 알아야해서, 위의 코드에서는 오류가 발생한다.

* ##### Heap Memory
  가변 배열을 만들 때 사용. 즉, 컴파일하는 시점에 객체의 크기를 모른다면, 런타임 시점에 메모리의 객체를 만들어야함 <br>
  Heap Memory는 런타임 시점에 객체를 저장할 때 사용 <br>
  Free Memory 또는 Dynamic Memory라고도함 <br>

C++은 스택에 있는 객체만 이름을 가질 수 있어, **힙 메모리의 객체는 자신의 이름을 가질 수 없음** 
힙 메모리에 생성한 객체는 스택 메모리에 있는 포인터로 가리켜야 한다. 즉, 런타임 시점에 메모리에 객체를 만드는 작업은 스택과 힙을 모두 사용한다. 

* new and delete

  new 객체를 생성할 때 사용하고, Heap Memory에 각각의 새로운 메모리 영역에 메모리 공간을 할당해준 역할을 함 <br>
  delete를 하면 해당 포인터는 dangling pointer가 됨 <br>

**주의점** 
+ 1. 메모리할당 없이 제거 - new를 사용하지 않고 delete 사용하는 경우 -> 런타임 오류가 발생 <br>
+ 2. 메모리 누수 - 제거 없이 메모리 할당을 하는 경우. 즉, new를 사용하고 delete를 사용하지 않은 경우 <br>
메모리 누수가 발생하면, 누수가 발생한 메모리 위치 사용 불가, 메모리 부족 현상이 발생할 수 있음. <br>
+ 3. 허상 포인터 (dangling pointer)- 포인터가 가리키고 있는 객체를 delete로 제거했는데, 포인터를 활용하려고 할 때 발생 <br>

  [9-14.힙 메모리에 크기가 유동적인 배열 만들기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-14.cpp)

---------------------------------------
* #### 2차원 배열과 메모리
 2차원 배열 만들 때 3가지 경우로 사용 가능함 <br> 
  1. Stack memory만 사용 
  2. Stack memory and Heap memory 사용 
  3. Heap memory만 사용

 [9-15. 이항계수 찾기](https://github.com/ysungJ/Cplusplus-UE/blob/main/CPP/Forouzan%20Cpp%20Bible/F_Chapter9/9-15.cpp)
    
 -----------------------
* #### Course 클래스 만들기
* #### Matrix 클래스 만들기

   

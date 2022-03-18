
# CHAPTER 3. 연산자    : 컴퓨터에게 작업을 시키는 기호

![1](https://user-images.githubusercontent.com/101503543/159010699-431db46e-9a5b-41a1-905f-a40595e0d2c0.PNG)

<br>

## 산술연산

- 산술연산에서 가장 많이 쓰이는 연산자
+, -,*, /
% (나머지)
- 나눗셈 같은 경우, 정수와 정수의 연산으로 계산하지 않도록 주의!!!
- 연산자 우선순위
— 곱셈(*), 나눗셈(/), 나머지(%) 연산자는 우선 계산.
— but, 괄호를 이용해서 연산의 우선순위를 높여줄 수 있다.

<br>

## 자동증감 연산자 : ++, --

- 연산자는 이용한 후 반드시 그 결과를 어떤 방식으로든 받아줘야 한다.  

<br>
1. 변수를 이용해서 결과를 담거나  
2. 어떤 형태로든 연산된 결과를 사용하거나  

```
int i = 10;
int j = 100;
i + j ; // 컴파일 에러 발생
```

-> 다만, 이 법칙에 지배를 벗어나는 연산이 바로 ‘자동증감 연산’

- 자동증감 연산자 : 별도의 연산 결과를 처리하지 않는 연산자  
++, -- 연산자는 연산 대상에 1을 증가하거나 감소한 후, 연산의 결과를 원래의 변수에 자동으로 대입해줌.  
새로운 변수나 별도의 할당 없이 그냥 사용 가능.  

- 다만, 연산자 위치가 변수의 앞인지 뒤인지에 따라 결과가 다르다.    
<br>

### 1. ++, -- 가 변수 앞에 붙는 경우 : 변수를 사용하기 전(before)에 증감을 먼저 시도하라는 뜻  
면저 해당 변수의 값을 증가 또는 감소하고 나머지 연산을 실행한다.  

```
int a = 0;
int b = 10;
System.out.println(++a) ;
System.out.println(--b) ;
// 결과 : 1과 9
```

a 변수는 먼저 +1한 후, System.out.println()에서 활용되므로 a의 값은 1  
b 변수는 먼저 -1한 후, 활용되므로 b의 값은 9  

<br>

### 2. ++, --가 변수 뒤에 붙는 경우 : 변수를 사용한 후(after) 1씩 더하거나 뺀다

```
int a = 0;
int b = 10;

System.out.println(a++);
System.out.println(b++);

System.out.println(“변경 후”);
System.out.println(a);
System.out.println(b);
// 결과값 :
0
10
변경후
1
11
```

-> 변수를 먼저 활용하므로 위쪽 system.out.println에선 기존의 값 0과 10이 그대로 유지  
이후 증감된 후 아래쪽 System.out.println에선 1과 11로 출력된다.  

<br>

### 3. 자동증감 연산자가 섞여 있는 경우
```
int x = 5;
int y = 10;
int z = x++ + ++x + y++ ;
System.out.println(z);
// 결과 : 22
```
x++ : 먼저 사용된 후 +1이므로, 여기서는 5  
++x : 앞서 x++에서 사용되고 +1되어 넘어오므로 x는 6 / ++x 에선 먼저 +1되고 사용되므로 7  
y++ : 먼저 사용된 후 +1이므로, 기존의 값 10 그대로  
따라서, z = 5 + 7 + 10 인 상태로 계산되고 system으로 넘어와 22로 출력된다.  

<br>

## 동등 비교(Equality) 및 관계(Relational) 연산자

- 비교 및 관계 연산자 : 부등호, 같다(==), 다르다(!=) 연산할 때 사용
- 특히 같다(==), 다르다(!=) 중요 (프로그램을 만들면서 가장 많이 하는 작업이 ‘비교’이기 떄문)
a == b // a와 b 변수의 내용물이 같으면 true 반환
a != b // a와 b 변수의 내용물이 다르면 true 반환

<br>

## 비트 연산자 : |, &, ^

- 비트 연산자 : 컴퓨터가 쉽게 이해하는 연산 기호 (속도 향상)  
(but CPU 성능이 비약적으로 향상된 요즘엔 많이 사용되지 않음)  

| (OR) : 양쪽 데이터의 비트 값을 OR 조건으로 따져서 한쪽 bit가 1이면 무조건 1이라는 결과를 낸다.  
& (AND) : 양쪽의 비트가 모두 1이면 1 / 아니면 0  
^ (XOR)  : 양쪽의 비트가 서로 다른 비트를 가져야만 1 / 아닐 경우 0  

```
int x = 3;
int y = 2;
System.out.println (x|y) ;
System.out.println (x&y) ;
System.out.println (x^y) ;
// 결과 : 3, 2, 4
```

![2](https://user-images.githubusercontent.com/101503543/159005231-c2240491-f1ba-47e3-923a-4062d0873f6c.PNG)
![3](https://user-images.githubusercontent.com/101503543/159005234-5b8f1211-5704-46e2-bb19-c505d78b2d08.PNG)
![4](https://user-images.githubusercontent.com/101503543/159005236-8cf991f0-1db6-4f48-af59-5ead9a655119.PNG)

```
int x = 3 | 2;
System.out.println(“OR 연산 : “ + x);

int y = 3 & 2;
System.out.println(“AND 연산 : “ + y);

int z = 7 ^ 3;
System.out.println(“XOR 연산 : “ + x);

// OR 연산 : 3
// AND 연산 : 2
// XOR 연산 : 4
```

<br>

## 논리 연산자 : &&, ||

- 논리 연산자는 여러 가지 조건, 상황을 종합적으로 검토해야 하는 경우 많이 사용 (주로 ‘제어문’)  
- 예1) 오늘 비가 오고, 온도가 낮으면 차를 타고 가겠다.  
지하철이나, 버스를 타고 오면 물건을 살 수 없다.  
// 논리적인 상황들을 결합해서 사용  
  
- 예2) 프로그래밍 관점에선 ‘로그인’ 같은 로직  
아이디가 일치하고, 패스워드가 일치하면 회원이라고 판단한다.  

- &&(AND), ||(OR)
A && B -> A 조건도 ‘참(true)’이고 B 조건도 ‘참’인 경우만 ‘참’으로 판단  
만약 앞의 조건이 false일 경우 뒤의 조건은 검사하지 않는다.  

A || B  -> A, B 조건 둘 중 하나라도 ‘참’이면 ‘참’으로 판단.  
만약 앞의 조건이 true인 경우 뒤의 조건은 검사하지 않는다.  

<br>

## 기타 연산자 : 삼항 연산자, 할당 연산자

- 삼항 연산자 : 3가지로 구성되는 연산자 / ‘?’를 이용해서 표현 / if~else 구문을 간단히 사용한 방식
(+ 실제로 코드 작성할 때는 if ~ else를 더 많이 사용한다.)

```
int a = 10;
char c = a == 10? ‘O’:’X’ ;
System.out.println(c);
```

a==10의 연산 결과가 true이면 char c에 O를 담고  
a==10의 연산 결과가 true이면 char c에 X를 담는다.  
(삼항 연산자는 결과 데이터를 변수로 받거나 처리해야 한다)  

![5](https://user-images.githubusercontent.com/101503543/159005238-d635b233-a107-40d5-a17a-d3a40d7a503d.PNG)

- =은 ‘같다’가 아니라, ‘할당(Assign) 연산자’
(Java에서 변수 처리는 데이터를 복사한다는 개념만이 있기 때문에 ‘=‘의 정확한 용도를 알아둬야 한다.)

```
int a = 10 ;  // a 변수 상자에 10이란 데이터를 할당한다.
a = a + 10 ;  // a 변수 상자에서 데이터를 꺼내서 10을 더한 결과를 왼쪽의 a 변수에 새롭게 담는다.
int b = a ; // b라는 변수 상자에 a 상자의 내용물을 복사(Copy)해서 담는다.
```

- 연산자의 응용 : +=, -=
(코드 내에 변수가 여러 번 나오면, 그만큼 메모리상에 상자가 존재했다가 사라져야 하기 때문에 좀 더 간결하게 사용하기 위해 위와 같이 쓰기도 한다.)

```
int a = 10;
a += 100; // ‘a = a + 100’을 줄여서 표현할 때 사용
```

- (응용) 홀짝 프로그램 만들기
- 임의의 숫자 발생하기 : Math.random() 또는 Randon.nextInt()을 이용한다.  

- (예) Random 클래스 이용하기

1. import java.util.Random; // import문으로 random 클래스 가져다 사용하기
2. Random r = new Random() ; // 임의의 숫자 발생기 선언하기.
3. int Value = r.nextInt(100); // nextInt(100)은 0에서 100미만의 임의의 정수를 발생시켜주는 장치
그리고 발생한 정수를 randomValue에 넣어준다.

```
import java.util.Random;

public class OddAndEven {
public static void main(String[] args) {
Random r = new Random();
int value = r.nextInt(100);
int odd = value%2;     // 홀이면 1, 짝이면 0  -> 여기서 제어문을 이용하여 홀짝을 출력해주면 됨
```
<br>

## 16진수와 8진수

(우리에겐 10진수가 익숙하지만, 컴퓨터가 좀더 편하게 사용하는 수 16진수와 8진수도 알아두면 좋다.)

- 16진수와 8진수 표기법
- 숫자의 단위가 8, 16
- 8진수는 0에서 7까지의 값을 사용 / 16진수는 0~9와 A,B,C,D,E,F까지 알파벳 6개 사용하여 표기
- 16진수는 숫자 앞에 ‘0x’를 붙여준다. / 8진수는 숫자 앞에 ‘0’을 붙인다.

```
int a = 0x11;  // 16진수
System.out.println(a) ; //  17 -> 10이 넘으면 16이라는 값이 추가됨. 따라서 a는 16 + 1 = 17의 값을 가짐

int b = 011;  // 8진수
System.out.println(b) ; // 9  -> 8진수는 0에서 7까지의 숫자만을 활용 / / 8+1 = 9의 값을 가짐
```
<br>

## 프로그램에서 쓰이는 특수문자

- 특수문자와 표기법  
- 특수문자는 주로 문자열을 처리할 때 많이 사용.
- 특히 \n, \b, \r 을 주의.
- 이 중 화면에 줄을 바꿀 때엔 주로 \n을 사용.

![6](https://user-images.githubusercontent.com/101503543/159005239-95d22ebe-f028-4a26-90ed-8b2c1a2b1632.PNG)


```
        System.out.println("1 Hello\tWorld");
        System.out.println("2 Hello\nWorld");
        System.out.println("3 Hello\bWorld");
        System.out.println("4 Hello\rWorld");
        System.out.println("5 Hello\'World");
        System.out.println("6 Hello\"World");
        System.out.println("7 Hello\\World");
```

```
1 Hello	World
2 Hello
World
3 HelloWorld
4 Hello
World
5 Hello'World
6 Hello"World
7 Hello\World
```  
-> 각 특수문자는 해당 기능을 했을 때의 처리 결과를 나타낸다.  
1번은 탭을 눌렀을 때의 결과  
2번은 줄 바꿈을 했을 때의 결과   
3번은 백스페이스의 효과를 했을 때의 결과    
4번은 행 바꿈을 했을 때의 효과  
5,6번은 백슬래시를 통해 이스케이프 문자  

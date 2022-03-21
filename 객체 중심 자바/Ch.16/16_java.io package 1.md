# CHAPTER 16. [java.io](http://java.io) 패키지 데이터 읽고 쓰기

### 1. 데이터 입출력 원리 - I/O : 입력(Input) / 출력(Output)

- **Input** : 사용자가 프로그램에 데이터를 전달하는 것  
(예 : 키보드 입력 장비)  
- **Output** : 프로그램이 결과를 내보내는 것.  
(예 : System.out.println()은 화면에 결과를 내보내는 방식)  

- **접두사 IN - READ - 읽기 전용 빨대  
접두어 OUT - WRITE - 쓰기 전용 빨대**

```java
Scanner s = new Scanner(System.**in**);
System.**out**.println();
```

- Java에서 I/O를 흔히 **Stream**으로 부름.  
데이터가 시냇물처럼 이쪽에서 저쪽으로 흐른다는 비유  

- **데이터를 읽는 대상** : 파일 데이터 / 키보드 / 네트워크 / 이미지, 동영상 데이터  
**데이터를 쓰는 대상** : 파일 데이터 / 모니터의 화면 / 네트워크를 통한데이터 전송  

- [System.in](http://System.in) / System.out → 읽고 쓰는 빨대  
Scanner는 빨대를 이용해서 조금 더 쉽게 사용할 수 있는 중간 장치 역할을 하는 객체  

<br>

## 2. [java.io](http://java.io) 패키지의 InputStream, OutputStream  

- InputStream, Reader 클래스 계열 - 읽기 기능  
OutputStream, Writer 클래스 계열 - 쓰는 기능  

| | 읽기 전용 | 쓰기 전용
|---|---|---|
|1byte 단위 처리 | java.io.inputStream | java.io.outputStream
|2byte(char) 단위 처리 | java.io.Reader | java.io.Writer

Reader, Writer는 2byte인 char 단위로 데이터를 주고받아 주로 문자열을 주고받는 프로그래밍에 적합    
InputStream과 OutputStream은 byte 기반의 데이터인 이미지나 데이터를 주고받을 때 많이 사용  
→ 이 중, InputStream, OutputStream이 압도적으로 많이 사용됨.  

- InputStream은 추상 클래스로 선언되어 있고, InputStream을 부모 클래스로 하여 많은 종류의 하위 클래스가 존재한다.  
실제로 데이터를 읽어내는 위치가 다양할 수 있기 때문에, InputStream은 아래와 같은 복잡한 상속 구조로 되어있다.  

<br>

### InputStream을 구하는 2가지 방법

1. **InputStream을 클래스로부터 객체를 생성하는 방식 이용**
2. **객체의 메소드 실행 결과로 InputStream 타입의 객체가 나오는 경우**

→ 상속이나 인터페이스를 쓰면서 가장 좋은 점은 부모 클래스 타입이나 인터페이스의 선언만으로 보이는 모든 메소드를 그대로 사용할 수 있다는 점.  
→ 어떤 방식이든 InputStream을 얻어낼 수 있다면 나머지 프로그래밍은 데이터 원천 상관없이 개발 가능  

- 클래스 이름에 InputStream이 붙으면 무조건 데이터를 읽어내는 기능을 하는 클래스라고 생각하기.  
예) **FileInputStream** : 파일에서 데이터 읽어들이는 기능을 가진 클래스  
**ZipInputStream** : 압축 파일 포맷 zip 파일에서 데이터 읽어들이는 기능을 가진 클래스  
**DataInputStream/BufferedInputStream** : 다양한 스타일의 데이터를 읽어들이는 InputStream  

- 메소드의 리턴 타입으로 InputStream이 나오는 경우  
**네트워크 연결**을 할 때 **Socket**을 이용하면서 가장 많음  

<br>

### InputStream에서 반드시 기억해야 하는 메소드 read() : 한 바이트의 데이터를 읽는다.

- **InputStream을 이용하는 코드 작성 순서**
1. 원하는 대상에서 데이터를 읽어낼 수 있는 InputStream 계열의 객체를 구한다.  
2. read() 메소드를 이용해서 데이터를 읽어낸다.  

- **InputStream와 read() 메소드 입력 과정**
1. 원하는 대상에서 데이터를 읽어내기 위해서 빨대(파이프)를 연결하는 것처럼 InputStream을 연결.  
2. 메소드 read()를 이용하여 얻어진 InputStream(파이프)를 통해 데이터를 읽어들임.  
예) read( ) 메소드 호출 10번 = 10개의 바이트 데이터를 읽어들임.  
3. 그 결과는 int 타입으로 반환된다. **(이때, int 결과는 숫자가 아니라 한 바이트의 데이터 값으로 생각해야 한다)**  
4. 더 이상 읽어들일 데이터가 없는 경우 음수가 나온다.  

- **InputStream의 read() 메소드는 추상 메소드로 정의되어 있다.**
```java
public abstract int read() throws IOException
```

어떤 종류의 InputStream을 얻든, 우리가 알아야 하는 메소드는 read() 메소드만 보이게 되어 있다.  
사용자 입장에서도 편리하고, InputStream을 상속하는 클래스를 새로 작성해도 read() 메소드는 반드시 구현된다.  
따라서, **‘읽어들이는 대상’**에 맞춰서 구현하는 방식을 지원하기 위해 추상 메소드 형태로 제공된다.  

- **read() 메소드를 호출하면 내부적으로 위치가 조금씩 변경**되고(내부적인 커서 cursor 이동), 때문에 다음 데이터를 읽어들이는 구조가 됨.  
InputStream의 메소드 중 reset(), mark()와 같은 메소드는 이런 커서의 위치를 조절하고 싶은 경우에 사용  

- **read(byte[ ]) 메소드는 한 번에 byte[ ]만큼씩 데이터를 읽어 낸다.**  
	- InputStream의 read( ) 메소드는 read(byte[ ])의 형태로도 제공됨.  
	- 이 메소드 역시 int 값을 반환하지만, **이 int 값은 byte[ ]로 새로이 읽혀 들어간 데이터의 바이트 수를 의미한다.**  
	- 메소드가 실행될 때 데이터를 실제로 담기 위해서 사용되는 것은 파라미터로 추가된 byte[]이다. 
	- 즉, 데이터가 한 번에 byte[]만큼 담기는 방식이다. 즉, read()가 데이터 하나씩 옮기는 방식이라면, read(byte[])는 byte[] 자체가 데이터를 임시로 담는 공간이다. 이런 공간을 buffer라는 용어로 부른다.
	- **예)** 한 번에 4byte를 읽어내는 보관 장치(buffer)라면, 한 번에 1바이트 읽는 read()보다 속도가 빨라질 것.
<br>

<details>
	<summary><strong>버퍼에 대한 추가 조사</strong></summary>
<div markdown="1">
<br>
	
> '버퍼'는 데이터를 한 곳에서 다른 한 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 메모리의 영역.  
> 버퍼링(buffering)이란 버퍼를 활용하는 방식 또는 버퍼를 채우는 동작을 말한다.
> 다른 말로 '큐(Queue)'라고 표현한다.  
> 버퍼는 컴퓨터 안의 프로세스 사이에서 데이터를 이동시킬 때 사용된다. 보통 데이터는 키보드와 같은 입력 장치로부터 받거나 프린터와 같은 출력 장치로 내보낼 때 버퍼 안에 저장된다. 이는 전자 통신의 버퍼와 비유할 수 있다. 버퍼는 하드웨어나 소프트웨어에 추가될 수 있지만 버퍼는 상당수가 소프트웨어에 추가된다. 버퍼는 보통 속도가 계속 바뀔 수 있으므로 데이터 수신, 처리 속도에 차이가 있다. (예: 프린터 스풀러)  
> 버퍼는 네트워크 상에서 자료를 주고 받을 때나 스피커에 소리를 재생할 때, 또는 디스크 드라이브와 같은 하드웨어의 입출력을 결합하는 데에 자주 이용된다. 버퍼는 또한 순서대로 데이터를 출력하는 FIFO 방식에서 보통 사용된다.  
> (출처 : 위키백과)

</div>
</details>

<br>

- **FileInputStream - 파일에서 데이터를 읽어내는 기능의 클래스**

```java
InputStream in = new FileInputStream(”C:\\zzz\\aaa.txt”); 
// Checked Exception 오류 발생
// 컴파일러가 반드시 예외 처리를 해야만 객체를 생성할 수 있게 허락하므로
// try ~ catch 나 throw ~ 를 이용하여 예외 처리해야 함.
```

```java
public static void main(String[] args)throws Exception { InputStream in = new FileInputStream("C:\\zzz\\aaa.txt");
```
+) Java에서는 특수문자를 사용할 때 이스케이프 문자 '\'를 이용하므로, 역슬래시 입력할 때는 '\\'으로 표현한다.  


- **while 구문 - 파일의 크기를 알 수 없으므로 while(true) 이용하여 데이터 읽기**
```java
public static void main(String[] args)throws Exception {
		InputStream in = 
							new FileInputStream("C:\\zzz\\aaa.txt"); 

  while(true){ 
		//한바이트를 읽어들인 결과 
		int data = in.read(); 
		System.out.println(data); 
		if(data == -1){break;}
		// 끝까지 읽어서 더 나올 데이터가 없으면 -1이 출력됨
```

<br>

### OutputStream : 바이트의 데이터를 기록할 수 있다.

- **OutputStream 구하는 방식 크게 2가지**  
1. 어떤 클래스의 형태로 제공되는 경우  
2. 어떤 클래스의 어떤 메소드의 실행결과로 OutputStream 계열을 반환해주는 경우  

- OutputStream의 write 메소드 - 3가지
> 1. write(int)
> 2. write(byte[])
> 3. write(byte[], int, int)

- **1) write(int) : 한 바이트에 해당하는 데이터를 기록할 때 사용**  

```java
public abstract void write(int b) throws IOException
```

write(int) 메소드는 추상 메소드  
InputStream의 read()와 마찬가지로 실제로 ‘**데이터를 기록하는 방법은 연결된 대상이 파일이나 네트워크냐’에 따라서 다르게 동작해야 하기 때문에 추상 메소드의 형태로만 제공**  

- **2) write(byte[ ])은 byte안에 있는 데이터를 한 번에 기록해준다.**  
write(int) 방식은 파라미터로 들어오는 한 바이트에 해당하는 데이터만을 넣어준다.    
write(byte[ ])은 파라미터로 입력된 데이터를 한 번에 원하는 대상으로 데이터를 출력하는 기능  
따라서 원하는 데이터를 **바이트의 배열**로 만든 후, OutputStream을 통해서 출력하면 그 데이터는 **OutputStream이 연결된 대상**으로 기록됨.  

- **3) write(byte[ ], int , int)**는 **byte[ ]**  -> 제일 많이 씀
데이터를 원하는 위치에서부터 원하는 숫자만큼 기록해 준다.    
첫 번째 int 파라미터 - byte안에서의 기록 시작 위치.   
두 번째 int 파라미터 - 기록을 원하는 데이터의 수.  

- **flush( ) - 스트림에 기록된 데이터를 확실히 보낼 수 있다.**  
flush - ‘물을 내리다’ / 확실하게, 강제로 보낼 때 사용  

<br>

### FileOutputStream 이용하여 파일에 원하는 데이터 기록하기  
- FileOutputStream은 객체를 만들기 위해서 파일명을 지정해주면, 파일이 없는 경우에는 **자동으로 파일을 만들고, 파일이 있는 경우에는 기존의 파일을 덮어쓰게 된다.**  (따라서 파일의 존재 여부는 신경쓰지 않아도 됨)
- **주의할 점**  
FileInputStream이나 FileOutputStream 모두 외부와 통신을 하는 방식이기 때문에 이와 관련된 **예외**를 명시적으로 처리해줘야 한다.  

## 문자열은 byte[ ]로 변경 가능 - 'getBytes( )' 메소드 이용  
```
String str = "한글";
byte[] arr = str.getBytes();
System.out.println(Arrays.toString(arr));
// 결과 : -57, -47, -79, -37
```
문자열은 위의 예처럼 손쉽게 byte[]로 전환할 수 있기 때문에 OutputStream의 write(byte[]) 기능을 이용해 주면 쉽게 파일 데이터를 기록해줄 수 있다.  
(+ 참고 : '한글' 문자열은 4byte로 변환되며, byte[]로 변경된 데이터는 각 바이트가 -128에서 127까지의 범위 내의 숫자로 표현된다.)
<br>

- OutputStream의 write(byte[]) 이용해서 파일에 문자열 기록하기
```
public static void main(String[] args) throws Exception{	// OutputStream은 예외 처리!
	OutputStream out = new FileOutputStream("aaa.txt");
	String str = "이 문자열을 파일에 기록";
	byte[] arr = str.getBytes();		// getBytes로 byte[] 배열로 변경
	out.write(arr);				// write(byte[]) 메소드를 통해 바이트 안에 있는 문자열 데이터 한번에 기록
```
<br>

## 입출력 프로그래밍에서 사용한 파이프는 반드시 close( )해야 한다.  
- **InputStream, OutputStream** 같은 데이터의 연결 파이프(Stream)은 사용 후 반드시 **close()를 통해 연결 종료**를 시켜줘야 함. 
입출력 프로그래밍은 기본적으로 외부와의 통신이 주를 이룬다. (파일에서 데이터를 읽거나 네트워크 사용 등과 같이 외부와 JVM 간의 통신)  
close() 메소드를 해주지 않는 이상, 데이터를 출력해줘도 아직 JVM은 파일과의 연결을 종료한 상태가 아니기 때문에 여러 문제점이 발생하거나 심각한 메모리 낭비를 초래한다.  
이를 막고자 모든 외부 연결을 맺는 코드에는 공통적으로 close()라는 메소드를 써준다.  

- **close()는 반드시 finally에서 처리한다.**
Exception이 발생하면 나머지 코드가 실행되지 않기 때문에 마지막에 작성된 close()라는 메소드는 실행되지 않음.  
따라서 close()는 예외와 관계없이 처리되어야만 한다.  


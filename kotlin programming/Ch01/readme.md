## 1. 코틀린 시작
> 변수 선언(var,val)  

&nbsp; var은 언제든지 읽기,쓰기가 가능하여 가변적이고 val은 선언시에만 초기화가 가능하며 중간에는 값을 변경할 수 없다.
</br></br>


> null 값  

&nbsp;코틀린은 기본 변수에서 null을 허용하지 않는다. 변수에서 값을 할당하지 않으면 문법 에러를 표시하고 컴파일을 막아준다.(nullPointexcecption)에러를 사전에 방지한다.
```java
    var a: Int =1  // 1과 같이 값을 할당해줘야 함(null x)
    print(a)
```
```java
    var a:Int? = null // null을 사용하고 싶으면  nullAble 형태로 변경 가능
```
</br></br>

> 기본 자료형( 자바와 거의 동일)

```java
    var intValue:Int = 123
    var LongValue:Long = 123L
    var intValueByHex:Int = 0x1af //16진수
    var intValueByBin:Int = 0b1011010 //2진수
    //8진수는 표기하지 않음!!
 
    var doubleValue:Double = 123.4  //double 형
    var doubleValueWithExp:Double = 123.4e10
    var floatValue:Float = 123.5f //float형
```
</br></br>

> 문자형(char) & *boolean* 값

&nbsp;코틀린은 UTF-16BE로 관리하여 글자 하나가 2bytes의 메모리 공간을 사용한다.
```java
    var charValue:Char ='a'
    var koreanCharValue:Char='가'
    var booleanValue:Boolean =true; // boolean 값
```
</br></br>

> 문자열(string)

&nbsp;줄바꿈이나 특수문자의 경우 ""개수 추가
```java
    var stringValue =" seungwon kotlin study "
    var multiLineStringValue =""" Seungwon
    kotlin
    study"""

```

</br></br></br>

> 형 변환(type casting)

&nbsp;하나의 변수에 지정된 자료형을 호환되는 다른 자료형으로 변경하느 기능이다.
코틀린에서는 단순한 변환 값 입력이 아니라 **형 변환 함수**를 이용해야 한다.
```java
    fun main(){
        var a:Int =123
        var b:Long =a.toLong() //명시적 형변환
    }
```
&nbsp;코틀린은 형 변환시 오류를 막기 위해 암시적 형변환을 사용하지 않는다.  

**명시적 형변환**이란 변환될 자료형을 직접 지정하는 것이다.  
**암시적 형변환**은 변수를 할당할 시 자동으로 형변환이 이루어 지는 것을 말한다.
</br></br>

> 배열(array)

&nbsp;배열을 사용할 변수를 만들고 *arrayOf*함수를 통해 배열에 저장할 값을 나열한다. 
```java
    fun main(){
        var arr = arrayOf(1,2,3,4,5) // arrayOf 함수 사용하여 값 저장
        var nullArr = arrayOfNulls<Int>(5) // 특정 크기의 빈 배열
        arr[1]=4 // 값 할당
        print(arr[2]) // 값 사용
    }
```
&nbsp;배열의 단점: 전체크기를 변경할 수 없다.  
&nbsp;배열의 장점 : 다른 자료구조보다 빠른 입출력이 가능하다.

</br></br>

> 타입추론(type inference)

&nbsp;변수나 함수들을 선언할 때, 혹은 연산이 이루어 질 때 자료형을 코드에 명시하지 않아도 자동으로 자료형을 추론해주는 기능

```java
    fun main(){
        var a = 123     //int
        var b = 123L    //long
        var e = 0xABC    //int
        var f = 0b101010    //int

        var c = 12.34   //double
        var d = 12.34f  //float
 
        var g = true    //boolean
        var h = 'char'  //char
    }
```

> 함수(function)

&nbsp;원하는 결과값을 연산하는데 사용한다. 
```java
    fun main(){
        print(add(1,2,3))
    }
    fun add(a: Int, b:Int, c:Int):Int // 마지막은 반환 값 타입지정
    {
        return a+b+c; //값 반환 후 함수 종료
    }
```
&nbsp;add함수와 같이 간단한 함수를 단일 표현식 함수(single-expression function)으로 나타낼 수 있다.
```java
    fun add(a: Int,b: Int,c: Int) = a+b+c;
    //단일 추론에서는 반환형의 타입을 생략할 수 있다!!
```
</br></br>

> 다중 조건문(when)

&nbsp;하나의 변수를 여러개의 값과 비교할 수 있다. (Switch문을 대체하여 사용 가능)
```java
    fun main(){

        doWhen(1)
        doWhen("SeungWon")
        doWhen(10L)
        doWhen(3.14)
        doWhen("Kotlin")

    }
    fun doWhen(a:Any) // Any: 어떤 자료형이든 상관없이 호환되는 최상위 자료형
    {
        when(a){
            1->println("1입니다");
            "SeungWon"->println("승원아 안녕");
            is Long -> println("Long 타입입니다")
            !is String -> println("String 타입이 아닙니다")
            else ->println("어떤 조건도 만족하지 않음");
        }
    }
```
결과 값:  
1입니다  
승원아 안녕  
Long 타입입니다  
String 타입이 아닙니다  
어떤 조건도 만족하지 않음  
</br></br>

&nbsp;혹은 코드의 결과 값을 이용해 값을 얻을 수도 있다. 
```java
    fun doWhen(a:Any){
        var result = when(a){
            1->"1입니다"
            str->"String 입니다"
        }
        println(result)
    }
```
결과 값:  
1입니다  
String 입니다  

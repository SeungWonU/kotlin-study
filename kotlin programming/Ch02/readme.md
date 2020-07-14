## 2. 클래스  

> 클래스  

&nbsp;클래스는 고유의 값을 가진 **속성**과 기능을 구현한 **함수**로 이루어져 있다.또한 **인스턴스**를 만드는 틀이라는 존재이다. **인스턴스**란 클래스를 이용해서 만들어 내는 서로 다른 속성의 객체를 지칭하는 용어이다.  

```java
    fun main(){
        var a = Person("Person1",2000)
        var b = Person("Person2",2001)
        var c = Person("Person3",2002)
        // Peson의 인스턴스 생성

        a.intro()   b.intro()   c.intro()
        // intro함수를 참조하여 호출
    }

    class Peson(var name:String,val birth:Int) //속성을 괄호안에 정의
    {
        fun intro(){
        println("안녕하세요, ${birth}년생 ${name}이라고 합니다.")
        }   
    }  
```  
</br></br>

> 기본 생성자  

&nbsp;새로운 인스턴스를 만들기 위해 호출하는 특수한 함수이며 인스턴스의 속성을 초기화 할 수 있다.
```java
    fun(){
        var a = Person("Person1",2000)
        var b = Person("Person2",2001)
        var c = Person("Person3",2002)
    }
    class Person(var name:String, val birth:Int){
        init{ // init은 생성자를 통해 인스턴스가 만들어질 때 호출된다.

            println("${this.birth}년생 ${this.name}입니다.")
            // this는 인스턴스 자신의 속성이나 함수를 호출하기 위해 클래스 내부에서 사용되는 키워드이다.

        }
    }
```
</br></br>

> 보조 새성자  
 
&nbsp;인스턴스 생성시 편의를 제공하거나 추가적인 구문을 수행하는 기능이다.  
```java
    fun(){
        var a = Person("Person1",2000)
        var b = Person("Person2",2001)
        var c = Person("Person3",2002)

        var d = Person("Person4") //init과 constructor 둘다 수행
    }
    class Person(var name:String, val birth:Int){
        init{
            println("${this.birth}년생 ${this.name}입니다.")
        }
        constructor(name:String):this(name,1999)
        // constructor:this(필요한 파러미터)
    }
```
</br></br></br>

> 상속

&nbsp;존재하는 클래스를 확장하여 새로운 속성이나 함수를 추가한 클래스를 만들 때,여러 개의 클래스를 공통으로 뽑아 관리할 때 상속을 사용한다.  
코틀린에서는 클래스가 일반적으로 상속받기 힘들기 때문에 *open*이라는 키워드를 붙여준다.
```java
    fun main(){
        var a = Animal("별",3,"강아지")
        var b = Dog("별",3)
        a.intro()   b.intro()
        //같게 나옴

        b.bark() //멍멍
        
    }
    class Animal(var name:String,var age:Int,var type:String){
        fun intro(){
            println("나는 ${type} ${name}이며 나이는 ${age}이다")
        }       
    }
    class Dog(name:String, age:Int) : Animal(name,age,"강아지")
    {
        fun bark(){
            println("멍멍!")
        }
    }

```

</br></br></br>

> 오버라이딩(Overriding) 11장

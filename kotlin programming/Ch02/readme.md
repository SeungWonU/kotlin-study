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

> 오버라이딩(Overriding)

&nbsp;서브클래스에서 수퍼클래스에 있는 함수를 같은 이름과 형태로 다시 구현할 수 있는 것을 오버라이딩이라고 한다. 이미 구현이 끝난 함수를 서브클래스에서 변경해야 할 때 사용된다.
```java
    fun main(){
        var d = Dog() // 인스턴스 생성
        d.eat() // 고기를 먹다
    }
    open class Animal{
        open fun eat(){ // open을 통해 override 할 수 있게 함
            println("음식을 먹다")
        }
    }
    class Tiger : Animal{
        override fun eat(){   // override 함수 를 통해 재정의 가능
            println("고기를 먹다")
        }
    }
``` 
</br></br></br>

> 추상화(abstraction)

&nbsp;선언부만 있고 기능이 구현되지 않은 추상함수 & 추상클래스로 구성된다. 보통 형식만 선언하고 실제 구현은 서브클래스에 일임할 때 사용한다.
```java
    fun main(){
        r.eat()    // 당근을 먹다
        r.sniff()  // 컹컹
    }
    abstract class Animal{ //추상 클래스  >> 반드시 서브 클래스에서 상속받음 
        abstract fun eat()   // 추상 함수의 내용은 적지 않음
        fun sniff(){
            println("컹컹")
        }
    }
    class Rabbit : Animal(){
        override fun eat(){
            println("당근을 먹다")
        }
    }
 
```
</br></br></br>

> 인터페이스(interface)

&nbsp;추상함수로만 이루어져 있는 순수 추상화 기능이다. 추상함수는 생성자를 가질 수 있는 반면, 인터페이스는 생성자를 가질 수 없다. 또한 구현부가 있는 함수는 open함수, 구현부가 없는 함수는 abstrcat함수로 정의된다.  
한번에 여러 인터페이스를 상속받을 수 있으므로 편리하다.
```java
    fun main(){
        var d = Dog()
        d.run()  // 뛰어갑니다
        d.eat()  // 고기를 먹다
    }
    interface Runner{
        fun run() // 구현부가 없는 함수 (abstract)
    }
    interface Eater{
        fun eat(){ // 구현부가 있는 함수 (open)
            println("음식을 먹다")
        }
    class Dog : Runner,Eater{
        override fun run(){  //abstract의 내용 재정의
            println("뛰어갑니다")
        }
        override fun eat(){  //open의 내용 재정의
            println("고기를 먹다")
        }
    }
    }
```  

> 접근제한자

&nbsp; 총 4가지 접근 제한자가 있다. (public , internal , private , protected) 변수, 함수, 클래스 선언 시 앞에 붙여 사용한다.
```java
    // package scope
    public // 어떤 패키지에서도 접근 가능
    internal // 같은 모듈 내에서만 접근 가능
    private // 같은 파일 내에서만 접근 가능

```
```java
    // class scope
    public // 클래스 외부에서도 접근 가능
    private // 클래스 내부에서만 접근 가능
    protected // 클래스 자신과 상속받은 클래스에서 접근 가능
```

> 고차함수

&nbsp;함수를 클래스에서 만들어낸 인스턴스처럼 취급하는 방법이다.패러미터로 넘겨줄 수도 있고 결과값으로 반환받을 수도 있다.

```java
    fun main(){
        b(::a) //고차함수
        //b가 호출하는 함수 a
    }
    fun a(str : String){
        println("$str 함수 a")
    }
    fun b(function : (String)->Unit){// 반환값이 없는 String
        function("b가 호출하는")
    }
```
</br></br>

> 람다함수

&nbsp;함수를 람다식으로 표현한다. 일반함수와 달리 고차함수이기 때문에 별도의 연산자 없이 변수에 넣을 수도 있다.
```java
    fun main(){
        val c : (String)->Unit = { str -> println("$str 람다함수")}
        // 람다함수
    }
       fun b(function : (String)->Unit){// 반환값이 없는 String
        function("b가 호출하는")
    }fun 
```

</br></br></br>

> 특별한 람다함수

&nbsp;1. 람다함수도 여러 구문의 사용이 가능하다
```java
    fun main(){
        val c : (String) -> Unit = {str -> println("$str 람다함수를")
        println(" 여러 구문으로")
        println(" 사용이 가능하다.")
        }
    
        val calculate : (Int,Int)->Int = {a,b-> println(a) println(b) a+b} // a+b의 값을 Int로 반환한다

    }
```
</br>

&nbsp;2. 패러미터가 없는 구문들은 실행할 구문들만 나열하면 된다
```java
    fun main(){
        val a () -> Unit ={ println( "패러미터가 없다")}
    }
```
</br>

&nbsp;3. 패러미터가 하나이면 it 사용
```java
    val c:(String) -> Unit = {println("$it 람다함수")}
```

</br></br></br>

> 스코프 함수 (scope function)

&nbsp;함수형 언어의 특징을 더 편리하게 사용하기 위해 기본으로 제공하는 함수이다. 클래스에서 생성한 인스턴스를 scope함수에 전달하면 인스턴스의 속성이나 함수를 scope함수에서 사용할 수 있다.  

scope 함수의 종류에는 **apply run with also let**가 있다

```java
    fun main(){
        //apply를 이용한 scope함수
       var a = Book("코틀린 수업",30000).apply{
           name = "[apply]" + name
           discount()
        }
        
       //run을 이용한 scope함수 (값이 나와야 함)
       a.run{ 
           println("책이름 :${name}, 가격 : ${price}원")
       }     

       //with와 run 은 같다
       with(a){
           println("책이름 :${name}, 가격 : ${price}원")
       } 

        var price = 5000
       //also는 apply와 비슷하지만 위의 price가 main에서도 정의 되었기 때문에 혼란방지
        var b = Book("코틀린 수업2",20000).also{
           it.name = "[apply]" + it.name  //it.속성값
           discount()
        }
       
       //let은 run과 비슷하지만 위의 price가 main에서도 정의 되었기 때문에 혼란방지
       a.let{
           println("책이름 :${it.name}, 가격 :${it.price}원")
           //it.속성값으로 나타내야 한다.
       }
       
    }
    class Book(var name : String, var price :Int){
        fun discount(){
            price -= 2000
        }
    }
```

</br></br></br>

> object

&nbsp;단 하나의 객체만으로도 생성자 없이 객체를 만든다. 
```java
    fun main(){
        println(Counter.count) //0

        Count.countUp()
        Count.countUp()

        println(Counter.count) //2

        Count.clear()

        println(Counter.count) //1

    }

    object Counter{ //생성자 x
        var count =0;
        fun countUp(0{
            count++
        })
        fun clear(){
            count--
        }
    }
```
</br></br></br>

> companion object

&nbsp;클래스의 인스턴스 기능을 그대로 사용하면서 인스턴스간에 공용으로 사용할 속성과 함수를 별도로 만드는 기능이다. (Static멤버와 비슷)

```java
    fun main(){
        var a = FoodPoll("비냉")
        var b = FoodPoll("물냉")

        a.vote() 
        a.vote()

        b.vote()
        b.vote()
        b.vote()

        println("${a.count}")2
        println("${b.count}")3
        println("총계 : ${FoodPoll.total}")5

    }
    class FoodPoll (val name : String){
        companion object{  //공유됨 a,b
            var total = 0
        }
        var count =0

        fun vote(){
            total++
            count++
        }
    }
```
</br></br></br>

> 옵저버(observer)

&nbsp;이벤트가 일어나는 것을 감시하는 역할을 한다. 이벤트가 발생할 때마다 즉각적으로 처리할 수 있는 프로그래밍 패턴을 옵저버 패턴이라고 한다. 두 클래스 사이에 인터페이스를 만들어 이벤트를 처리하는데 이를 옵저버라고 한다.

```java
    fun main(){ 
        EventPrinter().start() // 5->10->15->20 ...
    }
    interface EventListener{ // 두 클래스의 인터페이스 역할
        fun onEvent(Count : Int)
    }
    class Counter(var Listener : EventListener){
        fun count(){
            for(i in 1..100)
                if(i % 5 == 0 )listner.onEvent(i) //5의 배수일 때 count
        }
    }
    class EventPrinter EventListener{  //상속
        //화면에 출력
        override fun onEvent(count: Int){
            println("${count}->")
        }
        fun start(){
            val counter = Counter(this) //EventPrinter객체 this 
            counter.count()
        }
    }
```

</br></br></br>

> 익명객체

&nbsp;EventLister를 상속받아 구현하지 않고 임시로 만든 객체를 넘겨주는 익명 객체라고 한다. 

```java
    fun main(){ 
        EventPrinter().start() // 5->10->15->20 ...
    }
    interface EventListener{ // 두 클래스의 인터페이스 역할
        fun onEvent(Count : Int)
    }
    class Counter(var Listener : EventListener){
        fun count(){
            for(i in 1..100)
                if(i % 5 == 0 )listner.onEvent(i) //5의 배수일 때 count
        }
    }
    class EventPrinter {
        fun start(){
            // 이 함수에서만 상속받았음으로 클래스 전체에 해당되지않음
            // object를 사용해 코드 중간에 즉시 생성하여 사용할 수 있다.
            val counter = Counter(object :EventListener{
                override fun onEvent(count : Int){
                    println("${count}->")
                }
            })
            counter.count()
        }
    
    }
```
</br></br></br>

> 다형성

&nbsp; 클래스의 상속관계에서 오는 인스턴스의 호환성을 활용할 수 있는 기능으로 수퍼클래스가 같은 인스턴스를 한번에 관리하거나 인터페이스를 구현하여 사용되는 코드에서도 이용된다.  

음료로 빗대어 살펴보면 콜라라는 것이 단지 콜라일 뿐 아니라 음료라고도 볼 수 있다는 점을 다형성이라고 말한다. 콜라 인스턴스를 음료 변수에 담는 행위를 상위 자료형인 수퍼클래스로 변환한다는 말로 up-casting라고 한다. 이는 별도의 과정이 필요없지만 다시 하위 자료형으로 변환하는 과정 down-casting은 별도의 연산자가 필요하다.이는 as와 is인데  그 내용은 아래에서 살펴보겠다.
```java
    fun main(){
        var a = Drink()
        a.drink() // 음료를 마신다

        var b : Drink = Cola() // up-casting
        b.drink() // 음료중에 콜라를 마십니다
        //b.washDishes // 에러!! down-casting해야됨

        if(b is Cola)
        {
            b.washDishes() // 조건문안에서만 down-casting됨 
            //콜라를 다시사온다
        }

        var c = b as Cola
        c.washDishes() // as로 down-casting
        b.washDishes() // as를 사용하면 반환값 뿐아니라 변수 자체도 됨

    }
    open class Drink{
        var name ="음료"

        open fun drink(){
            println("${name}를 마신다")
        }
    }
    class Cola : Drink(){
        var type = "콜라"
        
        override fun drink(){ // Drink함수의 오버라이드
            println("${name}중에 ${type}을 마신다")
        }
        fun washDishes(){
            println("${type}를 다시 사온다")
        }
    }
```
</br></br></br>

> 제너릭(Generic)


&nbsp;함수나 클래스를 선언할 때 고정적인 자료형 대신 실제 자료형으로 대체되는 타입 패러미터를 받아 사용하는 방법이다. 따라서 캐스팅 연산없이도 자료형을 사용할 수 있다. Type패러미터의 이름은 일반적으로 T,U,V순으로 사용한다.
```java
    fun main(){
        UsingGeneric(A()).doShouting()
        UsingGeneric(B()).doShouting()
        UsingGeneric(C()).doShouting()
        
        doShouting(B())
    }

    //제너릭 함수로 사용하는 방법
    fun <T : A> doShouting( t: T){
        t.shout()
    }
    open class A{
        open fun shout(){
            println("A가 소리친다")
        }
    class B : A(){
        override fun shout(){
            println("B가 소리친다")
        }
    class C : A(){
        override fun shout(){
            println("C가 소리친다")
        }
    
    class UsingGeneric<T: A>( val t : T){
      fun doShouting(){
          t.shout()
      }  
    }
    }
    }
    }
```
</br></br></br>

> 리스트(List)

&nbsp;데이터를 코드에서 지정한 순서대로 저장하는 것을 리스트라고 한다. List는 데이터를 모아 관리하는 Collection Class 중 가장 단순한 형태로 여러개의 데이터를 원하는 형태로 넣어 관리하는 것이다. 두 가지 종류가 있는데 List와 MutableList가 있다. Mutable은 대체,추가,삭제가 가능하다.  

```java
    fun main(){
        val a = listOf("사과","딸기","포도")
        println(a[1]) //배열과 사용이 같음

    for(fruit in a){
        print("${fruit}:") // 사과: 딸기 :포도:
    }
    
    var b = mutableListOf(1,2,3,4) //변경 가능한 리스트
    println(b) //1,2,3,4

    b.add(5)
    println(b) //1,2,3,4,5

    b.add(2,8)
    println(b) //1,2,8,3,4,5

    b.shuffle()
    println(b) // random

    b.sort()
    println(b) // 1,2,3,4,5,8
    }
```

</br></br></br>

> 문자열

&nbsp; 입력값을 받거나 문자열로 된 자료를 처리할 때 사용되는 기능들을 소개하겠다.

```java
    fun main(){
        val test1 = "Test.SeungWon.Kotlin"

        pirntln(test1.length) //test1의 길이

        println(test1.toLowerCase()) // 전부 소문자로
        println(test1.toUppercase()) // 전부 대문자로
        
        val test2 = test1.split(".")
        println(test2)  // .을 기준으로 나눈다
        
        println(test2.joinToString()) // 이어붙인다
        println(test2.joinToString("&")) // &를 포함시켜 이어붙임

        println(test1.substring(5..10)) // 5~10인덱스의 test1값

        println(test1.startWith(Test)) //true
        println(test1.endsWith(Kotlin)) //true
        println(test1.contains("Seung")) //true
    }
```

```java
    //boolean값으로 반환받는 함수들
    fun main(){
        val nullStr : String? =null
        val emptyStr = ""
        val blankStr = " "
        val normalStr=  "normal"

        println(nullStr.isNullOrEmpty()) // true
        println(emptyStr.isNullOrEmpty()) // true
        println(blankStr.isNullOrEmpty())  // false
        println(normalStr.isNullOrEmpty()) // false
    
    
        println(nullStr.isNullOrBlank()) // true
        println(emptyStr.isNullOrBlank()) //true
        println(blankStr.isNullOrBlank()) //true
        //blank는  space , Tab, Line Feed, Carrige return 가능
        println(normalStr.isNullOrBlank()) //false 
    }
```
</br></br></br>

> Null

&nbsp;코틀린에서 nullable을 이용해 null을 사용하려면 if(!null)의 여부를 체크해야 하는데 이를 간단히 해결하기 위한 방법이 있다. *?.  ?:  !!.*이 있다.
아래의 예제를 통해 살펴보겠다.
```java
    var a String? =null
    //null이라면 .뒤에오는 객체를 실행하지 않음
    println(a?.toUpperCase())

    //null이면 "default"이 실행됨
    println(a?: "default".toUpperCase())
    
    //null 여부를 컴파일시 확인하지 않아서 null pointer execption을 유발함
    println(a!!.toUpperCase())

    //null safe연산자는 scope함수를 사용하면 더 좋다
    a?.run{
        println(toUpperCase())
        println(toUpperCase())
    }

```
</br></br></br>

> 변수의 동일성

&nbsp;내용의 동일성 : 메모리상에 서로 다른 곳에 할당된 객체여도 내용이 같으면 동일하다고 판단함(a==b)  

&nbsp;객체의 동일성 : 서로 다른 변수가 메모리상에 같은 객체를 가르킬때이다(a===b)  

내용의 동일성은 Any라는 최상위 클래스에 equals()함수가 반환하는 boolean값으로 판단하게 된다

```java
    fun main(){
        var a = Prodcut("사과",3000)
        var b = Prodcut("사과",3000)
        var c = a
        var d = Prodcut("포도",1000)

        //내용의 동일성
        println(a==b) //true 
        println(a===b) //false

        //객체의 동일성
        println(a==c) //true
        println(a===c) //true

        println(a==d) //false
        println(a===d) //false
    }
    class Product(val name : String, val price : Int){
        override fun equals(other : Any?): Boolean{
            if(other is Product){//내용의 동일성 판단
                return other.name == name && other.price == price
            }else{
                return false
            }
        }
    }

```
</br></br></br>

> 오버로딩

&nbsp;이름이 같더라도 패러미터의 자료형이 다르거나 개수가 다르다면 서로다른 함수로 동작이 가능하다.

```java
    fun main(){
        read(1) 
        read("안녕하세요")
    }
    fun read(x: Int){
        println("$x입니다")
    }
    fun read(x:String){
        println(x)
    }
```
</br></br></br>

> default arguments

&nbsp;패러미터를 받아야 하는 함수이지만 별다른 패러미터가 없더라도 기본값으로 동작해야 할때 사용한다
```java
    fun main(){
        deliveryItem("컵라면") //입력하지 않은 값은 default값으로 자동입력
        deliveryItem("우유",3)
        deliveryItem("주스",10,"직장"))
    }
    
    fun deliveryItem(name : String, count :Int =1, destination : String ="우리집"){
        println("${name}, ${count}개를 ${destination}에 배달한다")
    }
```
</br></br>

> named arguments

&nbsp;패러미터의 순서와 관계없이 이름을 사용하여 직접 패러미터 값을 할당하는 기능이다

```java
    fun main(){
        // 맨 앞의 name은 선물이 입력되고 destination은 해당 패러미터로 할당된다
        deliveryItem("선물",destination="학교")
         }
    
    fun deliveryItem(name : String, count :Int =1, destination : String ="우리집"){
        println("${name}, ${count}개를 ${destination}에 배달한다")
    }
```
</br></br>

>vararg(variable number of arguments)

&nbsp;개수가 지정되지 않은 패러미터이다. 다른 패러미터와 같이 쓸때에는 맨 마지막에 위치해야 한다.

```java
    fun main(){
        sum(1,2,3,4) //10
    }

    fun sum(vararg numbers : Int){
        var sum =0
        
        for(n in numbers){
            sum += n
        }
        print(sum)
    }
```
</br></br>

> infix function

&nbsp;연산자처럼 사용할 수 있다. 구현 방법만 알고 있으면 된다.
```java
    fun main(){
        println(3 multiply 5) //3 이 this를 가르킨다.
        println(3.multiply(4))
    }
    //infix함수는 클래스 이름을 쓰지 않는다.
    infix fun Int.multiply( x: Int) : Int = this* x
```
</br></br></br>

> 중첩 클래스 & 내부 클래스

&nbsp;클래스안에 클래스를 넣는 중첩클래스(Nested class)가 있다. 이는 하나의 클래스가 다른 클래스의 기능과 강하게 연관되어 있다는 것을 말한다.  
&nbsp;중첩클래스에 inner라는 키워드를 붙인 내부클래스(Inner class)가 있다. 이는 외부 클래스와 공유가 가능하다.

```java
    fun main(){
        Outer.Nested().introduce() // Nested Class

        val outer = Outer() 
        val inner = outer.Inner()

        inner.introduceInner() // Inner Class
        inner.introduceOuter() // Outer Class 

        outer.text = "Changed Outer Class"
        inner.introduceOuter() // Changed Outer Class
    }
    
    class Outer{ // 외부 클래스
        var text = "Outer Class"
        
        class Nested{ // 중첩 클래스
            fun introduce(){
                println("Nested Class")
            }
        }

        inner class Inner{ // 내부 클래스
            var text = "Inner Class"

            fun introduceInner(){
                println(text)
            }

            fun introduceOuter(){
                println(this@Outer.text) // 외부 클래스에 같은 이름의 속성이 있으면 @Outer를 이용해 구분한다
            }
        }
    }
```
</br></br></br>

> Data Class

&nbsp;데이터를 다루는 데에 최적화된 클래스로 5가지 기능을 내부적으로 생성한다.  
1. equals()의 자동구현  
2. hashcode()의 자동구현
3. toString()의 자동구현
4. copy()의 자동구현
5. componentX()의 자동구현  
```java
    fun main(){
        val a = General("승원",123)

        println(a== General("승원",123)) //false
        println(a.hashCode())
        println(a)

        val b = Data("유승",423)
        println(b== Data("유승",423)) //true
        println(b.hashCode())
        println(b)

        println(b.copy())
        println(b.copy("원승"))
        println(b.copy(id =666)) 
    

        val list listOf(Data("사과",123),Data("포도",333),
        Data("배",444))

        for((a,b)in list){// a= compnent1, b= compnent2
            println("$a,$b")  
        }
    }

    class General(val name :String, val id : Int)
    
    data class Data(val name :String, val id : Int)
```
</br></br>

> Enum Class

&nbsp;enumerated type의 줄인 말로 enum 클래스내에 상태를 구분하기 위한 객체들을 이름을 붙여 여러개 생성해두고 그 중 하나의 상태를 선택하기 위한 클래스이다. 보통 대문자로 기술한다.
```java
    fun main(){
        var state = State.SING 
        println(state) //SING이 나옴

        state = State.SLEEP
        println(state.isSleeping()) //true

        state = State.EAT
        println(state.message) // 밥을 먹다
    }

    enum class State(val message : String){
        SING("노래를 부른다"),
        EAT("밥을 먹다"),
        SLEEP("잠을 자다"); //세미콜론 사용!! 함수를 뒤에 쓰기 때문에

        //boolean값 반환
        fun isSleeping() = this == State.SLEEP
     }
```
</br></br></br>

> 컬렉션 클래스

&nbsp;컬렉션 클래스에는 List,Set,Map이 있다.  
Set은 순서가 정렬되지 않으며 중복이 허용되지 않는 컬렉션이다. 인덱스로 위치를 찾을 수 없고 contains로 확인은 할 수있다. Mutable로 추가,삭제가 가능하다.  
```java
    fun main(){
        val  a = mutableSetOf("사과","포도","밤")
        
        for(item in a){
            print("${item}") //사과 포도 밤
        }
        
        a.add("딸기")
        println(a) //[사과,포도,밤,딸기]

        a.remove("밤")
        println(a) //[사과,포도,딸기]
        
        println(a.contains("포도")) //true

    }
```
&nbsp;Map은 객체를 넣을 때 그 객체를 찾아낼 수 있는 Key를 쌍으로 넣어주는 컬렉션이다. Key와 Value를 MutableEntry에 객체로 담겨져 있다. Key를 통해 객체를 참조한다.
```java
    fun main(){
        val a = mutableMapOf("사과" to "빨강", "바나나" to "노랑",
        "포도" to "보라")
    
    for(entry in a){ //사과 :빨강  바나나 : 노랑  포도 :보라
        println("${entry.key} : ${entry.value}")
    }
    
    a.put("귤","주황")
    println(a) // 사과=빨강,바나나=노랑,포도=보라,귤=주황

    a.remove(사과)
    println(a) //바나나=노랑,포도=보라,귤=주황

    println(a["바나나"]) // 노랑
         
    }
```
</br></br></br>

> 컬렉션 함수1

&nbsp;컬렉션 또는 배열에 일반함수 or 람다함수 형태를 사용하여 for문 없이도 여러가지 함수를 나타낼 수 있다.  
1. collection.forEach{println(it)} it이라는 변수로 순서대로 참조된다  
2. collection.filter{it>5} it의 조건에 맞는 객체만 컬렉션으로 만들어 반환
3. collcetion.map{it+2} it의 수식을 적용하여 그 값을 컬렉션으로 만들어 반환
4. collection.first{it>3} 조건에 맞는 첫번째 반환  
5. collection.count{it<8} 조건에 맞는 개수 반환
만약 조건에 맞지 않는 경우이면 NoSuchElementException이 발생한다.  
이때는 firstOrNull 이나 LastOrNull을 사용하면 Null을 반환한다.
```java
    val fruitList = listOf("딸기","수박","참외","메론","키위")
    fruitList.forEach{print(it + " ")} // 딸기,수박,참외,메론,키위
    println()

    println(fruitList.filter{it.startWith("수")}) // 수박

    println(fruitList.map{ "과일이름 : "+ it}) //과일이름 : 딸기, ...

    println(fruitList.any{it == "사과"})  // true

    println(fruitList.frist{it.startWith("메")}) //메론

    println(fruitList.count{it.contains("위")}) //1
```
</br></br></br>

> 컬렉션 함수2
1. collection.associateBy{it.속성}  
&nbsp;객체에서 키를 따로 뽑아내서 map으로 만드는 함수  

2. collection.groupBy{it.속성}  
&nbsp;특정한 값을 key로 지정하여 해당값을 가진 객체끼리 묶은 value로 하는 map을 만들어주는 기능이다.  

3. collection.partition{it.속성}  
&nbsp;아이템에 조건을 걸어 true,false인지 두 컬렉션으로 나눈다.  

4. collection.flatMap{listOf (it+3,it+4)}
&nbsp;중괄호안에서 아이템마다 새로운 컬렉션을 생성하면 하나의 컬렉션으로 반환해준다.  

5. collection.getOrElse(1){50}
&nbsp;괄호안에 지정한 인덱스에 객체가 존재하는 경우 그것을 반환하고, 없는 경우 괄호안에 있는 값을 반환한다  

6. collectionA zip collectionB
&nbsp;두 컬렉션에 포함된 아이템을 1:1로 Pair클래스의 객체로 만들어 List에 넣어 반환해준다. 이때 결과 List의 아이템의 개수는 더 작은 컬렉션을 따라간다.

```java
    fun main(){
        data class Fruit(val fruit:String, val price:Int)

        val fruitList = listOf(Fruit("사과",2000),Fruit("배",2000)
        ,Fruit("메론",5000))

        println(fruitList.associateBy{it.price})
        //사과랑 배 묶임

        println(fruitList.groupBy{it.price})

        val numbers =listOf(-1,2,3,-5)

        println(numbers.flatMap{ listOf(it*5,it+5)})
        //[-5,4,10,7 ...]

        println(numbers.getOrElse(50){50}) //50

        val names = listOf("A","B","C'","D")

        println(names zip numbers) // [(A,-1),(B,2),(C,3),(D,-5)]
    }
```
</br></br></br>

> 변수의 사용방법29

&nbsp;


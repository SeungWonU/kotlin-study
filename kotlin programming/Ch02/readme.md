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
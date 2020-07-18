## 3. 리스트

> 리스트(List)

&nbsp;데이터를 코드에서 지정한 순서대로 저장하는 것을 리스트라고 한다. List는 데이터를 모아 관리하는 Collection Class 중  
  가장 단순한 형태로 여러개의 데이터를 원하는 형태로 넣어 관리하는 것이다. 두 가지 종류가 있는데 List와 MutableList가 있다. Mutable은 대체,추가,삭제가 가능하다.  

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
1. **collection.forEach{println(it)}**  :   it이라는 변수로 순서대로 참조된다  
2. **collection.filter{it>5}**  :  it의 조건에 맞는 객체만 컬렉션으로 만들어 반환
3. **collcetion.map{it+2}**  :  it의 수식을 적용하여 그 값을 컬렉션으로 만들어 반환
4. **collection.first{it>3}**   :  조건에 맞는 첫번째 반환  
5. **collection.count{it<8}**  :   조건에 맞는 개수 반환
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

> 변수의 사용방법

&nbsp;val은 할당된 객체를 바꿀 수 없고 val은 가능하다. 하지만 val은 객체의 내부의 속성은 변경할 수 있다.
</br>

> 상수

&nbsp;컴파일 시점에 결정되어 절대 바꿀 수 없는 값 : const val 상수 = 123  
상수는 기본 자료형만 가능하며 일반적인 다른 클래스의 객체들을 담을 수 없다.
```java
    fun main(){
        val food = FoodCourt()
        //상수에 따라 음식 가격 안내
        food.searchPrice(FoodCourt.APPLE)
        food.searchPrice(FoodCourt.DRINK)
        food.searchPrice(FoodCourt.NODDLE)
    }

    class FoodCourt{
        fun searchPrice(foodName: String){
                val price = when(foodName){
                    APPLE -> 3000
                    DRINK -> 2000
                    NODDLE -> 4000
                    else -> 0
                }
                println("${foodName}의 가격은 ${price}입니다")
        }

        companion object { // companion object안에 상수를 써서 표시한다
            const val APPLE = "사과"
            const val DRINK = "음료"
            const val NODDLE = "라면"
        }
    }
```
&nbsp; 늘 고정적으로 사용할 값은 상수를 통해 객체의 생성없이 메모리에 값을 고정하여 사용함으로써 성능을 향상시킬 수 있다.

</br></br>

> 늦은 초기화

&nbsp;변수를 선언할 때 객체를 할당하는 것을 선언과 동시에 하지 않고 싶을 때 사용한다. lateinit var 변수를 사용한다. 이는 초기값을 할당하기 전까지 변수를 사용할 수 없고, 기본 자료형에는 사용할 수 없다.  
::a.isInitialized를 사용하면 a가 초기화가 되었는지 확인할 수 있다.
```java
    fun main(){
        val a =LateInitSample()

        println(a.getLateInitText()) //기본값
        a.text = "새로운 값"
        println(a.getLateInitText()) //새로운 값
    
    }
    
    class LateInitSample{
        lateinit var text : String

        fun getLateInitText() : String{
            if(::text.isInitialized){  //a가 초기화가 되었으면
                return text //그 값을 반환
            }
            else{
                return "기본값"
            }
        }
    }
```
</br></br>

> 지연 대리자 속성

&nbsp;lateinit과 달리 val 변수에 by lazy{}를 사용한다.
```java
    fun main(){
        val number : Int by lazy{
            println("초기화를 한다")
            10
        }
        println("코드 시작!")
        println(number) // 초기화를한다 10
        println(number) // 10
        //두번째 number를 호출하면 이미 초기화를 했기 때문에 다시 초기화 구문을 실행하지 않는다!
    }
```
</br></br></br>

> 코루틴

&nbsp;메인루틴과 별도로 진행이 가능한 루틴이다. 개발자가 루틴의 실행과 종료를 제어할 수 있는 단위이다. 코루틴은 제어범위 및 실행범위를 지정할 수 있는데 이를 **코루틴 스코프**라고 한다.  

&nbsp;GlobalScope와 CoroutinScope가 있는데 GlobalScope는 프로그램 어디서든 제어나 동작이 가능하다. CoroutinScope는 특정한 목적의 Dispatcher를 지정해야만 한다.  
1. Dispatchers.Default : 기본적인 백그래운드에서 동작
2. Dispatchers.I O : I/O에 최적화 된 동작
3. Dispatchers.Main : 메인쓰레드에서 동작  

</br>

&nbsp;스코프는 또한 launch() 나 async()를 통해 새로운 코루틴을 생성할 수 있다.
launch()는 반환값이 없는 Job 객체이고, async()는 반환값 있는 Deffered 객체이다.
```java
    import kotlinx.coroutines.*
    fun main(){
        val scope = GlobalScope
        scope.lanuch{
            for(i in 1..5){
                println(i) //실행안됨, 실행즉시 종료됨으로
            }
        }


        runBlocking{ //runBlocking을 통해 막음
            var a =launch{
                for(i in 1..5){
                    println(i)
                    delay(10) 
                }
            }

            val b = async{
                "async 종료"
            }
            println("async 대기")
            println(b.await()) //1 결과를 받아 출력

            println("launch 대기")
            a.join() // 2345 끝까지 수행되기를 기다림
            println("launch 종료")
        }
    }
```
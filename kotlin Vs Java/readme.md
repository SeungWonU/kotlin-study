# Kotlin vs Java
## Kotlin 설명
&nbsp;Kotlin이란 JetBrains에서 만든 언어로 JVM에서 동작하는 프로그래밍 언어이다. 파일 확장자는 .kt 또는 .kts를 사용한다.
최근에는 안드로이드 앱 개발에 선호되는 언어가 되었다.
## Differences
1. 간결한 객체 생성
2. 값 및 변수 선언
3. Null의 안정성
4. 간결한 view 생성자
5. 접근 제한자
6. 생성자

--------------------------------------------------------------


### 간결한 객체 생성
&nbsp; **Java** : 객체를 new로 초기화 한 후에 객체를 이용한다.

```java
    Intent intent = new Intent(this,MenuActivity.class); //객체 초기화 및 생성
    intent.putExtra("Java",1);
    intent.putExtra("Kotlin",2);
```
&nbsp;이와 같은 형태로 선언을 하게 된다.  
</br>

&nbsp;**Kotlin** :객체를 new로 초기화 하지 않고 apply block을 통해 간결하게 선언할 수 있다. 코드가 block안에 내포되어 있기 때문에 한눈에 보기 좋고 가독성도 좋아진다.
```java
    val intent = Intent(this,MenuActivity::class.java).apply{ //apply block
        putExtra("java",1)
        putExtra("Kotlin",2)
    }
```
보기에는 차이가 없어 보이지만 코드가 복잡할수록 더 유용하다.  
</br></br>



### 값 및 변수 선언
&nbsp; **Java** :  타입을 항상 명시해 주어야 하고 불변의 경우 final을 붙여준다.
```java
    String name = "SeungWon";
    final int age = 24;
    Student st = new Student(name);
```
&nbsp;타입과 불변 그리고 객체 생성의 예시이다.  
</br>

&nbsp;**Kotlin** : 타입을 명시하지 않아도 타입추론을 통해 자동지정된다. 또한 불변의 경우 val로 지정하고 가변의 경우 var로 지정할 수 있다.
```java
    var name ="SeungWon" //가변
    val age = 24 //불변
    val st = Student(name) //new 없이 객체 생성
```

&nbsp;가변과 불변을 구분하고 타입을 명시하지 않아도 된다는 장점이 있다.  
</br></br>



### NULL의 안정성
&nbsp; **Java** :  @(Annotation)을 사용하여 구분이 가능하다.Nullable은 null허용 , NonNull은 null불허이다.
```java
    @Nullable String str1 = null;
    @NonNull String str2 = "notNULL";

    str1.substr(2); // error
    if(str1 != null)
        str1.substr(2); //ok
    
```
&nbsp;error부분에서는 str1이 null값이기 때문에 runtime error가 발생한다. 따라서 java에서는  if(not null)일 경우에만 실행하도록 코드를 짜야한다. 이는 번거롭고 실수할 경우 항상 error가 발생한다.  


&nbsp;**Kotlin**이를 보완하기 위해 null의 안정성을 추구하였다. 우선 ?(Optional)을 사용해 null의 여부를 구분한다. 또한 if(not null)을 하지 않아도 그 값이 null일 경우 빨간밑줄이 생기고 build를 할수 없게 된다.
```java
    var str1:String? =null
    var str2:String = "notNULL"
    str1.substr(2)  // 빨간밑줄이 생김
```
&nbsp; java보다 더 간결해지고 error의 가능성도 줄일 수 있다. 더 안전하고 코드 자체도 간결하다.  
</br></br>

### 간결한 VIEW (android)
&nbsp; **Java** : findViewById() 함수로 객체에 할당하여 view를 사용한다. 
```java
    Button bt = findViewById(R.id.bt);
    bt.setOnClickListner(new View.OnClickListner(){
        public void onClick(View view){
            System.out.println("SeungWon Button");
        }
    };
    )
```
</br>

&nbsp; **Kotlin** : id를 함수를 통해 찾지 않고 곧바로 사용할 수 있다. 훨씬더 간결하고 편하게 사용할 수 있다.
```java
      bt.setOnClickListner(new View.OnClickListner(){
        public void onClick(View view){
           print("SeungWon Button")
        }
    }
    )
```
</br>
</br>


### 접근 제한자
&nbsp; **Java** : 총 3가지 접근 제한자가 있다. *public, private, protected*
```java
    public int a=0;
    private int b=1;
    protected int c=3;
```
</br>

&nbsp; **Kotlin** : default로 *public*을 사용하고 *protected* 단점을 보완하기 위해 *internal* 접근 제한자를 사용한다. 이는 외부 모듈에서도 접근할 수 있는 점을 막기 위해 동일한 모듈에서만 접근 허용하도록 하는 제한자이다.
```java
    val a=0  //default 는 public
    protected val b=1
    private val c=2
    internal val d =3
```
</br>
</br>

### 생성자
&nbsp;**Java** : 생성자의 형태에 따라 아래와 같은 생성이 필요하다.
``` java
    public class Java{
        int a; int b;
        public Java(int a, int b){
            this.a=a; this.b=b;
        }
        public Java(int a){
            this(a,0); // a 값만 인자로 받는 생성자
        }
    }

```
</br>

&nbsp;**Kotlin** : 기본 생성자는 init 을 사용하여 대체한다. 또한 주 생성자는 아래와 같이 간결하게 작성할 수 있으며 다른 형태의 경우 *constructor*을 통해 선언할 수 있다.
```java
    public class Kotlin(a:Int, b:Int){
        init{
            //기본 생성자          
        }
    }
```
```java
    public class(val a:Int, val b:Int) //주 생성자 간결화
    constructor(a: Int) : this(a,0) // 다른 형태의 생성자
```
# Java 개발자의 C#공부

## C#에서의 Class

C#에서의 Class는 Java에서 지원하는 대부분의 기능을 지원을 하는것으로 보이며, 오히려 추가적으로 기능을 더 지원을 하는것으로 보인다. 그리고 기본적인 부분이 아닌 Class를 다루는 부분이다보니 다른 Java와 문법적인 형태가 상당히 달라지는 모습을 보여주었다.

## Method

### 참조에의한 매개변수 전달

Java에서는 참조에 의한 배개변수 전달을 위해서는 오로지 객체를 통해 전달을 하는것만이 방법였으나, C#에서는 간단하게 ref라는 명령어를 추가해 주면 된다.

```c#
public void add(int a, int b, ref int total){
    total=a+b;
}
```

위와 같이 선언을 해주고, 아래와 같이 사용을 해주면 된다.

```c#
int total=50;
add(5,6, ref total);
Console.WriteLine("{0}",total);
```

이 결과 같으로는 ```11```이 나올 것이다.

### 출력전용매개변수

출력전용 매개변수는 출력을 위해 사용이 되는 변수를 말하는데, 위의 add함수 처럼 오로지 출력을 위해서만 사용이 되는 경우를 위해 존재한다.

```c#
public void add(int a, int b, out int total){
    total=a+b;
}
```

위와 같이 선언을 해주고, 아래와 같이 사용을 해주면 된다.

```c#
int total=50;
add(5,6,out total);
Console.WriteLine("{0}",total);
```

이 결과 같으로는 ```11```이 나올 것이다.

이처럼 ```ref```를 사용한 것과 차이가 없는데 왜 귀찮게 두개의 명령어를 구분하여 사용하냐면, ```out```명령어를 사용한 메소드에 값을 넣어주지 않을경우 컴파일러 애러가 발생하여 빠른 오류의 발견을 도와주는 역활을 해준다.

### 가변길이매개변수

가변길이 매게변수는 인자값으로 몇개의 변수가 들어올지 모르는 경우에 사용이되며, 이 경우 예제는 다음과 같다.

```c#
public void Add(out int total,params int[] nums){
    total = 0;
    foreach(int num in nums)
    {
        total += num;
    }
}
```

```c#
int total = 50;
Add(out total,1, 2, 3, 4, 5, 6, 7, 8, 9);
Console.WriteLine(total);
```

위와 같이 인자 앞에 ```params```를 붙여주면, 같은 형의 여러개의 인자를 받을수 있으며, 이 ```params```가 붙는 인자는 오로지 1개만 지정이 가능하며, 인자들중 제일 뒤에 있어야 한다.

### 명명매개변수

명명매개변수는 메소드를 호출시 인자값을 지정해서 넣어주는 것이다

```c#
public void add(int a, int b, out int total){
    total=a+b;
}
```

위와 같이 선언을 해주고, 아래와 같이 사용을 해주면 된다.

```c#
int total=50;
add(a:5,b:6,total : out total);
Console.WriteLine("{0}",total);
```

이처럼 하면 코드의 가독성이 조금이나마 좋아지는 특성이 있다.

### 선택적매개변수

선택적 매개변수는 메소드의 인자에 기본값을 넣어주는 방식이다.

```c#
public void add(out int total,int a=1, int b=2){
    total=a+b;
}
```

위와 같이 선언을 해주고, 아래와 같이 사용을 해주면 된다.

```c#
int total=50;
add(out total);
Console.WriteLine("{0}",total);
```

이렇게 만든 코드를 실행하면 결과 값은 아마 ```3```이 나올것이다. 그리고 선택적매개변수는 필수매개변수 다음에 와야 한다.

## Class

### 소멸자

C#에서 소멸자는 ```~클래스명()```로 표시를 한다. 그러나 자바와 같이 가비지 컬렉션을 이용하여 객체의 메모리를 관리하기 때문에 사용하는것을 권장하지 않는다.

### this() 생성자

C#에서 this는 Java와 같은 방식으로 사용이 된다. 그러나 객체 내에서 생성자를 호출을 하는경우 다음과 같이 형태가 차이가 난다.

Java

```java
Class Test{
    String test;
    public Test(){
    }
    public Test(String test){
        this.test=test;
        this();
    }
}
```

C#

```c#
class Test{
    string test;
    public Test(){
    }
    public Test(string test) : this(){
        this.test=test;
    }
}
```

위와 같이 차이가 발생한다.

### 상속

기본적인 상속의 방법은 아래와 같으며, 아래의 방식은 오로지 생성자의방식이다.

```java
Class Test{
    String test;
    public Test(String test){
        this.test=test;
    }
}

public Test2 extends Test{
    public Test2(String test){
        super(test);
    }
}
```

C#

```c#
class Test{
    string test;
    public Test(string test){
        this.test=test;
    }
}
Test2 : Test{
    public Test2(string test):base(test){
    }
}
```

### sealed

```sealed```명령어는 상속시에 자손 클래스에게 넘겨주기 싫은 메소드에 넣어주면 상속이 되지 않는다.

```c#
class Test{
    string test;
    public sealed void showString(){
        Console.WriteLine(test);
    }
}
```

이처럼 작성을 하면 Test 클래스를 상속시 showString메소드를 오버라이딩이 되지 않게 봉인이 되며,

```c#
sealed class Test{
    string test;
}
```

이런식으로 작성을 하면, 클래스의 상속자체를 봉인을 한다.

### is as

is키워드의 as키워드는 거의 같은 키워드나 아주 약간씩 차이가 있다. 일단 기본적인 역활은 객체가 어떤 클래스를 상속했는지 체크를 해주는 키워드로 그결과값을 null로 돌려주냐 아니면 ```bool```값으로 돌려주는지에 대한 차이일 뿐 이다.
is 키워드는 ```객체 변수명 is 상속된 클래스명```식으로 사용을 하며, 결과값으로 bool값을 반환한다.
as 키워드는 ```객체 변수명 as 상속된 클래스명```식으로 사용을 하며, 결과값으로 객체값을 반환한다.

### virtual And override

일단 이 키워드는 오버라이드를 위한 키워드이다. c#에서는 Java와는 다르게, 메소드를 만들때 이 메소드를 오버라이드를 할 것인지 아닌지를 정해야 하며, 그것을 정하는 부분이 virtual키워드이다. 그리고 오버라이드를 할때는 메소드에 override라는 키워드를 추가를 해줘야한다.

```c#
class Test{
    string test;
    public virtual void showString(){
        Console.WriteLine(test);
    }
}
class Test2:Test{
    public override void showString(){
        base.showString();
        Console.WriteLine(test);
    }
}
```

### 메소드 숨기기

C#에서도 오버라이드를 자유롭게 하는 방법이 있기는 하다. 그 방법을 메소드 숨기기라고 한다.

```c#
class Test{
    string test;
    public void showString(){
        Console.WriteLine(test);
    }
}
class Test2:Test{
    public new void showString(){
        base.showString();
        Console.WriteLine(test);
    }
}
```

이런식으로 하면 ```Test Class```의 ```showString```메소드를 숨길수 있으나, 만약 ``Test test=new Test2();``라는 식의 객체를 생성하면 ```Test2 Class```의 ```showString```메소드를 
사용이 불가해 진다.

### 분할 클래스

분할클래스는 하나의 클래스에 많은 양의 메소드가 있으면, 코드를 읽기가 힘든 측면이 있어, 그 클래스를 두개로 분할을 하는것이다. 문법상으로 특이한 키워드를 쓰는것도 아니고 그냥 파일을 분할만 하면되는거라 더이상을 생략한다

## 후기

확실히 Java에 비해 다양한 키워드가 있었으며, 이러한 키워드를 통해서, 클래스를 다루는 방법이 좀더 다양한것 같다.
# Java 개발자의 C#공부

## Class

### 확장 메소드

확장 메소드는 기존 클래스의 기능을 확장하는 기법이다. 예를들어 이미 만들어서 배포가 되는 string 클래스에 내가 커스텀해서 만든 메소드를 추가 할수 있다는 것이다.

```c#
public static class 클래스이름{
    public static 반환형식 메소드이름(this 대상형식 식별자, 매개변수목록){
        ...
    }
}
```

일단 규칙은 다음과 같이 메소드를 static으로 선언을 해주어야한다.

```c#
public class Test{
    public static string stringTest(this string test){
        ...
    }
}

```

```c#
using Test;

...

string name="강성문";
name=name.stringTest();

...
```

이처럼 사용이 가능하다.

### 구조체

구조체는 c언어를 공부를 하고 자바를 공부했으면 대부분 아는 내용이어서 여기에서는 간단히 설명을 하고 넘어 가겠다. 일단 구조체는 struct명령어를 사용하며, c#에서의 구조체는 class와 거의 같다. 틀린점은 다음과 같다

|특징|클래스|구조체|
|:----:|:----|:----|
|키워드|class|struct|
|형식|참조형식|값형식|
|복사|얕은복사|깊은복사|
|인스턴스생성|new 연산자와 생성자|선언만으로 생성|
|생성자|매개변수 없는 생성자가능|매개변수가 필수|
|상속|가능|모든 구조체는 System.ValueType을 직접상속받음|

## 프로퍼티

프로퍼티는 우리가 클래스를 만들때 기본적으로 대부분의 필드를 private로 선언을 하여 필드의 오염을 최소화 하고, get메소드나 set메소드를 통해서 필드에 접근을 하는것을 간편하게 해주기 위해 존재한다. 예제는 다음과 같다.

```c#
class 클래스이름{
    데이터 형식 필드이름;
    접근한정자 데이터형식 프로퍼티이름{
        get{
            return 필드이름;
        }
        set{
            필드이름=value;
        }
    }
}
```

```c#
...

클래스이름 test=new 클래스이름();
test.프로퍼티이름="aaa";
Console.WriteLine(test.프로퍼티이름);

...
```

다음과 같이 사용이 가능하다. 물론 저런 동작을 간소화한 자동구현 프로퍼티도 있다

```c#
class 클래스이름{
    접근한정자 데이터형식 프로퍼티이름{
        get; set;
    }
}
```

### 프로퍼티와 생성자

```c#
클래스이름 인스턴스 = new 클래스이름(){
    프로퍼티1=값,
    프로퍼티2=값,
    프로퍼티3=값
}
```

### 무명형식 프로퍼티

```c#
var 인스턴스 = new {Name=값, Age=값}
```

## 배열

### System.Array

|이름|설명|
|:----:|:----|
|Sort()|배열을 정렬한다|
|BinarySearch< T >()|이진탐색을 수행합니다|
|IndexOf()|배열에서 찾고자하는 요소의 인덱스 반환|
|TrueForAll< T >()|배열의 모든 요소가 조건에 부합하는지의 여부반환|
|FindIndex< T >()|배열에서 지정한 조건에 맞는 첫번째 요소 반환|
|Resize< T >()|배열의 크기 재조정|
|Clear()|배열의 모든 요소 초기화|
|ForEach< T >()|배열의 모든 요소에 대해 동일한 작업 실행|
|GetLength()|배열에서 지정한 차원의 길이를 반환하다(인스턴스메소드)|
|Length|배열의 길이를 반환합니다(프로퍼티)|
|Rank|배열의 차원를 반환합니다(프로퍼티)|

### 2차원 배열

2차원배열의 선언은 다음과 같이 한다.

```c#
데이터 형식[,] 배열이름 = new 데이터형식[2차원 길이, 1차원 길이];

```

참고로 자바와는 다르게 2차원 배열에서 1개의 차원만 분리를해서 인자값으로 넘겨주지는 못한다.

### 가변 배열

가변배열의 선언은 다음과 같이 한다.

```c#
데이터 형식[][] 배열이름 = new 데이터형식[가변배열의 용량][];

배열이름= new int[5]{1, 2, 3, 4, 5};
```

## 델리게이트(CallBackFunction)

델리게이트는 흔히 말하는 콜백함수를 뜻하며, 인자를 값대신에 함수를 보내는 것을 말한다. 이를 좀더 전문적인 말로 하면 메소드의 주소값을 참조하여 인자값으로 보낸다고 하면 될것같다.

```c#
한정자 delegate 반환형식 델리게이트이름(매개변수 목록);
```

사용예제

```c#
namespace Test{
    delegate int MyDelegate(int a, int b);
    class Calculator{
        public int Plus(int a,int b){
            return a+b;
        }
        public static int Minus(int a, int b){
            return a-b;
        }
    }
    class MainApp{
        static void Main(string[] args){
            Calculator cla = new Calculator();
            MyDelegate del;

            del=new MyDelegate(cla.Plus);
            Console.WriteLine(del(3,4));

            del=new MyDelegate(Calculator.Minus);
            Console.WriteLine(del(7,4));
        }
    }
}
```

### 델리게이트체인

델리게이트 체인이란 하나의 델리게이트가 여러개의 메소드를 동시에 가깝게 참조를 하는것으로 먼저 호출한 메소드부터 순서대로 실행이 되는것이다.

```c#
//1번째 방법
MyDelegate del = new MyDelegate(cla.Plus)+new MyDelegate(Calculator.Minus);

//2번째 방법
MyDelegate del = new MyDelegate(cla.Plus);
del+=new MyDelegate(Calculator.Minus);

//3번째 방법
MyDelegate del = (MyDelegate)Delegete.Combine(new MyDelegate(cla.Plus), new MyDelegate(Calculator.Minus));
```

## 후기

이번에 부분에서는 Java보다 C#이 좀더 편리한 점에 대해 많이 알게 된것 같다.
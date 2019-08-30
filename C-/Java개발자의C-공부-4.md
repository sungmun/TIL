# Java 개발자의 C#공부

## 델리게이트(CallBackFunction)

### 이벤트

이벤트는 객체에서 어떠한 일이 생길경우 이를 알려주는 객체이다. 이벤트는 델리게이트와 거의 비슷하며, 델리게이트를 event한정자로 수식을 해서 만들어진다 만드는 방법은 다음과 같다

- 델리게이트 선언
- 클래스 내에 선언한 델리게이트의 인스턴스를 event 한정자로 수식해서 선언.
- 이벤트핸들러 작성(참고로 위에서 선언한 델리게이트와 일치하여야 한다.)
- 클래스의 인스턴스를 생성하고, 이 객체의 이벤트에 방금 작성한 이벤트핸들러 등록
- 이벤트가 발생시 이벤트핸들러가 호출됨

위와 같은 방식으로 이벤트를 만들수 있다

```c#
delegate void EventTest(String message);
class Test{
    public event EventTest EvnTest;
    public void TestMethod(int num){
        .....
        Evn(num);
    }
}
class MainApp{
    public static void EvnHandler(String message){
        Console.WriteLine(message);
    }
    static void Main(string[] args){
        Test test=new Test();
        test.EvnTest+=EvnHandler;

        test.TestMethod(2);
    }
}
```

이러한 식으로 작성이 가능하며, 델리게이트와 큰 차이가 없다. 그러나 이러한 event라는 것이 필요한 이유는 event는 public으로 선언이 되있어도 외부의 클래스에서 호출이 불가능하다는 특징 때문이다.

## 람다식

### Func 델리게이트

```c#
Func<int, int, int> fun=(x,y)=>x+y;
```

Func는 람다식을 좀더 편하게 사용하기 위한 식으로 ```Func<int,int,int>```라는 식에서 마지막 ```int```는 반환형이고 그외의 모든 ```int```는 인자값의 형태를 뜻한다.

### Action 델리게이트

```c#
Func<int, int> fun=(x,y)=>Console.WriteLine(x+y);
```

Func 과 매우 유사하나 반환형과 반환을 하지 않는다.

## LINQ

LINQ는 Language INtegrated Query의 약어로 데이터 질의 기능이다. 기본적으로 질문은 다음 3가지를 포함한다

- From : 어떤 데이터 집합에서 찾을 것인가
- Where : 어떤 값의 데이터를 찾을 것인가
- Select : 어떤 항목을 추출할 것인가

```c#
class People{
    public string Name{ get; set; }
    public int Age{ get; set; }
}
```

```c#
People[] MeetingMember={
    new People(){Name="첫번째멤버", Age=19},
    new People(){Name="두번째멤버", Age=20},
    new People(){Name="세번째멤버", Age=71},
    new People(){Name="네번째멤버", Age=45},
    new People(){Name="다섯번째멤버", Age=11},
    new People(){Name="여섯번째멤버", Age=32},
    new People(){Name="일곱번째멤버", Age=52},
    new People(){Name="여덟번째멤버", Age=33},
    new People(){Name="아홉번째멤버", Age=50},
    new People(){Name="열번째멤버", Age=24},
}
```

```c#
var members= from member in MeetingMember
            where member.Age < 20
            orderby member.Age
            select member

foreach(var member in  members){
    Console.WriteLine("{0} : {1}",member.Name, member.Age);
}
```

## 후기

이것 까지 대략적으로 C#에 대해 알아 보았다. 물론 Java와 큰 차이가 없는 부분이나 좀 깊숙히 알아야 하는 부분은 건너뛰었으며, 파일입출력이나, 데이터베이스 연결부분은 과감히 생략을 하였고, 서버 프로 그래밍부분도 과감히 생략을 하였다. 왜냐하면, 일단 이정도만 알아도 그외의 부분은 인터넷 검색으로 충분히 알수 있기때문에 나중에 그부분이 필요한 경우 검색으로 통해서 알아보면 된다고 생각하기 때문이다. 그러니 더 자세한부분은 내가 나중에 TIL에 올린 게시물은 보고 참고를 하던가 구글갓에게 물어보면 될것 같다.
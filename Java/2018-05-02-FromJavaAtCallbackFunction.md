# Callbackfunction란?

Callbackfunction는 ```function```내에서 매개변수를 받을 때 받는 변수중 ```function```인 것들을 Callbackfunction라고 한다. 자바8에서 추가된 기능인 람다식이 가장 큰 예이다. 자바스크립트와 같이 callback ```function```를 지원하는 언어에서는 별다른 추가 없이 매개변수를 ```function```로 주면 끝나나 Java에서는 Interface를 통해 Abstract method를 추가를 해줘야 한다.

## JavaScript 에서의 Callback Function

```javascript
function example(how,are,you){
    .....
    you();
}
example("I","am",function(){
    console.log("seungmun");
});
```
위와 같이 JavaScript에서는 변수와 ```function```를 저장하는 공간에 차이가 없기 때문에, 표시는 다른 변수와 같이 하고 ```function```내에서 실행을 시켜주면 된다. 그리고 사용은 ```function```를 따로 선언하고 해도 되고 그게 귀찮으면 위에서 처럼 ```function```를 통채로 넘겨 줄 수도 있다.

## Java 에서의 Callback Function
```java
public interface CallBackEvent {
	public void callBackEvent(Object obj); 
}
```
위와 같이 ```interface```를 만들어 주고,
```java
public class Test {
    public void testMethod1(){
        System.out.println("who are you");
    }
    public void testMethod2(CallBackEvent event){
        event.callBackEvent(this);
    }
}
```
```CallBackEvent interfac```를 매개변수로 가지는 메소드를 지닌 ```class```를 만든다. 그리고 ```event``` ```interface```에 있는 
```Abstract method```인 ```callBackEvent```를 호출한다. 이때 ```this```를 넘겨주는데 이런식으로 넘겨주면 객체를 넘겨는형식이 된다. 그래서 그 ```class```에 있는 모든 ```method```를 사용이 가능하다.
```java
public class MainThread {

	public static void main(String[] args) {
        String name="seung mun";
		Test test=new Test();

        test.testMethod2(new CallBackEvent() {
			
			@Override
			public void callBackEvent(Object obj) {
				((Test)obj).testMethod1();
                 System.out.println("who are you");
			}
		});
	}

}
```
이 코드에서 알아야  하는 부분이 있는데 우리가 ```class```를 선언하고 사용을 할때 2개의 명령어를 통합해서 대부분 사용하는데 분리를 하면,
```java
Test test=null;
```
 부분으로 자바의 ```class```를 선언하는 부분과
 ```java
 new Test();
 ```
 부분으로 자바의 생성자를 호출 함으로서 객체를 생성하는 부분이다.
 내가 왜 이부분을 알아야 한다고 했냐면, 우리가 자바에서 ```abstract method```가 있는 ```class```나 ```interface```의 객체를 생성하면 ```abstract method```를 채워야 한다. 이 말은 선언까지만 하면 추상메소드를 채울 필요가 없다는 사실이다. 참고로 자바에서는 선언만해도 그 ```class``` 내부에있는 메소드를 사용이 가능하다. 물론 선언만 한 ```class``` 내부에 있는 메소드를 사용하면 ```NullPointerException```이 발생하지만 일단 컴파일러 검사에서는 문제가 없다. 

 ## Ramda

 자바에서는 이를 지원하기 위해 자바 8부터 람다식이라는 것을 지원하는데, 위 ```java```에서 사용한 예제를 람다식으로 변경을 해보겠다.
 ```java
@FunctionalInterface
public interface CallBackEvent {
	public void callBackEvent(Object obj); 
}
```
그전과 같이 ```interface```를 만들어주고 ```@FunctionalInterface```어노미테이션을 넣어줌으로서 현재 ```interface```에 람다식으로 사용할 메소드를 하나로 고정한다.

```java
public class MainThread {
    public static void main(String[] args) {
        String name="seung mun";
        Test test=new Test();

        test.testMethod2((obj)->{
            ((Test)obj).testMethod1();
            System.out.println("who are you");
        });
    }
}
```
위에처럼 작성을 하면 되며 상당히 줄어든다. 여기에서 더 줄어 들 수 도 있는데, 만약 넘겨줄 메소드의 ```code```의 ```line```이 1줄인경우 다음과 같이 할 수도 있다.

```java
public class MainThread {
    public static void main(String[] args){
        Test test=new Test();
        String name="seung mun";

        test.testMethod2((obj)->System.out.println("who are you"));
    }
}
```
이처럼 자바에서 람다식을 사용함으로 ```code```의 ```line```을 상당히 줄여 줄수 있다.

## 필요성

```java```로 조금이라고 디자인패턴을 이용하여 프로그래밍을 하면 ```code```의 ```line```이 상당히 길어 지는데, 이런식으로 만들어지는 ```code```의 ```line```이 늘어나면 하나의 ```class```만 보고 이 ```class```가 무슨일을 하는지 한번에 이해가 어려워 진다. 이때 ```callback```을 이용하면, 하나의 ```class```를 보고 이 ```class```의 역활을 이해하는데 좀더 쉬워진다.
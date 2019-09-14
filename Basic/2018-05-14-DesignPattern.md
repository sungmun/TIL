# DesignPattern

## DesignPattern이란

DesignPattern이란 형식화된 패턴이다. 정도가 가장 정확한 설명이다. 
사람이 프로그램을 만들면서 나오는 프로그래밍 언어 내에서의 패턴을 정리하고 추상화 시켜놓은 것들을 DesignPattern이라고 하며, 개발자들은 이러한 Pattern을 습득함으로서 다름사람들이 직면했던 문제들을 좀더 쉽게 풀어나갈수 있게 되는것이다.   
물론 DesignPattern이 없이 프로그램을 만들 수는 있다. 그러나 나중에 DesignPattern을 공부하고 나면 `'어 이거는 내가 써봤던 건데'`라고 할 정도로 쉬운 DesignPattern도 있으며, DesignPattern을 모른체로는 며칠을 끙끙대면서 만든것이 DesignPattern에는 이미 규정이 되있는경우도 있고, 다른 개발자들과 소통을 할 때에도, DesignPattern의 명칭을 말하면 쉽게 소통이 되는 경우가 있어서 왠만해서는 알고 있어야 하는 부분이다.

## 대표적인 패턴

일단 대표적인 패턴으로는

- Model-View-Controller Pattern
- Observer Pattern
- ValueObject Pattern
- Single Pattern

이정도는 왠만해서는 알고 있어야 하는 패턴이다.

## Model-View-Controller Pattern

`Model-View-Controller Pattern`은 줄여서 `MVCPattern`이라고 하며, 보통 웹에서 많이 쓰이나, 클라이언트에서도 사용이 가능하다.
 이 패턴의 핵심은 하나의 프로그램을 Model-View-Controller로 분리를 하여 View에서 Model에 속하는 메소드나 클래스를 호출할 때, Controller를 통해서 호출을 해야하며 Model에서 View에 변경을 주려면, Controller를 통해서 호출을 해야한다.    
이러한 방식을 통해 Model에 변경을 줄 때 View에 최소한의 변경을 가하게 해주며, 그 반대의 경우에도 마찬가지로 Model에 적은 변화만 가져오게 된다.    
 그리고 이때 Model과 Controller와 View의 구분을 제대로 해 주는것이 좋은데 나의 경우는 Model에는 연산작용을 하는 대부분의 클래스가 모여있고, Controller에서는 Model에서 연산을 하고 나온 결과물을 전달을 해 주는 클래스와 결과물을 View에 맞게 변환을 해주는 클래스 그리고 View에서 일어나는 상호작용을 담당하는 Action클래스로 이루어져 있다. 
 그리고 View에서는 최대한 연산없이 출력만 하는 클래스로만 구성이 되있다.

## Observer Pattern

`Observer Pattern`은 객체에서 객체로 메세지를 전달을 해주는 패턴으로 주로 Action Listener에서 사용이 된다. 
예를 들어 A라는 객체에서 동작이 이루어지면 B라는 객체에 동작이 이루어 졌다는 사실을 전송을 해 줄 수 있다. 
이 패턴은 주로 `MVCPattern`에서 주로 사용이 가능하다.

## ValueObject Pattern

`ValueObject Pattern`은 클래스에 멤버변수는 전부 private로 선언을 해주고 접근은 오로지 set메소드와 get메소드를 통해서 접근을 해주는 패턴이며, 객체를 설계할때 오로지 값을 저장하기 위한 객체로 설계를 한다.    
이패턴을 사용함으로서 멤버변수의 접근과 변경을 제어가 가능하게 해준다.
 이 패턴을 다른 말로 하면 Bean이라고 한다.

## Single Pattern

`Single Pattern`은 객체를 생성을 할 때, 1개의 객체만 생성을 하도록 제한을 하는 패턴으로, 예를들어 통신프로그래밍을 할 때, 클라이언트 부분에서 서버로 접근을 하는 클래스는 1번만 생성을 해주는 것이 좋기때문에 클라이언트에서 여러번 생성을 하려고 해도 오로지 하나의 객체만 유지를 할 수 있도록 제한을 하는 패턴이다.      
예제로는

```java
public class Example{
    private static Example instance;
    private Example(){
        ....
    }
    public static Example getNewInstance(){
        if(instance==null){
            instance=new Example();
        }
        return instance;
    }
}
```

위와같이 메소드를 선언을 해주면 다른 클래스에서 생성자에 접근이 불가능 해지며, 오로지 생성은 `getNewInstance()`메소드를 통해서 접근이 가능해진다.     
이러한 접근법을 사용함으로서, `Example`클래스는 오로지 하나의 객체만 생성이 가능해며, 메모리를 좀더 효율적으로 사용이 가능해진다.  
# DesignPattern

## DesignPattern이란

DesignPattern이란 형식화된 패턴이다. 정도가 가장 정확한 설명이다. 사람이 프로그램을 만들면서 나오는 프로그래밍 언어 내에서의 패턴을 정리하고 추상화 시켜놓은 것들을 DesignPattern이라고 하며, 개발자들은 이러한 Pattern을 습득함으로서 다름사람들이 직면했던 문제들을 좀더 쉽게 풀어나갈수 있게 되는것이다. 물론 DesignPattern이 없이 프로그램을 만들 수는 있다. 그러나 나중에 DesignPattern을 공부하고 나면 ```'어 이거는 내가 써봤던 건데'```라고 할 정도로 쉬운 DesignPattern도 있으며, DesignPattern을 모른체로는 며칠을 끙끙대면서 만든것이 DesignPattern에는 이미 규정이 되있는경우도 있고, 다른 개발자들과 소통을 할 때에도, DesignPattern의 명칭을 말하면 쉽게 소통이 되는 경우가 있어서 왠만해서는 알고 있어야 하는 부분이다.

## 대표적인 패턴

일단 대표적인 패턴으로는

- Model-View-Controller Pattern
- Observer Pattern
- ValueObject Pattern
- Single Pattern

이정도는 왠만해서는 알고 있어야 하는 패턴이다.

## Model-View-Controller Pattern

Model-View-Controller Pattern은 줄여서 MVCPattern이라고 하며, 보통 웹에서 많이 쓰이나, 클라이언트에서도 사용이 가능하다. 이 패턴의 핵심은 하나의 프로그램을 Model-View-Controller로 분리를 하여 View에서 Model에 속하는 메소드나 클래스를 호출할 때, Controller를 통해서 호출을 해야하며 Model에서 View에 변경을 주려면, Controller를 통해서 호출을 해야한다. 이러한 방식을 통해 Model에 변경을 줄 때 View에 최소한의 변경을 가하게 해주며, 그 반대의 경우에도 마찬가지로 Model에 적은 변화만 가져오게 된다. 그리고 이때 Model과 Controller와 View의 구분을 제대로 해 주는것이 좋은데 나의 경우는 Model에는 연산작용을 하는 대부분의 클래스가 모여있고, Controller에서는 Model에서 연산을 하고 나온 결과물을 전달을 해 주는 클래스와 결과물을 View에 맞게 변환을 해주는 클래스 그리고 View에서 일어나는 상호작용을 담당하는 Action클래스로 이루어져 있다. 그리고 View에서는 최대한 연산없이 출력만 하는 클래스로만 구성이 되있다.
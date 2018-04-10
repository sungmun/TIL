# Junit 사용하기

Junit은 Java에서의 단위 테스트를 위한 프레임 워크로 Juint의 사용법을 알아보자

## 목록

- 설명
- 시작하기
- 기본적인 어노테이션

## 설명

Junit은 단위 테스트를 하기위한 자바 프레임워크인데 이 단위테스트를 좀더 쉽게 만들어 주는 역활이다. 단위 테스트는 자바에서 작은 단위인 메소드를 실행시켜보고 원하는 값이 나오는지를 테스트 하는 것이다. 물론 Junit에서는 실행속도도 원하는 속도 이하로 나왔는지 테스트를 해주니 속도가 중요한 프로그램에서도 충분히 쓸만하다

## 시작하기

1. 단위테스트를 하기위한 Class를 정한다.
2. 클래스를 오른쪽 클릭하고 New를 누르면 JunitTestCase를 선택할 수 있다
3. JunitTestCase를 선택하면, 단위 테스트를 위한 클래스를 만드는 창이 나오는데 이때 Next를 누르자.
4. Next를 누르면 지정한 Class의 메소드와 지정한 Class가 상속받은 클래스의 메소드가 나온다. 이때 단위 테스트를 원하는 메소드를 선택하자
5. 그럼 선택한 메소드가 다음과 같이나온다.

<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px; border-right:2px solid #4f4f4f"><div style="margin:0; padding:0; word-break:normal; text-align:right; color:#aaa; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div></div></td><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">@Test</div><div style="background-color:#303030; padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">void</span>&nbsp;testBackgroundImage()&nbsp;{</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;&nbsp;&nbsp;fail(<span style="color:#ffd500">"Not&nbsp;yet&nbsp;implemented"</span>);</div><div style="background-color:#303030; padding:0 6px; white-space:pre; line-height:130%">}</div></div></td><td style="vertical-align:bottom; padding:0 2px 4px 0"></a></td></tr></table></div>

6. 이제 원하는 테스트를 진행을 해주면 되는데 다음과 같이 수정을 해주면 된다.

<div class="colorscripter-code" style="color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; position:relative !important; overflow:auto"><table class="colorscripter-code-table" style="margin:0; padding:0; border:none; background-color:#272727; border-radius:4px;" cellspacing="0" cellpadding="0"><tr><td style="padding:6px; border-right:2px solid #4f4f4f"><div style="margin:0; padding:0; word-break:normal; text-align:right; color:#aaa; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="line-height:130%">1</div><div style="line-height:130%">2</div><div style="line-height:130%">3</div><div style="line-height:130%">4</div><div style="line-height:130%">5</div><div style="line-height:130%">6</div></div></td><td style="padding:6px 0"><div style="margin:0; padding:0; color:#f0f0f0; font-family:Consolas, 'Liberation Mono', Menlo, Courier, monospace !important; line-height:130%"><div style="padding:0 6px; white-space:pre; line-height:130%">@Test</div><div style="padding:0 6px; white-space:pre; line-height:130%"><span style="color:#ff3399">void</span>&nbsp;testBackgroundImage(){</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;지정한클래스&nbsp;temp&nbsp;<span style="color:#0086b3"></span><span style="color:#ff3399">=</span><span style="color:#ff3399">new</span>&nbsp;지정한클래스의생성자;</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;&nbsp;assertEquals(원하는&nbsp;값,&nbsp;테스트를&nbsp;할&nbsp;메소드);</div><div style="padding:0 6px; white-space:pre; line-height:130%">}</div><div style="padding:0 6px; white-space:pre; line-height:130%">&nbsp;</div></div></td></tr></table></div>
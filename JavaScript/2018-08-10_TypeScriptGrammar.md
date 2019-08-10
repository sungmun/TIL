# TypeScript

typescript는 javascript기반의 객체지향 언어이다.

우선 typescript의 장점을 얘기부터 해보자

1.  javascript최신 스펙을 포함한다.
2.  typescript를 사용하여 개발시 사용을 않할때보다 Production환경에서 나오는 Error가 15%정도 적개 나온다.

단점은

1.  코드가 길어진다.
2.  처음 배울시 새로운 언어를 배우는 듯한 느낌이 든다.
3.  추가적인 컴파일이 필요하다.

위와 같이 있는데, 하나하나 설명을 하면, typescript는 javascript 최신 스펙을 모두 포함할 뿐만 아니라 추가적으로 제공을 해주며 typescript를 사용시 Production환경에서 Error가 적게 나온다는 말은 엄격한 검사를 하는 경우 컴파일링 단계에서 찾는 Error가 15%정도 된다사실을 이용한 것이다. 그리고 코드가 길어진다는 점은

장점

1.  javascript최신 스펙을 포함한다.
    - typescript는 javascript 최신 스펙을 모두 포함할 뿐만 아니라 추가적으로 제공을 해준다
2.  typescript를 사용하여 개발시 사용을 않할때보다 Production환경에서 나오는 Error가 15%정도 적개 나온다.
    - 엄격한 검사를 하는 경우 컴파일링 단계에서 찾는 Error가 15%정도 된다

단점

1.  코드가 길어진다.
    - 인터페이스와 같은 형식을 지정해줘야하기 때문에 코드는 길어질 수 있다.
2.  처음 배울시 새로운 언어를 배우는 듯한 느낌이 든다.
    - typescript는 C#과 매우 비슷하며, typescript 컴파일러는 javascript문법과 호환이 가능하여 typescript에서 필요한 부분만 사용이 가능하다.
3.  추가적인 컴파일이 필요하다.
    - 최신 javascript 명세를 사용을 하려면 순수자바스크립트에서도 컴파일을 해줘야한다.

## 시작하기

```bash
npm -g install typescript
```

or

```bash
npm -D install typescript
```

이를 이용하여 typescript를 설치가 가능하다. 이후 typescript를 사용하려면 프로젝트 루트 폴더에 tsconfig.json을 만들어주어야 한다. [이곳](https://www.typescriptlang.org/docs/handbook/compiler-options.html)을 보면 설정파일의 설정법이 나와있다

**VScode에서 사용을 하는 경우 [이곳](https://code.visualstudio.com/docs/typescript/typescript-compiling)을 확인하면 쉽게 빌드하는 법이 나와있다.**

## 문법

typescript의 문법은 function이 다른데, 우선 함수부터 설명을 하면

```typescript
function sum(num1: number, num2: number): number {
  return num1 + num2;
}
```

기존의 javascript와 차이점은 형을 지정해주는 부분으로, :number 부분이 형을 지정해주는 부분이다. 함수옆의 :number부분도 반환값의 형을 지정해주는 부분이다. 이처럼 typescript의 가장 큰 차이점이 형지정부분이다. 물론 이부분을 간단히 회피하는 방법이 있는데, 이방법은 number대신 any를 넣어버리는 것이다. 이 경우 자바스크립트같이 사용이 가능하나 협업을 하는 경우 코드의 가독성이 떨어지게 되니 주의하자.

이런식으로 대부분의 부분이 형을 지정해주며, 코드의 확장성을 위해 제너릭으로 형을 지정을 해줄수도 있다.

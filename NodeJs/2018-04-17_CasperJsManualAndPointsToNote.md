# CasperJS

CasperJS는 헤드리스 브라우저인 PhantomJS를 사용하여 웹크롤링을 하는데 주로 사용되는 NodeJS API이다. 이 CasperJS를 이용하면 웹 로그인을 하고 로그인을 한뒤에 나오는 페이지에 들어간다음 페이지의 html을 긁어올 수도 있고 캡쳐를 찍을 수도 있다. 이러한 다양한 기능을 조합해서 웹페이지에 들어가 반복적인 동작을 자동화 할수 있으니 ~~코딩을 잘한다면~~ 매우 편리한 것이다 .

## PhantomJS

CasperJS에 들어가기 전에 PhantomJS는 위에 말했다 싶이 헤드리스 브라우저인데 이 PhantomJS의 원 목적은 개발자가 웹과 관련되있는 것들을 만들었을때 다수의 테스트를 해야하는 경우 그러한 동작을 자동화 시켜주기 위해 만들어 진 것이며, CasperJS는 그러한 PhantomJS를 사용하기 쉽게 만들어 주는 API일 뿐이다.

## 시작

일단 CasperJS를 시작하기 위해서는 당연하게 *NodeJS*와 *npm*이 설치 되있어야 한다.

이 두가지가 설치가 되있으면, npm을 통하여 phnatomJS와 casperJS를 설치를 추가적으로 해주어야 한다. 이때 이 두 모듈은 글로벌로 설치를 해주어야 한다
```
npm install -g phantomjs
npm install -g casperjs
```
이처럼 두개의 모듈이 설치가 끝나면 이제 CasperJS를 사용이 가능하다

## 접속한 사이트를 캡쳐하는 간단한 예제
```javascript
var casper=require('casper').create();
casper.start();

casper.viewport(1920,1080);

casper.userAgent('Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36');

casper.open('https://sungmun.github.io/TIL/NodeJs/2018-04-17_CasperJsManualAndPointsToNote.html');

casper.then(function(){
    this.capture('git-casperjs.png',{
        top:0,left:0,width:1920,height:1080
    });
});

casper.run();
```
이와 같이 코드를 작성한뒤 capture.js로 저장을 한뒤에 저장한 폴더에서  cmd창으로 들어가서 ```casperjs capture.js```를 입력하면 위에 있는 url부분에 해당하는 페이지가 *git-casperjs.png*로 캡처가 되어 있을 것이다.

한줄 한줄 해석을 하면
```javascript
var casper=require('casper').create();
```
맨처음 casper모듈을 선언을 해주는 부분으로 이부분에서 다양한 설정을 해줄수 있지만 생략했다.
```javascript
casper.start();
```
casper을 선언해 주었으니 지금부터 casper을 통해서 phantomjs브라우저를 실행하겠다는 의미이다.
```javascript
casper.viewport(1920,1080);
casper.userAgent('Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.181 Safari/537.36');
```
크롤링을 할경우 헤드리스 브라우져를 사용해야 하는 이유중 하나로 보통의 다른 언어를 이용하여 크롤링을 할경우 서버와 데이터를 주고 받아야 하는 경우 서버에서 데이터를 못받게 됨으로서 크롤링을 당하고 있다ㅏ는 사실을 바로 알 수 있으나, casperjs를 이용할 경우 *userAgent*나 *viewport*를 이용하여 서버에서 상시적으로 요구를 할 수 있는 정보를 저장해두고 바로 바로 전달을 해 줄 수 있다. 이때 *userAgent*는 현재 접속을 하고 있는 컴퓨터의 정보와 브라우저의 정보 등을 담고 있는 부분이고 viewport는 브라우져를 열었을때, 브라우져 창의 크기를 나타내는 부분이다.
```javascript
casper.open('https://sungmun.github.io/TIL/NodeJs/2018-04-17_CasperJsManualAndPointsToNote.html');
```
기본적인 설정이 끝났으니 casperjs를 통해 현재 페이지에 접속을 하는 부분이다. 만약, 다른 페이지를 열어보고 싶으면 url부분만 바꾸면 된다.

```javascript
casper.then(function(){
    동작...
});
```
페이지를 열었으니 할 동작을 정해주는 부분으로 Nodejs와 달리 비동기로 이루어 진다는 점이 특이하며, 전의 동작이 이루어 져야 이동작이 이루어 진다. 함수는 심플하게 ```casper.then(callback);```으로 아루어 져있다
```javascript
casper.capture('git-casperjs.png',{
    top:0,left:0,width:1920,height:1080
});
```
캡쳐를 하는 동작으로 then으로 전달되는 콜백함수 내부에 위치해있다. 함수는 ```casper.capture(캡처할 파일의 주소문자열, 캡처할 부위를 지정한 배열);```으로 이루어 져있다.

## 주의할 점
CasperJS는 npm에서 다운을 받을 수는 있지만 node에서 실행이 되지 않는다 위에서 실행예제를 보았다 시피 casperjs를 통해서 실행이 된다. 문제는 이런식으로 실행이 되는 방식이다 보니 npm에서 다운을 받을 수 있는 다양한 모듈을 사용한다는 것을 포기하는게 쉽다. 물론 node에서 기본적으로 지원이 되는 모듈은 지원을 해준다.

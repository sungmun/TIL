# JavaScript문법

JavaScript이하 js의 간단한 문법에 대하여 기록할 것이다.

## 변수 선언

js는 변수를 선언할때 다른 언어와는 다르게 변수의 형을 지정해주지 않으며, 간단하게 
'var 변수명' 과 같이 선언을 해준다. 이때 변수에 들어갈 수 있는 값으로는 정수, 실수, true, false, 문자열, 함수 등이 들어간다.
이때 문자열은 
```javascript
 var str='문자열'
 ```
 과 같이 ```'```(작은 따음표)로 묶어 주던가 
 ```javascript
 var str="문자열"
 ```
 과 같이 ```"```(큰 따음표)로 묶어주면 문자열로 인식을 한다.


## 제어문

js에서 제어문은 C에서 사용되는 제어문을 대부분 사용을 한다. 추가가 되는 부분은 for문의 새로운 특성부분정도만 알면 된다.
```javascript
for(var i in array){
    console.log(i);
}
```
위 와 같이 for문을 사용하는 경우, ```array```에 있는 값이 앞에 서부터 차례대로 ```i```에 들어가서 실행이 된다.

## 함수

js에서의 가장 큰 특징중 하나가 함수이다. 일단 기본적인 사용법은 
```javascript
var fun=function(params) {
    ....
}
```
과 같이 함수를 정해주고 그 함수를 변수에 저장을 하여 사용하는 방법과, 
```javascript
function fun(params) {
    ....
}
```
C와 같이 함수명을 정해주고 그 함수 명을 호출하는 사용하는 방법이 있다.
이때 ```params```를 넘겨 줄수 있는데 넘겨주는 값은 함수가 될수 도 있어서 넘겨주는 값이 함수일경우 이 값을 콜백함수라고 한다

```javascript
function fun(params) {
    ....
    params();
}

fun(function(){
    console.log('callBackFunction');
});
```
위와 같이 사용이 가능하며, 위와 같이 사용을 할경우, fun함수를 실행후 ```'callBackFunction'```문자열을 console창에 출력을 해주며 끝이 날것이다.

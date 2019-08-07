# Error Process

Express에서 Error를 처리하기 위한 프로세스은 여러가지가 있는데, try-catch방법, promise-catch, next-error 방법이 있다. 이 3가지 방법의 사용을 위한 대략적인 설명과, next-error의 자세한 설명을 소개하겠다.

## try-catch 

try-catch방법은 대부분의 프로그래밍 언어에서 사용하고 있는 방식으로
```javascript
try{
    ...
}catch(e){
    ...
}
```
위와 같은 방식으로 사용을 하는데 try내부에 Error가 나올수도 있는 코드를 작성후, Error가 나오는 경우 바로 catch로 넘어가 Error를 핸들링을 해주는 방법이다. 이때, catch에 인자값으로 넘어가는 e값은 Error 클래스값을 받는다.

## promise-catch

promise-catch방법은 Promise 패턴을 이용한 방법으로
```javascript
Promise
    .then(()=>...)
    .then(()=>...)
    .then(()=>...)
    .catch(e=>...)
```
위와 같은 방식인데, 이때 try-catch방식과는 다르게, Promise객체를 이용하여, then에서 Error가 나올경우 catch에서 처리를 해주는 방식이다.

## next-catch

next-catch방식은 위의 다른 방식들과 다르게 express에서만 사용이 가능한 방식이다.
```javascript
next(new Error('Test Error'))
```
---
```javascript
app.use((err,req,res,next)=>{
    ...
})
```
첫 번째 코드는 router의 controller부분에서 사용이 되는 코드로, next에 인자값으로 error값을 넘기는경우 express에서 자동으로 error 처리 미들웨어인 두번째 코드로 넘겨준다. 이때 error 처리 미들웨어는 총 4개의 인자값을 가지며, 모든 미들웨어중 마지막에 넣어준다. 이런식으로 Error를 처리를 해주는것이 node의 비동기적인 측면에서도 좋으며, Custom Error를 이용하여, 코드의 중복을 막아줄 수도 있다.
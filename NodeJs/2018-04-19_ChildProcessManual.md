# ChildProcess란?

childprocess는 node에서 child_process모듈을 이용하여 현재 쉘이 아닌 다른 쉘을 이용하는 방법으로 node의 특징인 싱글스레드의 성능문제의 해결 방법중 하나이다. node에서 child_process를 호출하고 실행을 할때 child_process를 호출하고 실행하는 프로세스를 부모 프로세스라고 하고 실행되는 프로세스를 자식 프로새스라고 한다.

## spawn 기초 예제

```javascript
var child=require('child_process');
var spawn=child.spawn('ls',['-al','~/']);
```
간단한 예제로 ```spawn```방식을 이용하여 ```ls -al ~/```을 실행하는 프로세스를 만들어 보았다 물론 이렇게만 하면 아무것도 나오지 않는다. 여기에 자식프로세스에서 보내는 데이터를 받아주는 부분을 정해줘야 결과값이 나온다

```javascript
spawn.stderr.on('data', function(data){
    console.log('stderr: '+data.toString())
});
  
spawn.stdout.on('data', function(data){
    console.log('stdout: '+data.toString());
});

spawn.on('exit',function(code,signal){
   console.log('exit: ');
});
```
이는 자식프로세스에서 오는 데이터를 받는 방법 3가지로, 위에서 부터 애러메세지, 메세지, 종료메세지에 해당한다. 이처럼 ```spawn```방식은 자식 프로세스와 지속적인 데이터를 스트리밍하기에 적합한 방식이다.

## exec 기초예제
```javascript
var child=require('child_process');
var exe=child.exec('ls -al ~/', (error, stdout, stderr) => {
  if (error) {
    console.error(`exec error: ${error}`);
    return;
  }
  console.log(`stdout: ${stdout}`);
  console.log(`stderr: ${stderr}`);
});
```
exec방식은 자식 프로세스와 주고 받을 데이터가 별로 없을 때 사용되며, 간단한 결과물들을 받을 때 사용된다.

## frok 기초예제

```javascript
var child = require('child_process');
var fork = child.fork('./worker');
child.on('message', function(m) {
  console.log('received: ' + m);
});

child.send('Please up-case this string');
```
worker.js
```javascript
process.on('message', function(m) {
  m = m.toUpperCase();

  process.send(m.toUpperCase(m));
});
```
위 예제는 스택오버플로워에서 퍼온 것이다.
일단 다른 방식들과는 큰 차이점이 있는데 그것은 바로 데이터를 주고 받는 다는 것이다. 다른 방식들은 데이터를 받기만 했지만 ```fork``` 방식은 데이터를 주고 받는다. 하나 하나 코드를 설명 하자면, 일단 부모 프로세스 2번째 줄을 통해 node worker.js를 실행하고 부모프로세스에서 자식 프로세스에서 데이터가 오면 어떠한 동작을 할것인지 ```child.on('message',function())```을 통해 정해준다 그다음 자식 프로세스에서 ```Please up-case this string```라는 문자열을 전해준다. 그럼 ```worker.js```에서는 일단 데이터가 오면 무었을 할것인지 정해주는데 그부분이 바로 ```process.on('message', function(m)) ```부분이다. 여기에서 function부분을 보면 ```m = m.toUpperCase();```부분이 있는데 이부분은 영어를 모두 대문자로 변환해주는 함수이고 ```process.send(m.toUpperCase(m));```부분은 대문자가 된 문자를 부모 프로세스에게 전해준다는 의미이다. 문자를 받은 부모 프로세스는 이제 아까 자식프로세스가 데이터가 오면 어떤식으로 할것인지 정해놓은 대로 동작으로 한다.

## 단점

일단 기본적으로 childprocess는 node의 한계이자 특징인 싱글스레드를 극복하는 방법으로 유용한 방법이다. 그러나 이 방식은 멀티프로세스의 단점인 메모리 관리에 취약한 측면이 있으며, 서버 동작시에 죽지 않는 프로세스가 생기면 서버가 죽어 버릴수도 있다는 점이 있어 조심히 사용을 해야된다.
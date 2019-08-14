# Sequelize 사용법 3

Sequelize의 CRUD(Create Read Update Delete)기능에 대하여 시작을 해보자.

일단 Sequelize를 사용을 하기 위해서는 sequelize-cli를 이용하여 만든 models 부분의 index.js파일을 호출을 하여주어야한다.

```js
import Model from "/models";
```

위와 같이 호출을 하고나면 `Model.User`이 처럼 모델들을 호출하여 사용이 가능해진다.

## Find

우선은 CRUD에서 가장 간단한 Read에 해당하는 부분을 소개 하겠다.

```js
Model.User.findOne({
  where: {
    id: 1
  }
});
```

위와 같이 사용을 하면 User테이블에 id값이 1인 값을 찾아서 프로미스의 형태로 id값이 1인 모델을 반환해준다.

Sequelize 는 기본적으로 Promise형태의 비동기 ORM으로 사용을 위해서는 Promise Chain으로 사용을 하던가, async/await를 사용을 하여야 한다.

프로미스 형태를 벗겨내도 모델 형태의 객체로 전달을 해줘서 바로 전달하기에 무리가 있는데, 그럴때,

```js
Model.get({ plain: true });
```

를 사용하면 전달하기 좋게 깔끔한 데이터 형이 나온다. 물론, 모델형태의 장점은 데이터를 추가적으로 가공을 해야하는 경우 바로 가공이 가능해 상당히 편하다는 장점이 있다.

예를 들어 저번편에 해놓은 관계설정을 이용하여 Join을 하는 방법은 2개정도가 있는데, 첫번째는

```js
Model.회사.findOne({
  include: {
    model: 직원
  },
  where: {
    id: 1
  }
});
```

위와 같은 방식과

```js
const 남의회사 = await Model.회사.findOne({
  where: {
    id: 1
  }
});
const 남의회사사원 = 남의회사.get사원();
```

이렇게 보는 방식이 있는데, 전자의 방식의 장점은 비교적으로 Document나 다른곳에 자세히 나와있는 방식이라는 장점이 있으나, 관계가 깊어지면 상당히 복잡해진다는 단점이 있다. 그에 비해 아래의 방식은 상당히 깔끔한 상태를 관계가 깊어져도 유지가 가능하다는 장점이 있으나, Promise Chain을 이용시 위의 방식보다 더 복잡해지는 점과, 문서가 좀 부실하다는 단점이 있다.

이외에도 아래의 방식(시멘틱테그)은 여러가지의 형태를 띄우고 있는데 기본적으로 get,set,add 등이 있으며, 사용의 방식은 연관관계설정을 해놓은 필드의 명을 뒤에 붙이는 형식으로 사용이 가능하다.

## Create

Create는 추가적으로 설명할부분이 적은 관계로 간단히 사용법만 적겠다

```js
Model.회사.create({ 회사정보 });
```

## Update

```js
const 남의회사=await Model.회사.build({회사정보}).reload()
...변경...
남의회사.save()
```

OR

```js
Model.회사.update({
    ...변경할데이터...
})
```

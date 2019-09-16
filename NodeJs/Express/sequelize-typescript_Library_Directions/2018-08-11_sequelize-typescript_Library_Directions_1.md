# sequelize-typescript

sequelize를 사용하는 프로젝트에 typescript를 도입을 하기위해 필요한 라이브러리이다. sequelize에서도 지원은 가능하다고 하나, 딱히 추천을 하고 있지 않고 있기도 하고, sequelize-cli에서 만든 파일들이 동작이 되지 않아 sequelize를 사용하기 위해 찾아본 라이브러리이다.

## 알아야 할점

- 타입스크립트다.
- model파일을 재작성해야한다
- 마이그레이션파일이 없다
- seed파일도 따로 없다.
- 시멘틱태그(addUser같은 함수)의 사용이 불가한것같다.
- 돌려서 사용은 가능하다.
- 함수도 조금씩 바뀐부분이 있다.
- sequelize가 필요하지는 않는것 같다

## model

위에서 말한대로 model파일을 Typescript에 맞게 다시 작성을 해줘야한다.

```typescript
import {
  Model,
  Table,
  Column,
  AutoIncrement,
  PrimaryKey,
  DataType
} from "sequelize-typescript";

@Table
export class User extends Model<User> {
  @PrimaryKey
  @AutoIncrement
  @Column(DataType.INTEGER)
  id!: number;

  @Column(DataType.STRING)
  address!: string;
}
```

이 와 같은 형식이며, 하나하나 설명을 하면

- `@Table`은 이 클래스가 모델이라고 알려주는 역활이며,
- `Model`은 차후에 이 클래스를 호출을 하여 findOne과 같은 함수를 사용해야하는데 그때 사용을 할 함수들이 있는 클래스이다.
- `@PrimartKey`는 기본키임을 나타내는 어노테이션이다.
- `@AutoIncrement`키의 값이 자동으로 증가하도록 해주는 어노테이션이다.
- `@Column`은 이 필드의 값이 컬럼임을 알려주며, 컬럼의 속성을 정하지도록 도와주는 어노테이션이다.

## 시작하기

```typescript

import { Sequelize } from 'sequelize-typescript';

const sequelize = new Sequelize({
  dialect: 'mariadb',
  database: development.database,
  host: development.host,
  password: development.password,
  logging: development.logging,
  username: development.username,
});

sequelize.addModels([...]);

sequelize
  .sync()
  .then(() => {
    console.log('✓ DB connection success.');
    console.log('  Press CTRL-C to stop\n');
  })
  .catch((err: Error) => {
    console.error(err);
    console.log('✗ DB connection error. Please make sure DB is running.');
    process.exit();
  });
```

위와 같이 작성을 해야하며 이중 development는 sequelzie-cli에서 초기 설정때 만들어진 `config/config.json`파일을 활용한것이다. 이 외에도 `addModels`함수 부분은 추가할 모델을 전부 추가해줘야하는데, 한번에 추가할수 있으나, typescript의 빌드후 파일을 기준으로 해야하여, 그냥 하나하나 추가하는 방식으로 하는것을 추천한다.

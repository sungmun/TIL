# Sequelize 사용법

sequelize는 node기반에서 사용을 하는 ORM(Object-Relaction Mapping)으로 관계형 DB인 MySQL,MaraiaDB,Postgres,SQLite,Microsoft SQL Server을 지원하며, 여기에서는 MySQL과 MaraiaDB만 다룰것이다.

## sequlize-cli

ORM의 사용을 위해서라면 대부분의 ORM에서는 코드 내에서 DB의 Table을 정의하도록 되있다. 이때 여기에서는 sequlize-cli를 통하여 Table을 정의하도록 할것이다

```
yarn add -g sequelize-cli
```

위의 sequelize-cli는 sequelize가 필요한 프로젝트의 기본적인 구조를 잡아주며, sequelize-cli를 통해 Table을 정의를 해주는 경우 프로그램 내부에서 사용이 될 model과 database에서 사용이될 migration이 생성이 된다. 그리고 sequelize의 동기화기능을 사용하는 경우 seed데이터 를 추가해주어 개발중 database의 변경 가능성을 염두할 필요가 없어진다.

프로젝트의 기본적인 구조

```
sequelize init
```

- /
  - config/config.json
  - migrations
  - models/index.js
  - seeders

위와 같이 4개의 폴더에 2개의 파일이 생성이 된다. 이때 생성되는 파일인 config.json파일은 db의 정보를 담아주는 파일이고, models/index.js파일은 sequelize의 나름 중요한 파일이라, 건들일 필요가 없는 파일이다. (변경이 필요한 경우가 있기는 있다.)

## models and migrations

이 폴더에 들어가는 파일은

```bash
sequelize model:generate --name Test --attributes id:num, testValue:string
```

명령어를 이용하면 생성이 가능하며, `--name User`값은 테이블의 이름을 뜻하고, `--attributes id:num,testValues:string`값은 컬럼을 뜻한다.

이를 통해 migrations폴더에 들어가는 파일과 models에 들어가는 파일이 동시에 생성이 된다. 이때, Service로직에서 직접적으로 호출을 하는 부분이 models부분이고, Database에 Table을 구성시 확인을 하는 부분이 migrations 부분이다.

차후에 model에 관계설정을 하는경우 migrations부분에 외래키같은 부분을 따로 추가를 해줘야 한다

**꼭 확인을 해야하며, 확인을 하지 않을시 오류가 날가능성이 높다.**

## seeders

이 폴더에 들어가는 파일은

```bash
sequelize seed:generate --name TestData
```

명령어를 통해 생성이 되며, 추가해야하는 데이터를 생성이 된 파일에 추가를 해주어야 한다.

## sequeilze-cli run

현재까지 만든부분을 기준으로 실행을 하면 models값을 기준으로 테이블이 만들어지므로 sequelize-cli 를 이용하여 database를 마이그레이션을 해주어야한다.

```bash
 sequelize db:migrate
```

이 명령을 통해 migrations파일을 기준으로 테이블이 생성이 되며,

```bash
sequelize db:seed:all
```

이 명령을 통해 테이블에 데이터가 추가된다.

## Sequelize 사용하기

위의 설정을 자신이 만들 DB의 테이블에 맞게 설정을 하면 이제 node를 키고 sequelize를 connect하면 사용이 가능해진다.
connect를 하는 법은 제일 처음 셋팅을 할 때 생성이 됬던, models/index.js파일을 import해주고, sync함수를 실행시켜 주면 된다.

```javascript
import { sequelize } from "/models";
sequelize
  .sync()
  .then(() => {
    console.log("connect success");
  })
  .catch(() => {
    console.error(err);
    console.log("✗ DB connection error. Please make sure DB is running.");
    process.exit();
  });
```

이후 service로직에서 사용이 가능해지며, 좀더 자세한 설명은 [여기](https://velog.io/@cadenzah/sequelize-document-4)를 보면 이해가 가능해질것이다.

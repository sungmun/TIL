# Sequelzie-TypeScript 2

**sequelize-typescript**의 연관관계 맵피에 대하여 설명을 하려고 한다.

우선 sequelize 에서는 연관관계 맵핑을 함수를 이용하여 하였으나, **sequelize-typescript**에서는 typescript에 있는 어노테이션을 이용하여 연관관계를 맵핑해준다.

기존의 관계에서는 외래키를 어느곳에 위치할것인가에 두고 관계의 명칭이 나뉘었는데, sequelize-typescript는 외래키를 어디에 둘 것 아예 필드값을 만들어버리기때문에 실질적으로 사용되는 명칭이 좀 줄었다. (물론 기존의 명칭을 사용을 할 수는 있는것으로 보이기는 한다.)

## @BelongsTo()

```ts
@Table
class 톡 extends Model<톡> {
  @BelongsTo(() => 카카오톡방)
  카카오톡방: 카카오톡방;
}
```

여기에서 톡은 카카오톡에서 메세지 하나를뜻하는데, 이경우 톡은 하나의 카카오 톡 방을 가지기 때문에 **1:1관계**를 뜻하는 BelongsTo연관관계를 사용하였다.

## @BelongsToMany

```ts
@Table
class 유저 extends Model<유저> {
  @BelongsToMany(() => 유저, () => 친구, "userId", "friendId")
  friendList!: User[] | [];
}
@Table
class 친구 extends Model<친구> {
  @ForeignKey(() => 유저)
  userId!: number;

  @ForeignKey(() => 유저)
  friendId!: number;
}
```

위와 같이 N:M관계는 관계를 저장을 해 줄 테이블이 필요하고, 관계를 저장해줄 테이블에 외래키를 이용하여, 값을 저장해줄수 있도록 한다. 그리고 BelongsToMany의 인자값중 첫번째 값은, 현재 테이블과 관계를 맺을 테이블값, 두번째 값은 관계를 저장해줄 테이블값, 세번째값은 관계를 저장해줄 테이블에 현재테이블의 값을 저장할 필드명, 네번째 값은 관계를 저장해줄 태이블에 관계를 맺을 테이블의 값을 저장해줄 필드명이다. 좀 복잡한것같지만 한번 공부해놓으면 그뒤에도 ORM을 사용시 쉽게 이해가 가능하다.

## @HasMany

```ts
@Table
class 카카오톡방 extends Model<카카오톡방> {
  @HasMany(() => 톡)
  톡: 톡[];
}
```

이제 마지막인 1:N관계인데, 카카오톡 방은 다수의 톡을 알고 있어야하므로 1:N관계가 된다. 이때 톡테이블에는 카카오톡방의 외래키가 생성이 되어 있어야한다.

이후의 부분은 컬럼의 상세설정이나 hook을 설정하는 부분인데 이부분은 나도 공부가 부실하여 document를 보고 추가적으로 공부를 해야할것같다. 그외에는 sequezlie-typescript를 직접쓴는 부분은 차후에 포스팅을 할 예정이다.

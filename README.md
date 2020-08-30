# immer 튜토리얼

> 벨로퍼트 리액트를 다루는 기술 12장

```js
import produce from 'immer';
const nextState = produce(originalState, (draft) => {
  draft.something = 2;
});
```

produce는 두가지 매개 변수를 받는데,
첫 번째 매개변수는 수정하고 싶은 state를,
두 번째 매개변수는 상태를 어떻게 업데이트할 지 정의하는 함수를 적는다.

두 번째 함수 내부에서 원하는 값을 변경하면, produce 함수가 불변성 유지를 대신해주면서 새로운 상태를 생성해준다.

## useState의 함수형 업데이트랑 같이 쓰기

```js
const [number, setNumber] = useState(0);
// prevNumbers는 현재 number
const onIncrease = useCallback(
  () => setNumber((prevNumber) => prevNumber + 1),
  []
);
```

immer에서 제공하는 produce 함수를 호출할 때, 첫 번째 매개변수가 함수 형태라면 업데이트 함수를 반환한다.

```js
const update = produce((draft) => {
  draft.value = 2;
});
const originalState = {
  value: 1,
  foo: 'bar',
};
const nextState = update(originalState);
console.log(nextState); // { value: 2, foo: 'bar'}
```

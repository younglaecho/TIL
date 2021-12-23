## immer를 활용한 불변성 유지

객체의 구조가 깊어지면 불변성을 유지하면서 업데이트가 힘들어진다.

#### immer 설치

```sh
$ yarn add immer
```

#### immer 사용법

```react
import produce from 'immer';
const nextState = produce(original, draft => {
  // 바꾸고 싶은 값 바꾸기
  daft.somewhere.deep.inside = 5;
})
```

1. produce라는 함수의 첫 번째 인자로 기존 객체를 넣는다.
2. 두 번째 인자로 바꾸고 싶은 값을  바꾸어주는 함수를 넣는다.

``` react
// 일정관리 앱의 불변서 유지에 immer를 사용해보았다. 
  const onToggle = useCallback(
    id => {
      // setTodos(todos => todos.map(todo => (
      //   todo.id === id ? {...todo, checked: !todo.checked} : todo
      // )))
      setTodos(todos => produce(todos, draft => {
        const todo = draft.find(t => t.id === id);
        todo.checked = !todo.checked;
      }))
    },
    []
  )
```

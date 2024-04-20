## 인터페이스 여러 개

이번엔 AllList.jsx를 타입스크립트로 바꿨다.

코드 일부를 보자.

```typescript
interface Todo {
  id: string;
  text: string;
  completed: boolean;
}

interface AllListProps {
  todo: Todo[];
  onDelete: (id: string) => void;
  onShow: () => void;
  toggleComplete: (id: string) => void;
}

const AllList = ({ todo, onDelete, onShow, toggleComplete }: AllListProps) => {
```

<br>
먼저 여기서 인자로 들어가는 todo는

```typescript
 {todo.map((todos) => (
            <ListContainer key={todos.id}>
              <Btn className={todos.completed ? 'completed' : ''} onClick={() => toggleComplete(todos.id)}>
                <IoMdCheckmarkCircleOutline />
```

이렇게 id도 있고 completed도 있고 그래서 `interface`를 만들었다.

그리고 이제 모든 인자 `interface`를 만들고 todo는 Todo[]라고 한다!

### 1. React.FC

먼저 원래 코드와 타입스크립트를 적용한 코드를 살펴보자

```javascript
import { useState } from 'react';
import { TodoListBtn, FormBackground, WriteBox, TodoInput, TodoLabel, TodoBottomLine } from './AddTodoForm.styles';

const AddTodoForm = ({ onAddTodo }) => {
  const [isCliked, setIsClicked] = useState(false);
  const [inputValue, setInputValue] = useState('');

  const handleBtnClicked = (e) => {
    setIsClicked(!isCliked);
  };

  const handleWriteBox = (e) => {
    e.stopPropagation();
  };

  const handleInputChange = (e) => {
    setInputValue(e.target.value);
  };

  const handleAddTodo = () => {
    onAddTodo(inputValue);
    setIsClicked(!isCliked);
    setInputValue('');
  };

  return (
    <div>
      <TodoListBtn onClick={handleBtnClicked}>
        MORE<br></br>MORE<br></br>MORE
      </TodoListBtn>
      {isCliked && (
        <FormBackground onClick={handleBtnClicked}>
          <WriteBox onSubmit={handleAddTodo} onClick={handleWriteBox}>
            <TodoInput type="text" placeholder="" value={inputValue} onChange={handleInputChange} autoFocus required></TodoInput>
            <TodoLabel>Todo</TodoLabel>
            <TodoBottomLine></TodoBottomLine>
          </WriteBox>
        </FormBackground>
      )}
    </div>
  );
};

export default AddTodoForm;
```

```typescript
import React, { useState } from 'react';
import { TodoListBtn, FormBackground, WriteBox, TodoInput, TodoLabel, TodoBottomLine } from './AddTodoForm.styles';

interface AddTodoFormProps {
  onAddTodo: (todoText: string) => void;
}

const AddTodoForm: React.FC<AddTodoFormProps> = ({ onAddTodo }) => {
  const [isCliked, setIsClicked] = useState<boolean>(false);
  const [inputValue, setInputValue] = useState<string>('');

  const handleBtnClicked = (): void => {
    setIsClicked(!isCliked);
  };

  const handleWriteBox = (e: React.FormEvent<HTMLFormElement>): void => {
    e.stopPropagation();
  };

  const handleInputChange = (e: React.ChangeEvent<HTMLInputElement>): void => {
    setInputValue(e.target.value);
  };

  const handleAddTodo = (): void => {
    onAddTodo(inputValue);
    setIsClicked(!isCliked);
    setInputValue('');
  };

  return (
    <div>
      <TodoListBtn onClick={handleBtnClicked}>
        MORE<br></br>MORE<br></br>MORE
      </TodoListBtn>
      {isCliked && (
        <FormBackground onClick={handleBtnClicked}>
          <WriteBox onSubmit={handleAddTodo} onClick={handleWriteBox}>
            <TodoInput type="text" placeholder="" value={inputValue} onChange={handleInputChange} autoFocus required></TodoInput>
            <TodoLabel>Todo</TodoLabel>
            <TodoBottomLine></TodoBottomLine>
          </WriteBox>
        </FormBackground>
      )}
    </div>
  );
};

export default AddTodoForm;
```

<br>
달라진 점을 살펴보자! <br>
먼저 이번 주제인 `React.FC` 부분을 보자.

<br>

```typescript
// 원래 코드
const AddTodoForm = ({ onAddTodo }) => {
  const [isCliked, setIsClicked] = useState(false);
  const [inputValue, setInputValue] = useState('');

// 타입스크립트 적용
  const AddTodoForm: React.FC<AddTodoFormProps> = ({ onAddTodo }) => {
  const [isCliked, setIsClicked] = useState<boolean>(false);
  const [inputValue, setInputValue] = useState<string>('');
```

FC는 FunctionComponent 타입의 줄임말로 리액트와 타입스크립트를 조합해서 사용할 때 사용하는 타입이다. 함수형 컴포넌트 사용 시 타입 선언에 쓸 수 있도로 리액트에서 제공하는 타입이다.

인자의 타입인 `AddTodoFormProps`를 props 옆에 붙이지 않고 `React.Fc` 옆에 붙였다.

약간 `as`느낌 처럼 뭔가뭔가 그렇다! 그래서 찾아보니까 후술할 단점들 때문에 사용을 지양한다고 한다, 이제 단점을 알아보자!

- **children prop이 옵셔널로 포함되어 props 타입이 명확하지 않다.** <br>
  FC는 `children`이 옵셔널 형태로 들어가있어서 props의 타입이 명확하지 않다. 예를 들어 `children`이 무조건 있어야 할 경우도 있고 들어가면 안되는 경우도 있을 것이다. 하지만 `React.FC`를 사용하면 이에 대한 처리를 제대로 하지 못한다. 물론 이러한 점을 해결하기 위해 리액트에서 제공하는 방식도 있는데 솔직히 타입 선언을 제대로 하는 것이 더 보기 좋다.

- **타입스크립트의 제네릭 문법을 지원하지 않는다.**<br>

```typescript
type GenericComponentProps<T> = {
  prop: T;
  callback: (t: T) => void;
};

const GenericComponent = <T>(props: GenericComponentProps<T>) => {
  /*...*/
};
```

이처럼 제네릭 문법을 사용해서 props를 사용할 경우 컴포넌트에 값을 전달할 수 없다.

- **defaultProps 속성이 적용되지 않는다.**
  defaultProps를 사용해서 props의 초기값을 설정해도 값을 인식하지 못한다.

<br>

---

때문에 React.FC는 지양한다고 한다.

그래서 이렇게 쓰는 대신 props 옆에 타입을 정의해주면 된다.

```typescript
// FC 사용 코드
const AddTodoForm: React.FC<AddTodoFormProps> = ({ onAddTodo }) => {
  const [isCliked, setIsClicked] = useState<boolean>(false);
  const [inputValue, setInputValue] = useState<string>('');

// 바꾼 코드
const AddTodoForm = ({ onAddTodo }: AddTodoFormProps) => {
  const [isCliked, setIsClicked] = useState<boolean>(false);
  const [inputValue, setInputValue] = useState<string>('');
```

이렇게 props 옆에 타입을 직접 지정해줬다!

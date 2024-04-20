## ReactNode

```typescript
// 원래 코드
import React from 'react';
import { Container } from './TodolistContainer.style';

const TodolistContainer = ({ children }) => {
  const childrenCount = React.Children.count(children);

// 바꾼 코드
import React, { ReactNode } from 'react';
import { Container } from './TodolistContainer.style';

interface TodolistContainerProps {
  children: ReactNode;
}

const TodolistContainer = ({ children }: TodolistContainerProps) => {
  const childrenCount = React.Children.count(children);
```

이 코드는 자식 요소를 처리하기 위해 리액트에서 제공하는 `children`이라는 prop를 통해 처리했다.

`ReactNode`는 `children` 속성의 타입으로 가장 많이 사용하는 타입인데 `jsx` 내에서 사용할 수 있는 모든 요소인 string, null, undefined 등을 포함한 가장 넓은 범위를 갖는 타입이다.

이걸 사용하려면 먼저 `import`를 하고 사용해야 한다!

<br>

### **번외**

- **React.ReactElement** <br>
  `createElement` 함수를 통해 생성된 객체의 타입이다.
  `ReactNode`와 달리 원시타입을 허용하지 않고 완성된 jsx 요소만을 허용한다.

- **React.Element** <br>
  얘는 컴포넌트, 원시 타입 리터럴을 허용하는 타입이다.

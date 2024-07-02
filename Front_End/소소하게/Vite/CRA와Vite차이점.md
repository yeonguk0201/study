CRA로 리액트 프로젝트를 했었는데 이번엔 Vite를 사용해 보았다.

그러니까 처음부터 뭐가 달랐는데 그 중 한 가지는 styled-components를 사용하는데 자동완성이 안되는 것이다!

찾아보니까 Vite는 CRA와 다르게 개발자가 명시적으로 패키지와 설정을 관리해야 하는 부분이 많아서 그런 것이다. CRA를 사용하면 TypeScript와 관련된 설정 및 패키지(@type/react) 이런 것들이 자동으로 포함되는 반면, Vite는 가볍고 빠른 설정때문에 TypeScript와 관련된 타입 정의 파일들을 직접 설치해야 한다.

그렇기 때문에 CRA와 다르게 Vite는 빠르지만 필요한 패키지들은 따로 알아서 챙겨야 한다. 예를 들어

```
npm install @types/styled-components --save-dev
```

이런 것들!

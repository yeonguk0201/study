## Install

### 시작하기 전 설정

Three.js를 설치할건데 vite를 사용할 것이다. <br>
왜 vite를 사용하느냐! Three.js는 3D를 다루기 때문에 속도면에서 중요할 텐데 vite가 속도가 빠르기 때문에 vite를 사용했다.

그럼 이제 cmd나 git bash에 차례대로 쓰면 된다.

```
npm create vite@latest


그리고 폴더 이름을 정하고 사용할 프레임 워크랑 옵션을 정할 수 있는데 나는 Vanilla와 TypeScript로 정했다.

그리고 vscode열어서 터미널 열고 npm i랑 npm run dev하면 잘 나온다.
```

그러면 이제 필요없는 파일 지우고 만들면 된다.

https://sbcode.net/threejs/create-threejs-boilerplate/

그리고 여기 나와있는 코드를 붙여 넣었다.

---

### 설치하기

위 과정까지 다 했다면 main.ts에 `three 모듈 또는 해당 형식 선언을 찾을 수 없습니다.` 라는 오류가 생길 것이다. 이건 `three`를 설치하지 않았기 때문으로

```
npm i three --save-dev
```

를 통해 설치해주자.

<br>

그리고 타입스크립트를 사용할 것이기 때문에 아래 문구도 넣어준다.

```
npm i @types/three --save-dev
```

<br>
처음 설치한 three는 Three.js 라이브러리 자체를 설치하는 것이고, 다음 설치한 @types.three는 TypeScript 정의 파일로 타입스크립트로 Three.js를 타입스크립트와 사용할 때 타입 정보를 제공하는 것이다. 이를 통해 IDE의 자동완성 기능을 사용할 수 있다.

<br>

IDE는 통합 개발 환경을 의미하는데 쉽게 말하면 Vscode에서 자동완성 기능을 지원하는데 그런 기능을 의미한다.

## 로딩 컴포넌트

Next에서 로딩 컴포넌트를 만드는 방법은 간단하다.

원하는 페이지 폴더에 `loading.tsx` 파일을 만들어 주고 컴포넌트를 만들면 끝!

```typescript
export default function Loading() {
  return <h2>Loading...</h2>;
}
```

이렇게만 만들어도 로딩 시에 이 컴포넌트가 등장한다.

지연시간을 만들어서 로딩 화면을 확인해 보자.

```typescript
await new Promise((resolve) => setTimeout(resolve, 1000));
```

공통된 로딩 컴포넌트를 원하면 공통된 layout 파일이랑 같은 위치에 넣으면 된다.

<br>

Next는 layout과 loading 컴포넌트를 먼저 주고, 완료되면 loading 컴포넌트가 교체된다.

<br>

```typescript
export const metadata = {
  title: 'Home',
};

const URL = 'https://nomad-movies.nomadcoders.workers.dev/movies';

async function getMovies() {
  await new Promise((resolve) => setTimeout(resolve, 1000));
  return fetch(URL).then((response) => response.json());
}

export default async function HomePage() {
  const movies = await getMovies();
  return <div>{JSON.stringify(movies)}</div>;
}
```

이 코드에서 HomePage가 async인 이유는 컴포넌트를 await해야하기 때문이다.
그리고 로딩이 끝나면 await된 컴포넌트를 보낸다.

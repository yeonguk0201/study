### Client-Side에서 fetch

이번엔 따로 라이브러리를 쓰지 않고 오직 react만을 사용해서 data를 fetching하는 경우를 리마인드 해봤다.

```typescript
'use client';

import { useEffect, useState } from 'react';

export default function page() {
  const [movies, setMovies] = useState([]);
  const [isLoading, setIsLoading] = useState(true);
  const getMovies = async () => {
    const response = await fetch('https://nomad-movies.nomadcoders.workers.dev/movies');
    const json = await response.json();
    setMovies(json);
    setIsLoading(false);
  };

  useEffect(() => {
    getMovies();
  }, []);
  return <div>{isLoading ? 'Loading...' : JSON.stringify(movies)}</div>;
}
```

이렇게 `useState`를 사용해서 data를 fetch했었는데 Next에서 `useState`를 사용하면 `use client`를 써야 하기에 `metadata`를 사용할 수 없게 되었다.

그런데 이렇게 fetch하면 브라우저에서 다 보여지기 때문에 비밀들을 넣을 수 없다. 그리고 로딩 상태도 직접 구현했고 api도 신경써야하고

반면 `server component`에서 fetch한다는 것은 `useEffect, useState`를 쓰지 않아도 된다.

<br>

---

#### Server Component

server component는 말 그대로 서버에서 렌더링 되는 컴포넌트를 말한다.

서버에서 렌더링 되기 때문에 클라이언트 측에서 초기 로딩 시간을 줄일 수 있고 미리 렌더링 되기 때문에 SEO에 유리하다.

또한 서버에서 데이터를 직접 fetching 할 수 있기 때문에 클라이언트 쪽에서 직접 데이터를 로드할 필요가 없고, 클라이언트 쪽에서 실행되지 않기 때문에 민감한 데이터나 환경변수를 안전하게 다룰 수 있다.

일반적으로 Next같은 프레임워크를 사용해서 서버 컴포넌트를 사용하는 것이 일반적이다.

<br>

단점

- 클라이언트와 서버 컴포넌트를 분리해 관리해야 하기 때문에 복잡성이 증가
- 서버가 필요하기 때문에 정적 사이트에선 사용할 수 없다.
- 클라이언트 쪽에서 상호작용할 수 없기 때문에 사용자와 인터렉션이 필요한 부분은 클라이언트 컴포넌트를 사용해야 한다.

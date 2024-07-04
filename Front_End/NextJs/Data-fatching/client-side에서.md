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

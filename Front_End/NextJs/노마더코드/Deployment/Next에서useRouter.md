Next에서 useRouter을 썼다.

```typescript
import Link from 'next/link';
import styles from '../styles/movie.module.css';
import { useRouter } from 'next/router';

interface MovieProps {
  title: string;
  id: string;
  poster_path: string;
}

export default function Movie({ title, id, poster_path }: MovieProps) {
  const router = useRouter();
  const onClick = () => {
    router.push(`/movies/${id}`);
  };
  return (
    <div className={styles.movie}>
      <img src={poster_path} alt={title} onClick={onClick} />
      <Link href={`/movies/${id}`}>{title}</Link>
    </div>
  );
}
```

먼저 이렇게 했다. `useRouter`을 통해 클릭 시 동작할 함수를 만들어서 onClick이벤트 시 사용하게 하려고 했다.

코드를 보면 import next/router 이라고 나와있는데 이러면 오류가 생긴다.

```
Use next/navigation instead.
```

그래서 바꿔주지만 아직도 오류가 있다!

```
You're importing a component that needs useRouter. It only works in a Client Component but none of its parents are marked with "use client", so they're Server Components by default.
```

바로 `useRouter`는 오직 `client` 에서만 사용 가능하다는 것이다. 그도 그럴 것이 server component는 상호작용이 불가능하다고 배웠는데 onClick 이벤트는 상호작용이기 때문이다. 그러므로 맨 위에 `use client`를 추가해주도록 하자.

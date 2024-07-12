## 에러 핸들링

이번엔 에러 핸들링에 대해 알아보자.

먼저 해당 폴더에 가서 `error.tsx`를 만들자.

그리고 일부러 에러를 일으킨 후

```typescript
async function getVideo(id: string) {
  await new Promise((resolve) => setTimeout(resolve, 3000));
  console.log(`Fetching 중: ${Date.now()}`);
  throw new Error('something broke');
  // const response = await fetch(`${API_URL}/${id}/videos`);
  // return response.json();
}
```

error.tsx파일을 작성한다.

```typescript
'use client';

export default function ErrorOMG() {
  return <h1>error something</h1>;
}
```

여기서 중요한 점은 `error.tsx`는 `useclient`가 꼭! 있어야 한다는 점이다.

이렇게 하면 해당 라우트 안에선 에러가 발생하면 error컴포넌트가 나오게 된다.

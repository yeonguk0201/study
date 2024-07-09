## Suspense

```typescript
export default async function MovieDetail({ params: { id } }: { params: { id: string } }) {
  const [movie, videos] = await Promise.all([getMovie(id), getVideo(id)]);
  return (
    <div>
      <h1>{movie.title}</h1>
      <h2>{videos.title}</h2>
    </div>
  );
}
```

이렇게 하면 `Promise.all`때문에 비동기적으로 실행되지만 UI는 movie와 videos가 완료되어야 하기 때문에 둘 다 기다려야 한다.

이번엔 movie와 videos 각각 따로 나눠서 UI를 표시하는 방법을 알아볼 것이다.

<br>

---

<br>

Promise에 있는 각각의 함수가 준비되면 이에 관련된 UI가 바로 나오게 할 것이다.

먼저 파일을 새로 만들어 준다. `components 폴더`에 `movie-vieos라는 파일`을 만들었다.

그리고 이 파일에 page 파일에 있던 `getVideo`함수를 넣어준다. 왜냐하면 지금 이 파일엔 video와 관련된 UI만 가질 것이기 때문이다.

그리고 export했다.

```typescript
export default async function MovieVideos({ id }: { id: string }) {
  const videos = await getVideo(id);
  return <h6>{JSON.stringify(videos)}</h6>;
}
```

그럼 이거랑 똑같이 page에 있던 나머지 함수도 components 폴더에 파일 만들어서 만들어 주자.

이제 page 코드를 수정하자.

```typescript
export default async function MovieDetail({ params: { id } }: { params: { id: string } }) {
  return (
    <div>
      <MovieInfo id={id} />
      <MovieVideos id={id} />
    </div>
  );
}
```

근데 여기서 끝이 아니다. 이번 장의 핵심은 Suspense!

React에서 제공하는 Suspense 컴포넌트가 있는데 Suspense에는 fallback props이 있다. 이건 component가 await되는 동안 표시할 메세지를 render할 수 있게 해준다.

```typescript
export default async function MovieDetail({ params: { id } }: { params: { id: string } }) {
  return (
    <div>
      <Suspense fallback={<h1>Loading Movie Info</h1>}>
        <MovieInfo id={id} />
      </Suspense>
      <Suspense fallback={<h1>Loading Movie Videos</h1>}>
        <MovieVideos id={id} />
      </Suspense>
    </div>
  );
}
```

> 요약 <br>
> 처음엔 page 파일에서 두 가지를 fetch해야 했다. 하지만 둘 다 기다려야 하는 단점이 있었고 그걸 해결하기 위해서 components를 따로 만들었다. 각 components 들은 각자의 것들만 fetch 했고 둘 다 async에 await 했다.
> 그 뒤 page파일을 정리하는데 Suspense를 사용했고 Suspense가 데이터를 fetch하기 위해 이 안에 있는 components를 await 하고 fetch중에는 fallback 안의 요소를 render한다. 끝나면 안에 있는 UI를 render한다.

이렇게 하면 데이터가 준비되는 되로 바로바로 UI를 받을 수 있어서 모든 fetch를 기다릴 필요가 없다!

이렇게 되면 이 page파일은 await하는 게 없기 때문에 같이 있는 loading.tsx가 필요 없어 진다.

## use client란

**hydration**이란 server side render된 초기 HTML을 사용자가 얻게되면 그 위에 React application이나 next가 얹어지는게 hydration이다.

이러한 hydration은 모든 component에 발생하는 것은 아니다. SSR은 모든 component에 적용되지만 client에서 interactive하게 만들어질 components는 오직 `use client`지시어를 맨 위에 가진 components 뿐이다. `use client`는 단지 client에서만 render된다는 뜻이 아니다. backend에서 render되고 frontend에서 hydrate 및 interactive하게 됨을 의미한다.

use client를 사용하지 않은 다른 모든 components들은 server components다.
사용자는 use client가 있는 components의 JavaScript만 다운 받는다.

즉, 모든 components들은 backend에서 HTML로 미리 render되는데 use client를 통해 어떤 components들이 JavaScript가 필요한 지, interactive할 것인지 선택할 수 있다.

이때, server components안에 client components를 가질 수 있을까?

답은 가질 수 있다. 하지만 client components 안에 server components를 가질 수는 없다. server components안에 client components를 넣는 것은 가능하지만 일단 client components가 되면 그 안의 components들은 모두 client components가 되기 때문이다.

`server components`의 장점은 server에서만 코드가 돌아가기 때문에 여기서 DB랑 통신해도 되고 API 키를 넣어도 된다. 왜냐하면 오직 server에서만 돌아가기 때문이다.

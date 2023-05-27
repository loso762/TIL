## 1. 파일 기반 라우팅이란?
react에서는 react-router-dom 패키지를 설치하고 App.js에서 라우트 코드를 직접 작성하여 라우팅을 구현하지만, Next.js는 폴더 구조를 통해 라우팅돼야 하는 파일들을 알아서 추론한다.
넥스트는 pages라는 이름의 폴더 안에 화면 파일을 만들면 알아서 라우팅한다. 아래의 구조를 보면 어떻게 path가 생성되는지 알 수 있다.
동적 라우팅은 대괄호([ ])를 써서 하면 된다.

```
/pages
 └ index.js -> my-domain.com/
 └ about.js -> my-domain.com/about
 └ /products
   └ index.js -> my-domain.com/products
   └ [id].js -> my-domain.com/products/1
```
<br><br>
## 2. 정적 페이지 라우팅(Named/Static page routing)
말 그대로 이름을 부여받은 정적 페이지를 라우팅하는 것으로 원하는 위치(path)에 이름이 고정된 파일을 생성하면 된다.

<br><br>
## 3. 중첩 라우팅(Nested routing)
중첩 라우팅은 path를 단계별로 거슬러 오르내리도록 라우팅하는 것이다. 개발자 입장에선 각 화면 별로 유사성이 있는 페이지끼리 분리해두는 것이라고 볼 수 있다.
원하는 위치에 폴더를 만들고 그 안에 파일을 생성하면 된다.
```
/pages
 └ index.js -> my-domain.com/
 └ about.js -> my-domain.com/about
```

<br><br>
## 4. 동적 라우팅(Dynamic routing)

1) 동적 라우팅이란?
동적 라우팅은 부여받은 path값에 따라 동적으로 라우팅하는 것이다. 개발자 입장에선 화면 구조는 똑같은데 다른 데이터를 받아올 시에 귀찮게 파일을 여러개 만들지 않고 한 파일을 만들어 데이터만 다르게 구성할 때 주로 사용한다.
파일을 생성하고 파일명을 지을 때 대괄호로 감싸면 된다. ex) [id].js
만약 아래와 같은 구조일 경우 my-domain.com/products/list 입력하면 [id].js가 아닌 list.js 파일을 불러온다. 동적 라우팅 시에 같은 하위 폴더 내에 이미 static으로 불러오는 파일이 있으면 그걸 먼저 불러오고, 없으면 동적 페이지를 불러온다.
```
/pages
└ index.js -> my-domain.com/
└ about.js -> my-domain.com/about
└ /products
   └ list.js -> my-domain.com/products/list
   └ [id].js -> my-domain.com/products/1
```

2) useRouter
동적 라우팅을 할 때는 넥스트에서 기본으로 제공해주는 라이브러리인 useRouter를 사용한다.
pathname: 경로를 알려주는 프로퍼티
query: 동적 라우팅 시 동적 경로값 알려주는 프로퍼티

```
import { useRouter } from "next/router";

export default function Project() {
  const router = useRouter();
  console.log(router.pathname);  // /portfolio/[projectId]
  console.log(router.query);  // Object -> projectId: "1"

  return (
    <div>
      <h1>Project</h1>
    </div>
  );
}
```

3) 중첩 동적 라우팅
동적 라우팅은 파일뿐만 아니라 폴더에도 적용할 수 있다. 폴더를 생성할 때 파일과 마찬가지로 대괄호([])로 감싸면 된다.

```
// /pages > /client > /[name] > [ClientProject].js
import { useRouter } from "next/router";

export default function Project() {
  const router = useRouter();
  console.log(router.query);  // Object -> ClientProject: "1" / name: "Max"

  return (
    <div>
      <h1>Client</h1>
    </div>
  );
}
```

4) Catch-All 라우팅
Catch-All 라우트 기능을 쓰면 이 파일 밑으로 중첩이 몇번을 타고 내려가든 간에 이 파일로 귀결(?)된다.
JS의 spread operator처럼 대괄호([]) 안에 ...을 써서 사용하면 된다. ex) [...slug].js
카테고리와 제품이 많은 사이트에서 사용하기 좋다.

```
// /pages > /blog > [...slug].js
// http://localhost:3000/blog/221004/post1
import { useRouter } from "next/router";

export default function Post() {
  const router = useRouter();
  console.log(router.query);  // Object -> slug: (2) ['221004', 'post1'] // 쿼리값이 배열로 나타난다.

  return (
    <div>
      <h1>Post</h1>
    </div>
  );
}
```

<br><br>
## 5. Link 컴포넌트

1) Link 컴포넌트 사용법
Link 컴포넌트를 호출한 후 href 속성에 path를 지정해주면 된다.

```
import Link from "next/link";

export default function Home() {
  return (
    <div>
      <h1>Home</h1>
      <ul>
        <li>
          <Link href="/portfolio">Portfolio</Link>
        </li>
        <li>
          <Link href="/client">Client</Link>
        </li>
      </ul>
    </div>
  );
}
```

2) Link 컴포넌트 동적 라우팅 사용법
동적으로 변하는 데이터를 map() 메소드를 이용해 length만큼 생성하고, path를 동적으로 부여하면 된다.

```
import Link from "next/link";

export default function Client() {
  // 고객 리스트
  const clients = [
    { id: 1, name: "Max" },
    { id: 2, name: "Anna" },
    { id: 3, name: "Tom" },
  ];

  return (
    <div>
      <h1>Client</h1>
      <ul>
        {clients.map((client) => (
          <li key={client.id}>
            <Link href={`/client/${client.id}_${client.name}`}>
              {client.name}
            </Link>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

3) Link의 href 속성 다르게 주는 방법
href를 문자열과 변수의 조합말고 객체로 주는 방법도 있다. 아래의 코드는 위와 똑같이 작동한다.

```
import Link from "next/link";

export default function Client() {
  // 고객 리스트
  const clients = [
    { id: 1, name: "Max" },
    { id: 2, name: "Anna" },
    { id: 3, name: "Tom" },
  ];

  return (
    <div>
      <h1>Client</h1>
      <ul>
        {clients.map((client) => (
          <li key={client.id}>
            <Link
              href={{
                pathname: "/client/[id]_[ClientName]",
                query: { id: client.id, ClientName: client.name },
              }}
            >
              {client.name}
            </Link>
          </li>
        ))}
      </ul>
    </div>
  );
}
```

6. router.push
router.push는 페이지 이동시켜주는 메소드이다. Link와 마찬가지로 객체로도 path 구성이 가능하다.

```
import Link from "next/link";
import { useRouter } from "next/router";

export default function Client() {
  const router = useRouter();

  // 고객 리스트
  const clients = [
    { id: 1, name: "Max" },
    { id: 2, name: "Anna" },
    { id: 3, name: "Tom" },
  ];

  function ClientProjectPage(e) {
    const { id, name } = e.target;
    router.push(`/client/${id}_${name}`);
  }

  return (
    <div>
      <h1>Client</h1>
      <ul>
        {clients.map((client) => (
          <button
            key={client.id}
            onClick={ClientProjectPage}
            id={client.id}
            name={client.name}
          >
            {client.name}
          </button>
        ))}
      </ul>
    </div>
  );
}
```

7. 404 페이지 만들기
존재하지 않는 path를 요청할 시 404 페이지가 뜨게 되는데 이 404 페이지를 커스텀할 수 있다.
pages 폴더 내 제일 상단에 404.js 파일을 생성하면 알아서 없는 페이지를 부르면 이 파일을 보여준다.

```
// pages/404.js
import Link from "next/link";

export default function NotFoundPage() {
  return (
    <div>
      <h1>Page no found</h1>
      <ul>
        <li>
          <Link href="/">Go home</Link>
        </li>
      </ul>
    </div>
  );
}
```

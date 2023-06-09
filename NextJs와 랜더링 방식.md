> **SPA** : 웹사이트에서 새로운 페이지 링크를 클릭 시 서버에 새로운 페이지를 요청해서 새로운 html을 받아와서 페이지를 리로딩 하는 것이 아니라 하나의 페이지 어플리케이션 내에서 필요한 부분만 즉각적으로 업데이트 해주는 페이지 (Client Side Rendering)
⇒ 페이지 url 변경 시 리액트 라우터가 필요하다

> **CSR **: 브라우저에 표기하기 위한 모든 코드들을 클라이언트 측에서 다운로드 받아서 클라이언트 측에서 코드를 실행해서 표기하는 것


<br><br>
## CSR의 문제점

페이지 로딩시간 (TTV)이 길다.FCP(First Contentful Paint)

1. 자바스크립트 활성화가 필수.
2. SEO 최적화가 힘들다. ⇒ 검색 크롤러가 빈페이지를 보기 때문에 어떤 컨텐츠가 들어있는지 모른다.
3. 클라이언트에서 모든 코드를 받아와서 실행하기 때문에 보안에 취약하다. ⇒ 서버에서 필요한 키 같은 요소들이 클라이언트에게 노출된다.
4. CDN(Content Delivery Network)에 캐시가 안된다.
- CDN : 서버가 사용자와 멀리 있을 때 사용자의 근처에 있는 네트워크(CDN)에 데이터를 저장하면 매번 멀리 있는 서버에 데이터를 요청할 필요 없이 CDN에 캐싱된 데이터를 가져와 쓸 수 있다.

⇒ 이런 문제점을 해결 하기 위해 나온게 SSG, SSR

<br><br>
## Next.Js의 장점

1. full-stack 으로 만들 수 있다
2. file-based routing
3. SEO 최적화 솔루션 제공
4. Server Side Rendering과 Hybrid Rendering 가능하다.

<br><br>
## Static Site Generation (SSG)

1. 렌더링 하는 주체자가 서버 ⇒ 빌드할 때 랜더링한다.
2. 클라이언트에서 서버에 요청을 하면 서버측에 미리 만들어진 html 파일을 보내주고 클라이언트 측에서는 받아온 html을 표기만 해주면 된다.
3. SSG의 장점
    - 페이지 로딩시간이 빠르다.
    - 자바스크립트가 필요없다.
    - SEO 최적화가 좋다.
    - 보안이 좋다.
    - CDN에 캐시가 된다.
4. 단점
    - 데이터가 정적이다. (데이터가 가변적으로 바뀌는 사이트에서 좋지 않음)
    - 빌드할 때 랜더링이 되기 때문에 사용자별 정보 제공이 어렵다.

⇒ 이러한 문제점을 해결하기 위해 ISR, SSR 등장

<br><br>
## Incremental Static Regeneration (ISR)

1. 기본적으로 SSG와 동일한 원리, 정해진 주기마다 페이지를 렌더링 해준다.
2. 주기적인 데이터이지만 실시간 데이터는 아니다.
3. 사용자별 정보 제공이 어렵다.

<br><br>
## Server Side Rendering (SSR)

1. 렌더링하는 주체가 서버이며 클라이언트가 요청시 렌더링 한다.
2. 장점
    - 페이지 로딩 시간이 빠름
    - SEO 최적화가 좋음
    - 보안이 뛰어남
    - 실시간 데이터 사용
    - 사용자별 필요한 데이터를 사용
3. 문제점
    - 비교적 느릴 수 있고, 서버에 과부하가 걸릴 수 있음
    - CDN에 캐시가 안됨

<br><br>
## Hybrid Web App
성능을 높이기 위해 페이지별로 각기 다른 렌더링 방식을 혼합

![](https://velog.velcdn.com/images/loso762/post/32c9966b-d9ef-448d-8e59-5bb561e76fc9/image.png)

<br><br>
## 렌더링 방식 결정 트리
![](https://velog.velcdn.com/images/loso762/post/10d3c585-2803-459a-adde-f668eef3fed9/image.png)

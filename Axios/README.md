# Axios

## Axios란 ?

- 브라우저, Node.js를 위한 Promise API를 활용하는 HTTP 비동기 통신이다.
- 즉, 백엔드와 프론트엔드 통신을 쉽게 하기 위해 Ajax와 더불어 사용한다.

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/16ddb0fb-24df-47b6-afd7-1b5819648e7e/Untitled.png)

## Axios 특징

- Promise(ES6) API 사용
- HTTP 요청과 응답을 JSON 형태로 자동 변경

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/c1b8ceeb-dc4d-41df-ba7d-906c89f0cad5/Untitled.png)

## Axios 인스턴스화 하는 이유

- 중복된 부분을 계속 입력하지 않아도 되기 때문이다.
- Get Movie By Latest
  - [`https://api.themoviedb.org/3`](https://api.themoviedb.org/3)/movie/latest?`api_key=<<api_key>`>&`language=en-US`
- Get NetflixOriginals
  - [`https://api.themoviedb.org/3`](https://api.themoviedb.org/3)//discover/tv?with_network=213?`api_key=<<api_key>>`&`language=en-US`

```jsx
// axios.js

import axios from "axios";

const instance = axios.create({
  baseURL: "https://api.themoviedb.org/3",
  params: {
    api_key: "<YOUR_API_KEY>",
    language: "ko-KR",
  },
});

export default instance;
```

```jsx
// request.js
const request = {
  fetchNowPlaying: "/movie/now_playing",
  fetchNetflixOriginals: "/discover/tv?with_network=213",
  fetchTrending: "/trending/all/week",
  fetchTopRated: "/movie/top_rated",
  fetchActionMovies: "/discover/movie?with_genres=28",
  fetchComedyMovies: "/discover/movie?with_genres=35",
  fetchHorrorMovies: "/discover/movie?with_genres=27",
  fetchRomanceMovies: "/discover/movie?with_genres=10749",
  fetchDocumentaries: "/discover/movie?with_genres=99",
};

export default request;
```

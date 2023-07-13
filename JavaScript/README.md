## 옵셔널 체이닝 연산자 (`?.`)

### 옵셔널 체이닝이 필요한 이유

- 옵셔널 체이닝 `?.` 을 사용하면 프로퍼티가 없는 중첩 객체를 에러 없이 안전하게 접근할 수 있다.
- 아래 코드처럼 user안에 없는 프로퍼티에 접근하고자 한다면 에러가 날 것이다.
  ```jsx
  let user = {};
  alert(user.address.street); // Uncaught TypeError: Cannot read properties of undefined (reading 'street')
  ```
- 이를 해결하기 위해서 예전에는 `&&` 를 사용해서 실제 해당 객체나 프로퍼티가 있는 지 확인했다.
  ```jsx
  let user = {};
  alert(user && user.address && user.address.street); //undefined, 에러 발생 X
  ```

<aside>
💡 그러나 ! 너무 코드가 길어진다. 이 때문에 등장한 것이 옵셔널 체이닝 연산자

</aside>

### 옵셔널 체이닝의 등장

- `?.` 은 `?.` ’앞’의 평가 대상이 undefined나 null이면 평가를 멈추고 undefined를 반환한다.

<aside>
💡 **주의 !**

**옵셔널 체이닝을 남용하지 마세요.**

`?.`는 존재하지 않아도 괜찮은 대상에만 사용해야 합니다.

사용자 주소를 다루는 위 예시에서 논리상 `user`는 반드시 있어야 하는데 `address`는 필수값이 아닙니다. 그러니 `user.address?.street`를 사용하는 것이 바람직합니다.

실수로 인해 `user`에 값을 할당하지 않았다면 바로 알아낼 수 있도록 해야 합니다. 그렇지 않으면 에러를 조기에 발견하지 못하고 디버깅이 어려워집니다.

</aside>

### ?.() 와 ?.[]

- ?. 은 연산자가 아니다. 때문에 ?.은 함수나 대괄호와 함께 동작하는 특별한 문법 구조체이다.
- 아래 코드를 통해 ?.( )를 어떻게 쓸 수 있는 지 보자
  ```jsx
  let user1 = {
    admin() {
      alert("어드민 계정입니다");
    },
  };
  let user2 = {};

  user1.admin?.(); // 어드민 계정입니다.
  user2.admin?.(); // undefined
  ```
- ?.[ ]를 사용해 객체 프로퍼티에 접근할 수 있다.
  ```jsx
  let user1 = {
    firstName: "Violet",
  };

  let user2 = {};

  let key = "firstName";
  alert(user1?.[key]); // Violet
  alert(user2?.[key]); // undefined
  alert(user1?.[key]?.something?.not?.existing); // undefined
  ```
  ### 요약
  옵셔널 체이닝 문법 `?.`은 세 가지 형태로 사용할 수 있다.
  1. `obj?.prop` – `obj`가 존재하면 `obj.prop`을 반환하고, 그렇지 않으면 `undefined`를 반환
  2. `obj?.[prop]` – `obj`가 존재하면 `obj[prop]`을 반환하고, 그렇지 않으면 `undefined`를 반환
  3. `obj?.method()` – `obj`가 존재하면 `obj.method()`를 호출하고, 그렇지 않으면 `undefined`를 반환

## 객체 분해 할당 (Object Destructuring Assignment)

```jsx
const { data: movieDetail } = await axios.get(`movie/${movieId}`, {
  params: { append_to_response: "videos" },
});
```

- 이 코드를 보면 `movie/${movieId}`, {params: { append_to_response: "videos" )에 대해서 video 정보를 가져오는데, 이 data 값을 movieDetail이라는 변수에 넣어주는 것이다.

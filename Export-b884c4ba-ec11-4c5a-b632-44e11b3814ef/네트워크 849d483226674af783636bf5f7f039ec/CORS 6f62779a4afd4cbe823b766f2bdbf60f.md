# CORS

# CORS는 무엇인가

![https://blog.kakaocdn.net/dn/cjX54W/btrABKbqTNU/Q5kpaFkndu6YmrbefbAXP1/img.png](https://blog.kakaocdn.net/dn/cjX54W/btrABKbqTNU/Q5kpaFkndu6YmrbefbAXP1/img.png)

먼저 CORS를 알기 이전에, SOP에 대해 알아보자.SOP(Same Origin Policy)는 다른 출처의 리소스를 사용하는 것을 제한하는 보안 방식이다.

브라우저에서는 보안적인 이유로 `cross-origin` HTTP 요청들을 제한한다. 그래서 `cross-origin` 요청을 하려면 서버의 동의가 필요한데, 만약 서버가 동의한다면 브라우저에서는 요청을 허락하고, 동의하지 않는다면 브라우저에서 거절하고 오류메시지가 뜬다.

이러한 허락을 구하고 거절하는 메커니즘을 HTTP-header를 이용해서 가능한데, 이를 CORS(Cross-Origin Resource Sharing)라고 한다.

그래서 브라우저에서 `cross-origin` 요청을 안전하게 할 수 있도록 하는 메커니즘이다.

![[https://beomy.github.io/tech/browser/cors/](https://beomy.github.io/tech/browser/cors/)](CORS%206f62779a4afd4cbe823b766f2bdbf60f/Untitled.png)

[https://beomy.github.io/tech/browser/cors/](https://beomy.github.io/tech/browser/cors/)

`cross-origin`이란 다음 중 한 가지라도 다른 경우를 말한다.

1. 프로토콜 - http와 https는 프로토콜이 다르다.
2. 도메인 - domain.com과 other-domain.com은 다르다.
3. 포트 번호 - 8080포트와 3000포트는 다르다.

# CORS는 왜필요한가

CORS가 없이 모든 곳에서 데이터를 요청할 수 있게 되면, 다른 사이트에서 원래 사이트를 흉내낼 수 있게 됩니다. 예를 들어서 기존 사이트와 완전히 동일하게 동작하도록 하여 사용자가 로그인을 하도록 만들고, 로그인했던 세션을 탈취하여 악의적으로 정보를 추출하거나 다른 사람의 정보를 입력하는 등 공격을 할 수 있습니다. 이렇나 공격을 할 수 없도록 브라우저에서 보호하고, 필요한 경우 에만 서버와 협의하여 요청할 수 있도록 하기 위해서 필요합니다.

출처 : [https://hannut91.github.io/blogs/infra/cors](https://hannut91.github.io/blogs/infra/cors)

# CORS를 사용하는 요청

- 위에서 논의한 바와 같이, `[XMLHttpRequest](https://developer.mozilla.org/ko/docs/Web/API/XMLHttpRequest)`와 [Fetch API](https://developer.mozilla.org/ko/docs/Web/API/Fetch_API) 호출.
- 웹 폰트(CSS 내 `@font-face`에서 교차 도메인 폰트 사용 시), [so that servers can deploy TrueType fonts that can only be cross-site loaded and used by web sites that are permitted to do so.](https://www.w3.org/TR/css-fonts-3/#font-fetching-requirements)
- [WebGL 텍스쳐](https://developer.mozilla.org/ko/docs/Web/API/WebGL_API/Tutorial/Using_textures_in_WebGL).
- `[drawImage()` (en-US)](https://developer.mozilla.org/en-US/docs/Web/API/CanvasRenderingContext2D/drawImage)를 사용해 캔버스에 그린 이미지/비디오 프레임.
- [이미지로부터 추출하는 CSS Shapes.](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Shapes/Shapes_From_Images)

# CORS의 메커니즘

# 참조

[[CORS] Cross Origin Resource Sharing](https://zamezzz.tistory.com/137)

[CORS란 무엇인가?](https://escapefromcoding.tistory.com/724)

[교차 출처 리소스 공유 (CORS) - HTTP | MDN](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)
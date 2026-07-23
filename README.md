# sp_preparation

Chuẩn bị kiến thức và phương án kỹ thuật để làm spotify client bằng java và spring boot.

## Caching

### Target

App này sử dụng Spotify API để lấy các thông tin như Album, Artist, Tracks, ...

Spotify API giới hạn rất nhiều cho developer, chính vì thế **Caching** là phương án bắt buộc.

### How

Sử dụng `spring-boot-starter-cache` và [caffeine](https://github.com/ben-manes/caffeine).

Các thuộc tính cấu hình đã tìm hiểu:

- maximumSize
- expireAfterWrite
- refreshAfterWrite (không tương thích với `spring-boot-starter-cache`)

### Ref

- [Cache Abstraction Java annotations](https://docs.spring.io/spring-framework/reference/integration/cache/annotations.html)
- [SpEL](https://docs.spring.io/spring-framework/reference/core/expressions.html)
- [caffeine](https://github.com/ben-manes/caffeine)
- [stackoverflow - refreshAfterWrite requires a LoadingCache](https://stackoverflow.com/questions/53659142/refreshafterwrite-requires-a-loadingcache-in-spring-boot-caffeine-application)

## Authentication

### Target

Có khả năng sử dụng OAuth 2.0 để xác thực người dùng sử dụng **tài khoản Spotify**, sử dụng **authorization_code**.

### How

Sử dụng `spring-boot-starter-security-oauth2-client`, sửa `application.properties`, cấu hình đủ cho `registration` và `provider`.

```
spring.security.oauth2.client.provider.<your_provider>.authorization-uri=https://accounts.spotify.com/authorize
spring.security.oauth2.client.provider.<your_provider>.token-uri=https://accounts.spotify.com/api/token
spring.security.oauth2.client.provider.<your_provider>.user-info-uri=https://api.spotify.com/v1/me
spring.security.oauth2.client.provider.<your_provider>.user-name-attribute=email
spring.security.oauth2.client.registration.<your_registration_id>.provider=<your_provider>
spring.security.oauth2.client.registration.<your_registration_id>.client-id=your_client_id
spring.security.oauth2.client.registration.<your_registration_id>.client-secret=your_client_secret
spring.security.oauth2.client.registration.<your_registration_id>.authorization-grant-type=authorization_code
spring.security.oauth2.client.registration.<your_registration_id>.redirect-uri={baseUrl}/login/oauth2/code/your_registration_id
spring.security.oauth2.client.registration.<your_registration_id>.scope[0]=user-read-private
spring.security.oauth2.client.registration.<your_registration_id>.scope[1]=user-read-email
```

Code mẫu bên trên đang có 2 scope, nhưng thực tế cần nhiều scope hơn để dùng Spotify SDK playback, fetch private playlist,...

Để truy vấn thông tin authenticated user có một vài cách:

#### Thymeleaf + SpEL

- Sử dụng `spring-boot-starter-webmvc`, `spring-boot-starter-thymeleaf`, `thymeleaf-extras-springsecurity6`
- `xmlns:th="https://www.thymeleaf.org"`
- `xmlns:sec="https://www.thymeleaf.org/thymeleaf-extras-springsecurity6"`
- Cách dùng [thymeleaf-extras-springsecurity6](https://github.com/thymeleaf/thymeleaf/tree/3.1-master/lib/thymeleaf-extras-springsecurity6)

#### Java

- Các @Annotation như @AuthenticationPrincipal có tại [Spring MVC Integration](https://docs.spring.io/spring-security/reference/servlet/integrations/mvc.html)

## Web template / SPA

## UI components library

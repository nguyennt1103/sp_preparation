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

## Web template / SPA

## UI components library

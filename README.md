# spring-cloud-gateway

![image](https://user-images.githubusercontent.com/51283645/144987110-9e68dc97-87cf-470b-b63e-30d129c844cc.png)


### gradle 의존성 추가
```
    // https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-netflix-eureka-client
    implementation("org.springframework.cloud:spring-cloud-starter-netflix-eureka-client:3.1.0")
    // https://mvnrepository.com/artifact/org.springframework.cloud/spring-cloud-starter-gateway
    implementation("org.springframework.cloud:spring-cloud-starter-gateway:3.1.0")
```

### yml
```
server:
  port: 7777

eureka:
  client:
    fetch-registry: true
    register-with-eureka: true
    service-url:
      defaultZone: http://localhost:9999/eureka # eureka port

spring:
  application:
    name: gateway-service
  cloud:
    gateway:
      routes:
        - id: test
#          uri: http://localhost:10000 # http://localhost:8000/test -> http://localhost:10000
          uri: lb://MSA # eureka 등록된 이름 사용시
          predicates:
            - Path=/test/** #  /test/**
#       - id: temp #여러개 사용시
#         uri: http://localhost:10001 # http://localhost:8000/temp -> http://localhost:10000
#         uri: lb://MSA2 # eureka 등록된 이름 사용시
#         predicates:
#           - Path=/temp/** #  /temp/**    

```
### curl 테스트
```
curl -X GET --location "http://localhost:7777/test"
```


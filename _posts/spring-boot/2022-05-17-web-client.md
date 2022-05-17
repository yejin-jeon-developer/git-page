---
title:  "WebClient 이슈 정리"
excerpt: "WebClient 이슈 정리"
categories:
  - spring-boot
---
## WebClient Pool Aquire Exception 발생
https://github.com/reactor/reactor-netty/issues/1060

45초 경과후 reactor.netty.internal.shaded.reactor.pool.PoolAcquireTimeoutException 발생.


## 이슈 원인
Spring Bug로 5.2.6 버전에서 수정됨.
운영서버 버전 확인 결과 5.2.1 버전으로 운영중인것 확인.

## 해결
spring-boot-starter-parent 버전업 (2.2.1.RELEASE -> 2.2.13.RELEASE)



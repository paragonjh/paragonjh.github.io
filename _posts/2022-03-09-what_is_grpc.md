---
title:  "gRPC란?"
excerpt: "gRPC 기술 소개"

categories:
  - gRPC
tags:
  - gRPC
last_modified_at: 2022-03-09T22:02:00-05:00
---

# gRPC란?

- Google에서 개발한 RPC(Remote Procedure Call) 시스템

- TCP/IP 프로토콜과 HTTP 2.0 프로토콜 사용

- IDL(Interface Definition Language)로 protocol buffer(proto3)를 사용


## gRPC의 구조
<center><img src="/assets/images/gRPC1.jpg" width="100%" height="100%"></center>

## gRPC의 장단점
### 장점
- gRPC의 protocol buffer로 리소스 사용량을 크게 줄여 JSON을 사용할 때보다 응답속도를 줄일 수 있음.
- 다양한 언어에서 사용 가능
C#, C+, Dart, Go, Java, Kotline, Node, Object-C, PHP, Python, Ruby 지원 (proto3)
- 서버-클라이언트 streaming, multiduplex bidirectional streaming 기능 제공 (HTTP2.0 특징)

### 단점
- 브라우저(Client)에서 proto 파일을 가지고 있을 수 없으므로 사용하기 어려움
- 서버의 proto 파일에 변화가 생길 경우 클라이언트의 proto 파일도 업데이트 필요


## gRPC Stream 종류
grpc에서 제공하는 Stream 종류는 다음과 같이 4가지가 있으며 이어지는 포스트에서 각각의 기술에 대해서 알아볼 예정이다.

1. Unary RPC
2. Server Streaming RPC
3. Client Streaming RPC
4. Bidirectional Streaming RPC
# 资源

* [https://github.com/grpc/grpc/tree/master/doc](https://github.com/grpc/grpc/tree/master/doc)

* gRPC状态转换：[https://github.com/grpc/grpc/blob/master/doc/connectivity-semantics-and-api.md](https://github.com/grpc/grpc/blob/master/doc/connectivity-semantics-and-api.md)

* gRPC鉴权：[https://grpc.io/docs/guides/auth/](https://grpc.io/docs/guides/auth/)

* proto3 guide: [https://developers.google.com/protocol-buffers/docs/proto3](https://developers.google.com/protocol-buffers/docs/proto3)

* http and gRPC Transcoding: [https://google.aip.dev/127](https://google.aip.dev/127)

* error: [https://cloud.google.com/apis/design/errors](https://cloud.google.com/apis/design/errors)

* 常用类型：[https://github.com/protocolbuffers/protobuf/blob/main/src/google/protobuf/wrappers.proto](https://github.com/protocolbuffers/protobuf/blob/main/src/google/protobuf/wrappers.proto)

* 《gRPC与云原生应用开发》代码示例：[https://grpc-up-and-running.github.io/](https://grpc-up-and-running.github.io/)

# 认证

# basic认证

https://github.com/grpc-up-and-running/samples/blob/master/ch06/basic-authentication/go/client/main.go

# 中间件

grpc提供的默认中间件

```go
import "github.com/grpc-ecosystem/go-grpc-middleware"

myServer := grpc.NewServer(
    grpc.StreamInterceptor(grpc_middleware.ChainStreamServer(
        grpc_ctxtags.StreamServerInterceptor(),
        grpc_opentracing.StreamServerInterceptor(),
        grpc_prometheus.StreamServerInterceptor,
        grpc_zap.StreamServerInterceptor(zapLogger),
        grpc_auth.StreamServerInterceptor(myAuthFunction),
        grpc_recovery.StreamServerInterceptor(),
    )),
    grpc.UnaryInterceptor(grpc_middleware.ChainUnaryServer(
        grpc_ctxtags.UnaryServerInterceptor(),
        grpc_opentracing.UnaryServerInterceptor(),
        grpc_prometheus.UnaryServerInterceptor,
        grpc_zap.UnaryServerInterceptor(zapLogger),
        grpc_auth.UnaryServerInterceptor(myAuthFunction),
        grpc_recovery.UnaryServerInterceptor(),
    )),
)

```
```mermaid
graph TB;
A-->B--C-.->D
```
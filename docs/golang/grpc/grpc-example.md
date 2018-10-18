# How to use gRPC

[Reference Link](https://github.com/grpc/grpc-go/blob/master/examples/gotutorial.md)

## Steps

###1. Defining the service

Define a service within file *route_guide.proto*.

Syntax:

```protobuf
// Interface exported by the server.
service RouteGuide {
	// you could place 'string' before a type
    rpc GetFeature(Point) returns (Feature) {}
}

message Point {
    int32 latitude = 1;
    int32 longitude = 2;
}

message Feature {
    string name = 1;
    Point location = 2;
}
```

### 2. Generating client and server code

You could do this using the **protobuf compiler** `protoc` with a special gRPC **go plugin**.

```shell
[root@k8s-1 tmp]# protoc --go_out=plugins=grpc:. route_guide.proto
[root@k8s-1 tmp]# ls
route_guide.proto route_guide.pb.go
```

### 3. Handle the server

First, implement the generated interface.

Then, build and start the server:

```reStructuredText
1. Specify the port we want to use to listen for client requests;
2. Create a instance of the gRPC server;
3. Register our service implementation with the gRPC server;
4. Call Serve() on the server with our port details to do a blocking wait until the process is killed or Stop() is called.
```

### 4. Handle the client

First, create a stub.

```text
1. Create a gRPC channel to communicate with the server;
2. Once the gRPC channel is setup, we need a client stub to perform RPCs;
```

Note that, in gRPC-go, RPCs operate in a blocking/synchronous mode.

### 5. Try it out

```text
1. Start the server;
2. Start the client to try it our.
```






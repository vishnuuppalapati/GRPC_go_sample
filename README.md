Install the grpc files globally:
--------------------------------
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

Download & Install protoc:
--------------------------
https://github.com/protocolbuffers/protobuf/releases
(protoc-25.1-win64.zip)

Floder structure will be like this:
-----------------------------------

grpc-greeter/
├── client/
│   └── main.go
├── gen/
│   └── helloworldpb/
│       ├── helloworld.pb.go
│       └── helloworld_grpc.pb.go
├── proto/
│   └── helloworld.proto
├── server/
│   └── main.go
└── go.mod

helloworld.proto: Need to delcare the services with request and response objects.
-----------------
syntax = "proto3";

package helloworld;

option go_package = "github.com/EnsurityTechnologies/gosamples/grpcsample/gen/helloworldpb";


service Greeter {
    rpc SayHello (HelloRequest) returns (HelloReply);
}

message HelloRequest {
    string name = 1;
    int32 age = 2;
}

message HelloReply {
    string message = 1;
}

Proto cmd execution:  terminal path should be in (github.com/EnsurityTechnologies/gosamples/grpcsample/proto)
--------------------
if proto exe recognizes globally and internal project --
protoc --go_out=../gen/helloworldpb --go-grpc_out=../gen/helloworldpb --go_opt=paths=source_relative --go-grpc_opt=paths=source_relative helloworld.proto

if not recognizes in the internal project but recognizes in globally --
& "C:\tools\protoc\bin\protoc.exe" --go_out=../gen/helloworldpb --go-grpc_out=../gen/helloworldpb --go_opt=paths=source_relative --go-grpc_opt=paths=source_relative helloworld.proto

server/main.go:
---------------
need to write the function and need to expose the port


client/main.go:
---------------
need to call the function and need to listen the port


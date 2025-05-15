Install the grpc files globally:
--------------------------------
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

Download & Install protoc:
--------------------------
CMD to install Protoc:winget install protobuf
(protoc-25.1-win64.zip)

##Floder structure will be like this:
-----------------------------------

grpc-greeter/
├── client/
│ └── main.go
├── gen/
│ └── helloworldpb/
│ ├── helloworld.pb.go
│ └── helloworld_grpc.pb.go
├── proto/
│ └── helloworld.proto
├── server/
│ └── main.go
└── go.mod

- **client/**: Contains the client-side logic for communicating with the gRPC server.
  - `main.go`: The entry point for the client, which connects to the gRPC server and calls the service.
  
- **gen/**: Contains the generated Go code from the `.proto` file.
  - **helloworldpb/**: This folder contains the Go files generated from `helloworld.proto`.
    - `helloworld.pb.go`: The Go struct definitions for the gRPC messages.
    - `helloworld_grpc.pb.go`: The Go code for the gRPC client and server methods.

- **proto/**: Contains the `.proto` file(s) that define the gRPC service and messages.
  - `helloworld.proto`: The Protocol Buffers definition for the Greeter service.

- **server/**: Contains the server-side logic for the gRPC service.
  - `main.go`: The entry point for the server, which implements the Greeter service.

- **go.mod**: The Go module file that defines the project dependencies.
  
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
if proto exe recognizes globally and internal project :
protoc --go_out=../gen/helloworldpb --go-grpc_out=../gen/helloworldpb --go_opt=paths=source_relative --go-grpc_opt=paths=source_relative helloworld.proto

if not recognizes in the internal project but recognizes in globally:
& "C:\tools\protoc\bin\protoc.exe" --go_out=../gen/helloworldpb --go-grpc_out=../gen/helloworldpb --go_opt=paths=source_relative --go-grpc_opt=paths=source_relative helloworld.proto

server/main.go:
---------------
need to write the function and need to expose the port


client/main.go:
---------------
need to call the function and need to listen the port


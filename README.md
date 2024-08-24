# tronprotocol

```shell
go install google.golang.org/protobuf/cmd/protoc-gen-go@latest
go install google.golang.org/grpc/cmd/protoc-gen-go-grpc@latest

export PATH="$PATH:$(go env GOPATH)/bin"

git submodule update --recursive --remote

find ./protocol -name "*.proto" -exec sed -i '' '/option go_package/ s|github.com/tronprotocol/grpc-gateway|github.com/v03413/tronprotocol|g' {} +

protoc -I ./protocol -I . --go_out=. --go-grpc_out=. --go_opt=paths=source_relative --go-grpc_opt=paths=source_relative ./protocol/api/*.proto
protoc -I ./protocol -I . --go_out=. --go_opt=module=github.com/v03413/tronprotocol ./protocol/core/*.proto
protoc -I ./protocol -I . --go_out=. --go_opt=module=github.com/v03413/tronprotocol ./protocol/core/contract/*.proto
```
# Golang Build

## Usage

```
build-linux-arm64:
        podman run --rm -it \
        -v $(CURR_DIR):/app \
        -v $$HOME/go/pkg/mod:/go/pkg/mod \
        -w /app \
        -e GOOS=linux \
        -e GOARCH=arm64 \
        -e CGO_ENABLED=1 \
        -e CC=/opt/gcc-linaro-7.4.1-2019.02-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-gcc \
        -e CXX=/opt/gcc-linaro-7.4.1-2019.02-x86_64_aarch64-linux-gnu/bin/aarch64-linux-gnu-g++ \
        $(BUILD_IMAGE) \
        go build -ldflags="-s -w" -v -buildvcs=false -o ${ARM64_OUTPUT} ${CMD_DIR}

build-linux-arm:
        podman run --rm -it \
        -v $(CURR_DIR):/app \
        -v $$HOME/go/pkg/mod:/go/pkg/mod \
        -w /app \
        -e GOOS=linux \
        -e GOARCH=arm \
        -e CGO_ENABLED=1 \
        -e CC=/opt/gcc-linaro-5.3.1-2016.05-x86_64_arm-linux-gnueabi/bin/arm-linux-gnueabi-gcc \
        -e CXX=/opt/gcc-linaro-5.3.1-2016.05-x86_64_arm-linux-gnueabi/bin/arm-linux-gnueabi-g++ \
        $(BUILD_IMAGE) \
        go build -ldflags="-s -w" -v -buildvcs=false -o ${ARM_OUTPUT} ${CMD_DIR}

build-windows-amd64:
        podman run --rm -it \
        -v $(CURR_DIR):/app \
        -v $$HOME/go/pkg/mod:/go/pkg/mod \
        -w /app \
        -e GOOS=windows \
        -e GOARCH=amd64 \
        -e CGO_ENABLED=1 \
        $(BUILD_IMAGE) \
        go build -ldflags="-s -w" -v -buildvcs=false -o ${AMD64_OUTPUT} ${CMD_DIR}
```

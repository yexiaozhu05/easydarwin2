# 使用 Go 语言官方基础镜像
#FROM golang:latest
FROM ubuntu:22.04
RUN mv /etc/apt/sources.list /etc/apt/sources.list.bak
COPY dockerbuild/tuna_http.list /etc/apt/sources.list.d/163.list
RUN apt-get update && apt-get install -y ca-certificates

COPY dockerbuild/tuna_https.list /etc/apt/sources.list.d/163.list

RUN apt-get update && apt-get install -y openssl \
    openssh-server \
    openssh-client \
    sudo \
    vim \
    supervisor \
    jq \
    gcc \
    libc6-dev \
    git \
    lrzsz \
    golang \
    curl && apt-get clean
# 设置工作目录
ENV GOROOT=/usr/lib/go
ENV PATH=$PATH:/usr/lib/go/bin
ENV GOPATH=/root/go
ENV PATH=$GOPATH/bin/:$PATH
WORKDIR /app

# 复制所有文件到工作目录
COPY . .

# 初始化 Go module
RUN go mod init github.com/yexiaozhu05/easydarwin2

RUN go mod tidy

RUN go mod vendor

COPY ./play.html /app/www/play.html

# 构建应用
RUN go build -o easydarwin .

# 暴露所需的端口
#EXPOSE 554
#EXPOSE 10008

# 启动应用
CMD ["./easydarwin"]

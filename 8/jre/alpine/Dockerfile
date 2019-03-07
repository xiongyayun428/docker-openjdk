FROM openjdk:8-jre-alpine
LABEL Author="熊亚运 <xiongyayun428@163.com>"

# Install cURL
# RUN echo -e "https://mirror.tuna.tsinghua.edu.cn/alpine/v3.9/main\n\
# https://mirror.tuna.tsinghua.edu.cn/alpine/v3.9/community" > /etc/apk/repositories
RUN echo -e "http://dl-cdn.alpinelinux.org/alpine/v3.9/main/\n\
http://dl-cdn.alpinelinux.org/alpine/v3.9/community" > /etc/apk/repositories

RUN apk --update add curl bash ttf-dejavu && \
    rm -rf /var/cache/apk/*

#****************** 安装gclib ；解决时区问题 ***********************
#RUN在镜像中运行命令，必须是基础镜像识别的命令
#Java是基于GUN Standard C library(glibc)，Alpine是基于MUSL libc(mini libc)  ，需要安装gclib库
#截止到目前最稳定的版本是2.29

RUN apk --no-cache add ca-certificates wget && \
    wget -q -O /etc/apk/keys/sgerrand.rsa.pub https://alpine-pkgs.sgerrand.com/sgerrand.rsa.pub && \
    wget https://github.com/sgerrand/alpine-pkg-glibc/releases/download/2.29-r0/glibc-2.29-r0.apk && \
    apk add glibc-2.29-r0.apk && \
#解决时区错乱的问题*******************************************************    
    apk update && \
    apk add --no-cache ca-certificates && \
    apk add --no-cache curl bash tree tzdata && \
    cp -rf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    rm -rf glibc-2.29-r0.apk

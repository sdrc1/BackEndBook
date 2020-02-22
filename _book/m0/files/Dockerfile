# 基础镜像
# 任何 Dockerfile 都需要有一个 FROM
# 如果想从一个空镜像开始构建, 则可以使用 `FROM scratch`
FROM debian:jessie

# 环境变量, 可选
# 环境变量可以在后续指令中使用, 环境变量在 container 运行时会被设置为 envvar.
ENV NGINX_VERSION=1.11.10-1~jessie

# 下面这段是简化了的一个 RUN, 实际 nginx 构建的时候比这个复杂, 仅为说明 RUN 指令.
# RUN 即在构建时在 container 的 shell 中执行的命令
# 通过 && 连接命令的话可以不用把多个指令分配到多个 Layer, 这样可以节约空间和时间.
RUN apt-get update \
    && apt-get install nginx -y

# 将所有的日志转发到标准输出和标准错误中, 在 Docker 中只能用这样的方式来输出日志.
# 其中 stdout 和 stderr 就是 Docker 中的 "log collector".
# 转发后 Docker 就可以获取这些日志信息了
RUN ln -sf /dev/stdout /var/log/nginx/access.log \
    && ln -sf /dev/stderr /var/log/nginx/error.log

# 暴露端口
# 默认情况下, Docker container 中没有任何暴露的端口, 无论 tcp 还是 udp 协议.
# 可以通过 EXPOSE 指令将端口暴露到虚拟网络下.
# 暴露端口后, 就可以通过 -p/-P 参数在启动时将端口开放/转发到 host 了.
EXPOSE 80 443

# CMD一般都是最后一个指令, 且是必须的指令
# 它提供当 container 启动后所要执行的命令, 且只能有一个 CMD 指令存在
# 如果有多个 CMD, 则最后一个将会被执行.
CMD [ "nginx", "-g", "daemon off;" ]
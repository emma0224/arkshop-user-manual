# 自定义镜像

如果平台提供的基础镜像不满足您的需求，可以使用平台提供的自定义镜像功能。点击控制台左侧导航-镜像，查看推送命令，根据提示将您的Docker镜像推送到平台，就可以在工作空间或者推理服务创建的时候，选择您指定的自定义镜像。

自定义镜像构建时，有几点注意：

1. 如果您是在mac电脑上构建镜像，请注意在docker build时加上platform=linux/amd64的选项，例如

```bash
docker buildx build -f Dockerfile --platform=linux/amd64 -t my-image -f Dockerfile .
```

2. 在工作空间中使用的自定义镜像，需要新增一个具有sudo权限的user用户，并且没有配置过SSH，下面是一个简单的Dockerfile示例。您也可以基于平台提供的标准镜像之上进行构建。

```docker
FROM python
RUN sed -i -e 's/\w\+\.debian\.org/mirrors.aliyun.com/g' /etc/apt/sources.list \
    && apt-get update && apt-get install sudo \
    && useradd -ms /bin/bash user && echo "user ALL=(ALL) NOPASSWD:ALL" | tee -a /etc/sudoers.d/90-cloud-init-user \
    && rm -rf /var/run/sshd \
    && pip config set global.index-url https://mirror.baidu.com/pypi/simple \
    && pip install torch
ENV SHELL=/bin/bash
CMD ["bash"]
```


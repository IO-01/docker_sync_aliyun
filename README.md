# 转存 docker 镜像到阿里云镜像托管服务
使用 GitHub Actions 拉取 docker 推送到阿里云镜像托管服务，用于缓解国内 docker 镜像服务集体失效的问题。

使用阿里云出品的 [image-syncer](https://github.com/AliyunContainerService/image-syncer) 而非直接通过 Docker pull & push 可以规避 Docker 客户端不方便自定义复杂的拉取规则。

##  简单使用方式
### 1. 配置阿里云容器镜像服务
1. 登录[容器镜像服务](https://cr.console.aliyun.com/)，新建个人版容器命名空间。
2. 「访问凭证」- 设置固定密码。
3. 记住「访问凭证」中的仓库地址、非脱敏后的用户名和密码，下一步需要用到。
### 2. Fork 本项目
1. 进入 Fork 后自己的项目。
2. 修改 `auth.yaml` 中的字段为 `自己仓库地址/命名空间`。
3. 「Settings」-「Secret and variables」-「Actions」-「New repository secret」新增 `ACR_USER` 和 `ACR_PASSWORD`，分别为「阿里云容器镜像服务」-「访问凭证」中非脱敏后的用户名和密码。
4. 进入「Actions」启用 Actions。
5. 编辑 `images.yaml` 添加对应镜像即可，规则参考 [image-syncer](https://github.com/AliyunContainerService/image-syncer)，**建议用 `latest` 等 TAG 限制转存范围，防止过分滥用 Actions 服务**。
6. （可选）把自己仓库地址配置成镜像源，省去输入完整镜像地址。
7. 修改原来的镜像地址为 `images.yaml` 配置的目标地址。

---
sidebarDepth: 2
---
### 创建您的第一个服务

> 从项目列表中点击"查看服务" 进入服务列表。点击创建标准服务进入创建服务流程。

<img src="https://resource.spotmaxtech.com/maxcloud-doc/createserving/image-20210906154903846.png" alt="image-20210906154903846" style="zoom:50%;" />

- 命名空间

  - 只能选择已经添加到项目中的命名空间，无法选择集群中的其他命名空间

- 服务名称

  - 微服务名称，建议填写有意义且容易区分的名称

- 版本别名

  - 可选参数，默认为 服务名-yyyyMMdd-HHmmss。您也可以按照自己的习惯填写。

- 镜像名称

  - docker镜像地址，如果镜像不是在`hub.docker.com` 则镜像需要填带有域名的完整地址，例如阿里云镜像地址`registry.cn-hongkong.aliyuncs.com/spotmax/helloworld-go`

- 镜像版本

  - 镜像的版本。

- 秘钥，

  - 如果您的镜像不是公开的，则需要提前创建秘钥，这里选择已经创建好的秘钥。

    再集群管理页面的控制台执行如下命令，创建拉取镜像的秘钥。

    ```shell
    kubectl create secret docker-registry regcred \
      --docker-server=<你的镜像仓库服务器> \
      --docker-username=<你的用户名> \
      --docker-password=<你的密码> \
      --docker-email=<你的邮箱地址>
    ```

    

- 访问协议

  - 按照您服务对外提供的服务类型选择HTTP or GRPC

- 容器端口

  - 填写您服务对外提供的端口。

---

### 高级选项

<img src="https://resource.spotmaxtech.com/maxcloud-doc/createserving/image-20210906172328741.png" alt="image-20210906172328741" style="zoom:50%;" />

- 伸缩指标

  > 选择基于那个指标做扩容、缩容

  - 最大并发数。
  - 每秒最大请求数
  - CPU  （cpu使用率）

- 伸缩值
  - 指标值达到伸缩值后扩容，小于伸缩值缩容
- 最大值、最小值
  - 扩容最大pod数，和最小pod数
- 并发目标容量
  - 没有缓冲的情况下处理的流量突发大小
- 资源限制CPU
  - 单个Pod 可使用最大CPU量。对应k8s的 limits.cpu
- 内存
  - 单个Pod 可使用最大内存。对应k8s的 limits.memory

- 环境变量

  > 环境变量支持自定义、配置想（comfigMap）、秘钥（secret）三种设置方式

  ![image-20210907103704776](https://resource.spotmaxtech.com/maxcloud-doc/createserving/image-20210907103704776.png)

- 数据卷

  > 数据卷支持本地存储和云存储
  >
  > 本地存储

![image-20210907105412073](https://resource.spotmaxtech.com/maxcloud-doc/createserving/image-20210907105412073.png)





```text
kubectl create secret tls spotmaxtech-secret \
    --namespace maxcloud-prod \
    --key server.key \
    --cert server.pem
```
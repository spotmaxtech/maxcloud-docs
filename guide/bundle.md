---
sidebarDepth: 2
---

## 📦 Bundle 使用简介

> bundle 是MaxCloud制定的一种k8s资源的组织方式。可以把一组有逻辑关系的资源组装到一起作为应用，从而实现应用级别发布、回滚等操作。

**下面以MaxCloud 管理的MaxCloud测试环境相关bundle为例说明。**

### 预览


![image-20220301155015651](https://resource.spotmaxtech.com/maxcloud-doc/clusterImport/image-20220301155015651.png)

### 创建bundle

点击`New App`,填写Bundle名称，选择类型

- Native Bundle：选择集群中已经创建好的资源创建bundle
- Helm Bundle：选择Helm创建bundle（方便helm相关资源使用bundle相关能力）
- 从其他应用复制：复制已有的bundle为新Bundle（私有化部署或基于测试环境bundle创建线上环境bundle）

![image-20220301162320319](https://resource.spotmaxtech.com/maxcloud-doc/clusterImport/image-20220301162320319.png)

1. 创建Native Bundle选择资源

   - 选择命名空间
   - 选择资源，假设选择了Deployment，会自动关联Deployment相关的Service、ConfigMap、Secret等资源
   - 填写版本描述（主要用于后续回滚的时候判断当前版本的操作，修改的时候建议填写）
   - 填写应用描述（填写应用简介，方便区分应用）

   ![image-20220301163218252](https://resource.spotmaxtech.com/maxcloud-doc/clusterImport/image-20220301163218252.png)

2. 创建Helm Bundle

   >  如果您的应用是用Helm部署，但是为了使用MaxCloud相关操作也可以给Helm创建Bundle

   - 选择命名空间
   - 选择Helm 填写相关信息后直接提交
   - 由于Helm的发布、升级由Helm 管理，基于Helm创建的Bundle不能使用GitOps相关功能

   ![image-20220301164849341](https://resource.spotmaxtech.com/maxcloud-doc/clusterImport/image-20220301164849341.png)

3. 复制Bundle

   - 填写新bundle名称
   - 选择已有bundle

   <img src="https://resource.spotmaxtech.com/maxcloud-doc/clusterImport/image-20220301165319852.png" alt="image-20220301165319852" style="zoom:50%;" />

   - 确定后可以继续修改已有资源或新增其他资源

     ![image-20220301165457780](https://resource.spotmaxtech.com/maxcloud-doc/clusterImport/image-20220301165457780.png)

   

### 查看Bundle资源详情

点击Bundle的资源可以查看资源的详情，以Deployment为例：包含（pod列表、Yaml、Lables、等信息）也可以在这个页面执行重启、伸缩等操作

![image-20220301171629073](https://resource.spotmaxtech.com/maxcloud-doc/clusterImport/image-20220301171629073.png)

### GitOps

以jenkins 为例，当我们生成Docker 镜像后需要发布到集群。可以使用GitOps中提供的Curl脚本和jenkins集成。

**Jenkinsfile 示例**

增加如下Stage即可通过MaxCloud把镜像发布到集群中，其中Tag 变量需要和您打包镜像的tag一致。

```shell
stage("Rollout") {
        steps {
        sh '''
        #!/bin/bash
        #请将这段脚本粘贴到合适的位置，并修改这个tag，集成即完成。
        image="registry.cn-hongkong.aliyuncs.com/spotmax/maxcloud-api:${Tag}"
        secret="xxxxxxxx"
        sign=`echo -n "${image}|${secret}" | md5sum | awk '{print $1}'`
        curl --location --request POST 'https://maxcloud-api.spotmaxtech.com/api/external/bundle/upgrade' \
        --header 'Content-Type: application/json' \
        --data '{
            "bundle_id": 164568,
            "resource_name": "maxcloud-api-test",
            "resource_kind": "deployment",
            "image": "'$image'",
            "sign": "'$sign'"
        }'
        '''
    }
}
```



# MaxLang 操作MaxCloud相关功能示例

## 登录MaxCloud
loginMaxCloud("用户名","密码")

参数1：用户名（登录MaxCloud账户）

参数2：密码（登录MaxCloud密码）
```
loginMaxcloud("jianwen.gao@mobvista.com", <<password>>)
```

## 使用Credential 方式登录MaxCloud
setCredential("maxcloud", "jianwen.gao@mobvista.com", <\<password\>>)

loginMaxcloud("maxcloud")
```
setCredential("maxcloudab", "jianwen.gao@mobvista.com", <<password>>)

loginMaxcloud("maxcloudab")
```

## 获取Team列表
获取登录账号可以使用的所有Team列表
```
listTeam()
```

## 获取Team下的所有项目列表
listProject(teamId)

参数1：团队ID
```
listProject(1)
```

## 获取项目下的所有集群列表
listCluster(teamId, projectId)

参数1：团队ID

参数2：项目ID
```
listCluster(1, 79)
```

## 初始化集群参数变量
使用一个map变量保存teamId、projectId,clusterId、namespace 等参数，使用一个方便识别的名称，后续集群相关方法调用第一个参数都传入这个变量，用于指定集群环境。

teamId,projectId,clusterId 等参数可以直接从MaxCloud项目管理页面复制，如下图所示


<img src="https://resource.spotmaxtech.com/common/1665386004933.jpg" alt="image-20221010151738693" style="zoom:50%;" />

从网页中复制的一下内容，只有 `teamId`、`projectId`、 `clusterId`、 `namespace` 几个参数是必填的，Name相关参数只是为了方便您识别
```
Crazywolf_test_ack_maxcloud_bj_demo = {
        "teamId": 1,
        "teamName": "MaxCloud",
        "projectId": 62,
        "projectName": "Crazywolf-test",
        "clusterId": 22,
        "clusterName": "ack-maxcloud-bj-demo",
        "namespace": "crazywolf"
}
```

## 设置当前环境的kubeconfig
参数1：集群环境变量

此函数执行后会把当前集群环境变量指定集群的kubeconfig放在当前环境的~/.kube/config 文件中，后续可以使用 `exec(xxx)`执行shell 命令，如果使用`exec(kubectl get pod -n namespaceName)` 就可以获取指定namespace下的pod列表

如果需要切换kubeconfig需要重新执行useCluster，该操作会用新集群kubeconfig覆盖之前的文件
```
useCluster(bj_demo_crazywolf)
```

### 展示设置集群kubeconfig后使用shell命令操作集群
```
exec("kubectl get deployment -n crazywolf")
```

## 创建命名空间
参数1：集群环境变量

参数2：新命名空间名称
```
createNamespace(bj_demo_crazywolf, "gjw-0910")
```

## 获取资源Yaml
参数1：集群环境变量

参数2：资源类型

参数3：资源名称
```
getYaml(bj_demo_crazywolf, "deployment","ngxin-dep-0")
```

## Describe 资源
参数1：集群环境变量

参数2： 资源类型

参数3：资源名称
```
describeResource(bj_demo_crazywolf, "deployment", "ngxin-dep-0")
```

## Scale Deployment
参数1：集群环境变量

参数2：Deployment 名称

参数3： Replicas 数量
```
scaleDeployment(bj_demo_crazywolf, "ngxin-dep-0", 1)
```

## Scale Statefulset
参数1：集群环境变量

参数2：Statefulset 名称

参数3：Replicas 数量
```
scaleStatefulset(bj_demo_crazywolf, "xxxx", 2)
```

## 列举所有资源
参数1：集群环境变量

参数2：资源类型

listResource 指定资源类型后可以获取上面指定集群命名空间下的所有资源
listResource 可以只传入一个类型参数，也可以传入第二个参数作为零时命名空间（不会覆盖之前useCluster设置的命名空间）

目前支持的资源为：

- deployment
- job
- cronjob
- daemonset 
- statefulset
- service
- ingress
- persistentvolumeclaim
- configmap
- secret
- gateway
- namespace
- pod
- horizontalpodautoscaler
- serviceaccount
- replicaset
- poddisruptionbudget
- node
- storageclass
```
listResource(bj_demo_crazywolf, "deployment")
```

## 获取随机字符串
randStr参数为需要获取随机字符串长度，如果不传参数默认为6
```
randStr(6)
```

## 把Maxlang对象转换成Json

### 测试把Map转换为json
```
/*
声明一个MAP 对象
*/
mapObj = {
    "name" : "CrazyWolf",
    "age" : 18,
    "address" : "beiijng"
}
/* 把map 对象转换成json */
toJson(mapObj)
```

### 测试把数组对象转换成json
```
/*
声明一个Array 对象
*/

arrayObj = [1, true, "stringObj"]

/* 
把map 对象转换成json 
*/
toJson(arrayObj)
```

### 测试把函数返回对象转为json
```
toJson(listTeam())
```

## 等待N秒
sleep(second)

参数1：休眠秒数
```
sleep(5)
```

## 使用模版Apply Yaml

### 声明字符串模版
模版语法同Golang 语法
```
configStr = `apiVersion: v1
kind: ConfigMap
metadata:
  name: myconfigmap-{{.nameSuffix}}
  namespace: crazywolf
  labels:
    app: myapplication
data:
  data: {{.randData}}`
```

### 声明一个Map数据用于替换上面模版的占位
Map 数据key、value 都必须是字符串，暂不支持其他类型
```
randstr = randStr(6)
data = {"nameSuffix":randstr, "randData":randstr}
```

### 使用fillTemp 方法用map 替换模版中的占位符，获取最终可执行的yaml字符串
```
yaml = fillTemp(configStr, data)
yaml
```

### 调用applyYaml 方法在集群中部署yaml
```
applyYaml(bj_demo_crazywolf, yaml)
```

# HPA

## 锁定HPA
参数1：当前集群环境
参数2：HPA 名称
参数3：minReplicas

设置minReplicas值，默认MaxReplicas不变，如果当前MaxReplicas小于要设置的minReplicas则修改 MaxReplicas为minReplicas一样
例如：

```yaml
demo-hap
 minReplicas: 2
 maxReplicas: 5
```

调用 localHpa(env, "demo-hpa", 3)，锁定为3则执行后结果为
```yaml
demo-hap
 minReplicas: 3
 maxReplicas: 5
```

如果再次调用调用 localHpa(env, "demo-hpa", 10)，锁定为10则执行后结果为
```yaml
demo-hap
 minReplicas: 10
 maxReplicas: 10
```
```
lockHpa(bj_demo_crazywolf, "gjw-test", 1)
```

## 设置HPA 的Replicas
参数1：HPA名称

参数2：minReplicas

参数3：maxReplicas
```
setHpaReplicas(bj_demo_crazywolf, "gjw-test", 1, 2)
```

### 获取HPA的minReplicas
参数1：集群环境

参数2：HPA名称
```
getHpaMin(bj_demo_crazywolf, "gjw-test")
```

### 获取HPA的maxReplicas
参数1：集群环境

参数2：HPA名称
```
getHpaMax(bj_demo_crazywolf, "gjw-test")
```

### 获取HPA当前Replicas
参数1：集群环境

参数2：HPA名称
```
getHpaCurrent(bj_demo_crazywolf, "gjw-test")
```

## Helm 安装

### 添加Repo

参数1：集群环境变量

参数2：repo name

参数3：repo URL
```
addOrUpdateRepo(bj_demo_crazywolf, "bitnami", "https://charts.bitnami.com/bitnami")
```

### 设置sets 
```
sets = {
"wordpressBlogName" : "CrazyWolf3453456"
}
```

### 安装Chart
参数1：集群环境变量

参数2：releaseName

参数3：chart name

参数4：chart版本

参数5：sets参数 （可选）
```
installOrUpgradeChart(bj_demo_crazywolf, "my-wordpress", "bitnami/wordpress", "15.2.5", sets)
```

## 查循已安装的Helm列表
参…-stage-old.detailroi.mintegral.com")


## AWS ASG Size查询和更改

ASG 相关方法都支持通过公共方法执行云商，或者用云商的方法名，以获取asg为例

- 参数中指定云商（aws、aliyun、huawei）
```

    getASG("credential", "aws","us-west-2", "kmax-demo-asg-small")
```

- 直接用云商的方法
```
    getAwsASG("credential", "us-west-2", "kmax-demo-asg-small")
```

listASGs、getASG、updateASG、lockASG 都支持上述使用方式

### usage:

#### 列出region的ASG， 如果asgName是空， 列出所有的ASG
```
- listASGs("credential", "aws", region, asgName)
```

#### 更新ASG的最小容量、最大容量、所需容量
```
- updateASG("credential","aws", region, asgName, miniSize, maxSize, desiredSize)
```
#### 获取ASG的最大、最小、所需容量
```
- getASG("credential","aws", region, asgName)
```
#### 锁定ASG到lockSize
```
- lockASG("credential","aws", region, asgName, lockSize)
```
e.g.  
```
    listASGs("credential", "aws", "us-west-2", "kmax-demo-asg-small")
	getASG("credential", "aws","us-west-2", "kmax-demo-asg-small")
	updateASG("credential", "aws", "us-west-2", "kmax-demo-asg-small", 2, 2, 2) 
	lockASG("credential", "aws", "us-west-2", "kmax-demo-asg-small", 2) 
    
    listAwsASGs("credential", "us-west-2", "kmax-demo-asg-small")
	getAwsASG("credential", "us-west-2", "kmax-demo-asg-small")
	updateAwsASG("credential", "us-west-2", "kmax-demo-asg-small", 2, 2, 2) 
	lockAwsASG("credential", "us-west-2", "kmax-demo-asg-small", 2) 
```

### 查询ASG(s)

参数1：云商credential ，请先试用setCredential(name, key, value 设置)

参数2：region

参数3：asgName （可选）

- 获取Aws asg列表
```
listAwsASGs("credential", "us-west-2")

listAwsASGs("credential", "us-west-2", "asgName")
```
- 获取阿里云 asg 列表
```
listAliASGs("credential", "us-west-2")

listAliASGs("credential", "us-west-2", "asgName")
```
- 获取huawei asg 列表
```
listHwASGs("credential", "us-west-2")

listHwASGs("credential", "us-west-2", "asgName")
```
**使用参数指定云商**
```
listHwASGs("credential", "aws", "us-west-2")

listHwASGs("credential", "aws", "us-west-2", "asgName")

listAwsASGs("credential", "us-west-2")
listAliASGs("credential", "us-west-2")
listHwASGs("credential", "us-west-2")
```

### 更改ASG的最小容量、最大容量、所需容量

参数1：云商credential ，请先试用setCredential(name, key, value 设置)

参数2：region

参数3：asgName

参数4：最小

参数5：最大

参数6：期望值

- 修改Aws asg
```
updateAwsASG("credential", "us-west-2", "asgName", 1, 100, 50)
```
- 修改阿里云 asg
```
updateAliASG("credential", "us-west-2", "asgName", 1, 100, 50)
```
- 修改 huawei asg
```
updateHwASG("credential", "us-west-2", "asgName" ,1, 100, 50)
```
**使用参数指定云商**
```
updateHwASG("credential", "aws", "us-west-2", "asgName" ,1, 100, 50)
updateAwsASG("credential", "us-west-2", "kmax-demo-asg-small", 2, 2, 2)
updateAliASG("credential", "us-west-2", "kmax-demo-asg-small", 2, 2, 2)
updateHwASG("credential", "us-west-2", "kmax-demo-asg-small", 2, 2, 2)
```

### 锁定ASG容量

参数1：云商credential ，请先试用setCredential(name, key, value 设置)

参数2：region

参数3：asgName

参数4：锁定值

如果参数4锁定值小于1，则最小值会被修改为当前的期望值
如果参数4大于最大值，则最大值会被修改为锁定值
如果期望值小于参数4锁定值，则期望值修改为所定值

- 锁定Aws asg
```
lockAwsASG("credential", "us-west-2", "asgName", 10)
```
- 锁定aliyun asg
```
lockAliASG("credential", "us-west-2", "asgName", 10)
```
- 锁定huawei asg
```
lockHwASG("credential", "us-west-2", "asgName", 10)

lockAwsASG("credential", "us-west-2", "asgName", 10)
lockAliASG("credential", "us-west-2", "asgName", 10)
lockHwASG("credential", "us-west-2", "asgName", 10)
```

## 获取asg
参数1：云商credential ，请先试用setCredential(name, key, value 设置)

参数2：region

参数3：asgName

- 获取Aws asg列表
```
getAwsASG("credential", "us-west-2", "asgName")
```
- 获取阿里云 asg 列表
```
getAliASG("credential", "us-west-2", "asgName")
```
- 获取huawei asg 列表
```
getHwASG("credential", "us-west-2", "asgName")

getAwsASG("credential", "us-west-2", "asgName")
getAliASG("credential", "us-west-2", "asgName")
getHwASG("credential", "us-west-2", "asgName")
```

# Bucket 管理

## 列出Bucket
```
listBucket
```

参数1：credential

参数2：云商provider

参数3：endpoint(aliyun的时候必传)

- 列出Aws bucket
```
listBucket("credential", "aws")
```
- 列出Aliyun bucket
```
listBucket("credential", "aliyun",  "https://oss-cn-beijing.aliyuncs.com")

listBucket("credential", "aws")
listBucket("credential", "aliyun",  "https://oss-cn-beijing.aliyuncs.com")
```

## 创建文件夹
```
newBucketDir
```

参数1：credential

参数2：云商provider （aws,aliyun）

参数3：bucketName

参数4：dirName

参数5：endpoint(aliyun的时候必传)

- aws 指定bucket下创建文件
```
newBucketDir("credential", "aws", "bucketName", "test_dirname")
```
- aliyun 指定bucket下创建文件
```
newBucketDir("credential", "aliyun", "bucketName", "test_dirname", "https://oss-cn-beijing.aliyuncs.com")

newBucketDir("credential", "aws", "bucketName", "test_dirname")
newBucketDir("credential", "aliyun", "bucketName", "test_dirname", "https://oss-cn-beijing.aliyuncs.com")
```

## 列出Bucket 中的文件
```
listBucketFile
```

参数1：credential

参数2：云商provider

参数3：bucketName

参数4：前缀 Prefix

参数5：endpoint(aliyun的时候必传)

- 列出aws 指定bucket 下的文件
```
listBucketFile("credential", "aws", "bucketName", "test_dirname/")
```
- 列出aliyun 指定bucket 下的文件
```
listBucketFile("credential", "aliyun", "bucketName", "test_dirname/", "https://oss-cn-beijing.aliyuncs.com")

listBucketFile("credential", "aws", "bucketName", "test_dirname/")
listBucketFile("credential", "aliyun", "bucketName", "test_dirname/", "https://oss-cn-beijing.aliyuncs.com")
```
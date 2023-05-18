# MaxLang Quick Start 
## -- All New Design, All For DevOps
`MaxLang` is the dedicated programming language for automating the DevOps tasks, which is implemented and maintained by SpotMax team.

## addOrUpdateRepo
#### 方法描述:
``` 
Helm 安装添加Repo
		addOrUpdateRepo(bj_demo_crazywolf, "bitnami", "https://charts.bitnami.com/bitnami")

		参数1：集群环境变量
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

		参数2：repo name

		参数3：repo URL
```

#### 示例:
``` 
addOrUpdateRepo(参数1, 参数2, 参数3)
``` 

## applyYaml
#### 方法描述:
``` 
获取Pod详情
		applyYaml(bj_demo_crazywolf, yaml) 
		可以与fillTemp(configStr, data)配合使用
		
		参数0：指定集群环境
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

		参数1：资源类型
		"apiVersion: v1
		kind: ConfigMap
		metadata:
		  name: myconfigmap-b64ded
		  namespace: crazywolf
		  labels:
			app: myapplication
		data:
		  data: b64ded"
```

#### 示例:
``` 
applyYaml(参数1, 参数2)
```

## build_bundle_group_scale_plan
#### 方法描述:
``` 
构建bundle_group的伸缩计划
```

#### 示例:
``` 
build_bundle_group_scale_plan({
	"team_id":3,
	"bundle_group_id":8,
	"scare_source":"same_time_yesterday",
	"scare_ratio":"1.3"
})
``` 

## bundle_group_scale
#### 方法描述:
``` 
根据bundle伸缩计划进行bundle的伸缩
```

#### 示例:
``` 
bundle_group_scare(plan)
``` 

## createCluster
#### 方法描述:
``` 
创建K8S集群

		参数会替换模版中相应的字段。 如name参数会替换template中的name字段
	subnetIDs:
		字符串数组， 指定集群所在的subnets 例如
		credential = "aliCredit"
		provider = "aliyun"// aliyun, aws, huawei
		region = "cn-beijing"
		vpcID = "xxxdfsdfsdf"	
		setCredential(credential, "keyid", <<password>>)
		subnetIDs = ["vsw-2zen61tp041lskzzzhukq","vsw-2ze9gtpk7rgmugk2rphli"]
		createCluster(credential, provider, region, name, vpcId, subnetIds, template string)
```

#### 示例:
``` 
createCluster(credential, provider, region, name, vpcId, subnetIds, template string)
``` 

## createNamespace
#### 方法描述:
``` 
创建命名空间
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		createNamespace(bj_demo_crazywolf, "gjw-0910")

		参数1：集群环境变量
		
		参数2：新命名空间名称
```

#### 示例:
``` 
createNamespace(参数1, 参数2)
``` 

## createNodegroup
#### 方法描述:
``` 
创建nodegoup

		provider： aliyun, aws, huawei
		region: example cn-beijing
		clusterID: 要创建节点组的集群ID
		name: 节点组名字
		odOrSpot: od, spot
		instanceCount:新节点组的节点数量
		instanceTypes: 数组["ecs.n1.medium","ecs.sn1.medium"]
		subnetIDs: 数组["vsw-2zen61tp041lskzzzhukq","vsw-2ze9gtpk7rgmugk2rphli"]
		
		参数会替换模版中相应的字段。 如name参数会替换template中的name字段
```

#### 示例:
``` 
createNodegroup(provider, region, clusterID, name, odOrSpot, instanceCount, instanceTypes, subnetIDs, template)
``` 

## deleteCluster
#### 方法描述:
``` 
删除K8S集群
		credential = "aliCredit"
		provider = "aliyun"// aliyun, aws, huawei
		region = "cn-beijing"
		clusterID = "xxxxx"
		setCredential(credential, "keyid", <<password>>)
		deleteCluster(credential, provider, region, clusterID)
```

#### 示例:
``` 
deleteCluster(credential, provider, region, clusterID)
``` 

## deleteNodegroup
#### 方法描述:
``` 
删除K8S集群的节点组
```

#### 示例:
``` 
deleteNodegroup(credential, provider, region, clusterID, nodegroupID)
``` 

## deleteResource
#### 方法描述:
``` 
创建命名空间
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		deleteResource(bj_demo_crazywolf, "deployment","ngxin-dep-0")

		参数1：集群环境变量

		参数2：资源类型
			deployment
			job
			cronjob
			daemonset
			statefulset
			service
			ingress
			persistentvolumeclaim
			configmap
			secret
			gateway
			namespace
			pod
			horizontalpodautoscaler
			serviceaccount
			replicaset
			poddisruptionbudget
			node
			storageclass
			
		参数3：资源名称
```

#### 示例:
``` 
deleteResource(参数1, 参数2， 参数3)
``` 

## describeResource
#### 方法描述:
``` 
Describe 资源
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		describeResource(bj_demo_crazywolf, "deployment","ngxin-dep-0")

		参数1：集群环境变量

		参数2：资源类型
			deployment
			job
			cronjob
			daemonset
			statefulset
			service
			ingress
			persistentvolumeclaim
			configmap
			secret
			gateway
			namespace
			pod
			horizontalpodautoscaler
			serviceaccount
			replicaset
			poddisruptionbudget
			node
			storageclass
			
		参数3：资源名称
```

#### 示例:
``` 
describeResource(参数1, 参数2， 参数3)
``` 

## detailBundle
#### 方法描述:
``` 
获取bundle详情
```

#### 示例:
``` 
detailBundle(env,bundleId)
``` 

## detailBundleGroup
#### 方法描述:
``` 
获取bundleGroup详情
```

#### 示例:
``` 
detailBundleGroup(teamId,bundleGroupId)
``` 

## detailPod
#### 方法描述:
``` 
获取Pod详情
		detailPod(bj_demo_crazywolf, "my-wordpress-mariadb-0")
		相当于调用detailResource(bj_demo_crazywolf, "deployment", "ngxin-dep-0")
		
		参数0：指定集群环境
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

		参数1：资源类型
		资源为：
			deployment
			job
			cronjob
			daemonset
			statefulset
			service
			ingress
			persistentvolumeclaim
			configmap
			secret
			gateway
			namespace
			pod
			horizontalpodautoscaler
			serviceaccount
			replicaset
			poddisruptionbudget
			node
			storageclass
```

#### 示例:
``` 
detailPod(参数1, 参数2)
``` 

## detailResource
#### 方法描述:
``` 
获取资源详情
		detailResource(bj_demo_crazywolf, "deployment", "ngxin-dep-0")

		参数0：指定集群环境
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

		参数1：资源类型
		资源为：
			deployment
			job
			cronjob
			daemonset
			statefulset
			service
			ingress
			persistentvolumeclaim
			configmap
			secret
			gateway
			namespace
			pod
			horizontalpodautoscaler
			serviceaccount
			replicaset
			poddisruptionbudget
			node
			storageclass

		参数2：资源名称
```

#### 示例:
``` 
detailResource(参数1, 参数2，参数3)
``` 

## exec
#### 方法描述:
``` 
execute  shell cmd and return the output

	arg1:
		string object, executable shell cmds
		example
		exec("ls | grep 'build'")

	return:
		output of shell cmd arg1
```

#### 示例:
``` 
exec( arg1 )
``` 

## execSql
#### 方法描述:
``` 
执行SQL语句
	example 
		host="spotmaxxxxxx.mazonaws.com"
		user="admin"
		password=<<password>>
		port=3306
		dbName="maxcloud_group"
		openMysql(host, port, dbName, user, password)
		sql="select * from db.table where limit 1";
		execSql(sql)
```

#### 示例:
``` 
execSql(参数1)
``` 

## fillTemp
#### 方法描述:
``` 
填充模版

	参数1： 
		模版字符串，待填充字符占位语法同golang
		example
		configStr = “apiVersion: v1
			kind: ConfigMap
			metadata:
			name: myconfigmap-{{.nameSuffix}}
			namespace: crazywolf
			labels:
				app: myapplication
			data:
			data: {{.randData}}”

	参数2：
		HashTable example {"nameSuffix":randStr(6), "randData":randStr(6)}

	返回值：
		变量被替换之后的字符串
```

#### 示例:
``` 
fillTemp( arg1, arg2 )
``` 

## first
#### 方法描述:
``` 
return first element of array

	arg1:  Array

	return null if arg1 is empty array
```

#### 示例:
``` 
first(arg1)
``` 

## fromBase64
#### 方法描述:
``` 
对string进行Base64解码
		fromBase64("bW9idmlzdGE")
		输出 mobvista
```

#### 示例:
``` 
fromBase64(string)
``` 

## getASG
#### 方法描述:
``` 
获取asg
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)

		参数2：云商 aliyun, aws, huawei
		
		参数3：region
		
		参数4：asgName

		getASG("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
getASG(参数1,参数2,参数3,参数4)
``` 

## getAliASG
#### 方法描述:
``` 
获取asg
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName

		getAliASG("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
getAliASG(参数1,参数2,参数3)
``` 

## getAwsASG
#### 方法描述:
``` 
获取asg
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName

		getAwsASG("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
getAwsASG(参数1,参数2,参数3)
``` 

## getClusterKubeConf
#### 方法描述:
``` 
获取集群的kubeConfig
```

#### 示例:
``` 
getClusterKubeConf(credential, provider, region, clusterID)
``` 

## getCreateClusterTemplate
#### 方法描述:
``` 
获取创建集群的模版字符串
	terwayPlugin:
		bool类型, 只对aliyun ACK起作用的参数
		true: 使用terway 网络插件
		false: 使用默认网络插件(Flannel)
```

#### 示例:
``` 
getCreateClusterTemplate(credential, provider)
getCreateClusterTemplate(credential, provider, terwayPlugin)
``` 

## getCreateNodegroupTemplate
#### 方法描述:
``` 
获取创建集群节点组的模版字符串
```

#### 示例:
``` 
getCreateNodegroupTemplate(credential, provider)
``` 

## getHpaCurrent
#### 方法描述:
``` 
获取HPA的 currentReplicas
		参数1：集群环境
		
		参数2：HPA名称
		
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		getHpaCurrent(bj_demo_crazywolf, "gjw-test")
```

#### 示例:
``` 
getHpaCurrent(参数1,参数2)
``` 

## getHpaMax
#### 方法描述:
``` 
获取HPA的maxReplicas
		参数1：集群环境
		
		参数2：HPA名称
		
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		getHpaMax(bj_demo_crazywolf, "gjw-test")
```

#### 示例:
``` 
getHpaMax(参数1,参数2)
``` 

## getHpaMin
#### 方法描述:
``` 
获取HPA的minReplicas
		参数1：集群环境
		
		参数2：HPA名称
		
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		getHpaMin(bj_demo_crazywolf, "gjw-test")
```

#### 示例:
``` 
getHpaMin(参数1,参数2)
``` 

## getHwASG
#### 方法描述:
``` 
获取asg
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName

		getHwASG("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
getHwASG(参数1,参数2,参数3)
``` 

## getUserSecret
#### 方法描述:
``` 
获取签名需要的秘钥
```

#### 示例:
``` 
getUserSecret()
``` 

## getYaml
#### 方法描述:
``` 
创建命名空间
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		getYaml(bj_demo_crazywolf, "deployment","ngxin-dep-0")

		参数1：集群环境变量

		参数2：资源类型
			deployment
			job
			cronjob
			daemonset
			statefulset
			service
			ingress
			persistentvolumeclaim
			configmap
			secret
			gateway
			namespace
			pod
			horizontalpodautoscaler
			serviceaccount
			replicaset
			poddisruptionbudget
			node
			storageclass

		参数3：资源名称
```

#### 示例:
``` 
createNamespace(参数1, 参数2)
``` 

## helmValues
#### 方法描述:
``` 
Helm 查循已安装的Helm列表
		helmValues(bj_demo_crazywolf, "my-wordpress", false)
		
		参数1：集群环境变量

		参数2：releaseName

		参数3：是否展示所有values
```

#### 示例:
``` 
helmValues(参数1, 参数2, 参数3)
``` 

## importCluster
#### 方法描述:
``` 
导入K8S集群到MaxCloud

	teamID:
		数字， 可以使用listTeam()进行查询

	name：
		字符串， 该集群在MaxCloud中的名字
		
	privider:
		字符串， 可以是
		-    ali
		-    aws
		-    tencent
		-    huawei

	region：
		K8S集群所在的地区， example cn-beijing

	k8sConfig:
		K8S集群的链接字符串， 可以使用getClusterKubeConf(credential, provider, region, clusterID)获取

	返回值：
		成功/错误信息
```

#### 示例:
``` 
importCluster(teamID, name, provider, region, k8sConfig)
``` 

## installOrUpgradeChart
#### 方法描述:
``` 
Helm 安装Chart
		sets = {
			"wordpressBlogName" : "CrazyWolf3453456"
			}
		installOrUpgradeChart(bj_demo_crazywolf, "my-wordpress", "bitnami/wordpress", "15.2.5", sets)

		参数1：集群环境变量
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

		参数2：releaseName

		参数3：chart name

		参数4：chart版本

		参数5：sets参数 （可选）
```

#### 示例:
``` 
addOrUpdateRepo(参数1, 参数2, 参数3)
``` 

## isErr
#### 方法描述:
``` 
判断value是不是maxlang的 error对象
```

#### 示例:
``` 
isErr(value)
``` 

## jpath
#### 方法描述:
``` 
query the json string and return target value 

	arg1:
		string type path e.g "." to match the root element

	arg2:
		the valid json string to query

	return:
		element(s) in the specified path
```

#### 示例:
``` 
jpath( arg1, arg2 )
``` 

## keys
#### 方法描述:
``` 
get keys of HashTable as array

	arg1:
		HashTable object
		example 
		dic = {1:"one","one":1,"inc":fn(x){x+1}, "arr":[1,2,3,5], "table":{2:"two","sub":fn(x){x-1}}}

	return:
		keys as array of the HashTable
		example [1,"one", "inc","arr","table"]
```

#### 示例:
``` 
keys( arg1 )
``` 

## last
#### 方法描述:
``` 
return last element of array

	arg1: Array

	return null if arg1 is empty array
```

#### 示例:
``` 
last(arg1)
``` 

## len
#### 方法描述:
``` 
return the length of arg for following data types
	Array:
		element count of inthe array

	String:
		the length of string

	Default:
		return argument error
```

#### 示例:
``` 
len(<string/array>) number
``` 

## listASGs
#### 方法描述:
``` 
查询ASG(s)
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)

		参数2：云商 aliyun, aws, huawei
		
		参数3：region
		
		参数4：asgName （可选）

		setCredential("credential", "key_xxxxxx", <<password>>)
		listASGs("credential", "us-west-2")
		listASGs("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
listAliASGs(参数1,参数2,参数3)
listAliASGs(参数1,参数2,参数3,参数4)
``` 

## listAliASGs
#### 方法描述:
``` 
查询ASG(s)
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName （可选）

		setCredential("credential", "key_xxxxxx", <<password>>)
		listAliASGs("credential", "us-west-2")
		listAliASGs("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
listAliASGs(参数1,参数2)
listAliASGs(参数1,参数2,参数3)
``` 

## listAwsASGs
#### 方法描述:
``` 
查询ASG(s)
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName （可选）

		setCredential("credential", "key_xxxxxx", <<password>>)
		listAwsASGs("credential", "us-west-2")
		listAwsASGs("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
listAwsASGs(参数1,参数2)
listAwsASGs(参数1,参数2,参数3)
``` 

## listBucket
#### 方法描述:
``` 
列出Buckets
		参数1：credential 请先试用setCredential(name, key, value)设置
		参数2：云商provider aliyun、aws、huawei
		参数3：endpoint(aliyun的时候必传)
```

#### 示例:
``` 
listBucket(参数1,参数2,参数3)
``` 

## listBucketFile
#### 方法描述:
``` 
列出Bucket的文件
		参数1：credential 请先试用setCredential(name, key, value)设置
		参数2：云商provider aliyun、aws、huawei
		参数3：bucketName
		参数4：前缀 Prefix
		参数5：endpoint(aliyun的时候必传)
```

#### 示例:
``` 
listBucketFile(参数1,参数2,参数3,参数4,参数5)
``` 

## listBundleGroup
#### 方法描述:
``` 
获取BundleGroup列表
```

#### 示例:
``` 
listBundleGroup(teamId,page,page_size)
``` 

## listCluster
#### 方法描述:
``` 
列出MaxCloud项目组的项目

	参数1:
		数字，项目组ID， 登陆后使用listTeam()进行查询

	参数2:
		数字，项目ID， 登陆后使用listProject(teamID)进行查询

	返回值：
		项目相关的K8S集群列表
```

#### 示例:
``` 
listCluster(arg1， arg2)
``` 

## listClusters
#### 方法描述:
``` 
查寻K8S集群
		credential = "aliCredit"
		provider = "aliyun"// aliyun, aws, huawei
		region = "cn-beijing"
		setCredential(credential, "keyid", <<password>>)
		clusters = listClusters(credential, provider, region)
```

#### 示例:
``` 
createCluster(credential, provider, region, name)
``` 

## listECSInstanceTypes
#### 方法描述:
``` 
查询该region可创建的机型

		nodeTypes是类似的查询CPU、内存的结构
		[{"type":"general","configuration":{"cpu":2,"mem":4}},{"type":"general","configuration":{"cpu":4,"mem":8}}]
```

#### 示例:
``` 
listECSInstanceTypes(credential, provider, region, subnetZones, nodeTypeQuery)
``` 

## listHelmReleases
#### 方法描述:
``` 
Helm 查循已安装的Helm列表
		listHelmReleases(bj_demo_crazywolf)

		参数1：集群环境变量
```

#### 示例:
``` 
listHelmReleases(参数1)
``` 

## listHwASGs
#### 方法描述:
``` 
查询ASG(s)
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName （可选）

		setCredential("credential", "key_xxxxxx", <<password>>)
		listHwASGs("credential", "us-west-2")
		listHwASGs("credential", "us-west-2", "asgName")
```

#### 示例:
``` 
listHwASGs(参数1,参数2)
listHwASGs(参数1,参数2,参数3)
``` 

## listNodeGroupNodes
#### 方法描述:
``` 
查询集群的Nodegroup
```

#### 示例:
``` 
listNodegroups(credential, provider, region, clusterID)
``` 

## listNodegroups
#### 方法描述:
``` 
查询K8S集群的节点组
```

#### 示例:
``` 
listNodegroups(credential, provider, region, clusterID)
``` 

## listPod
#### 方法描述:
``` 
指定资源类型后可以获取上面指定集群命名空间下的所有资源 
		可以只传入一个类型参数， 相当于listResource(bj_demo_crazywolf, "pod")
		example
			ListPod(bj_demo_crazywolf)
			
	参数1：
		集群环境变量
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
```

#### 示例:
``` 
ListPod(参数1, 参数2)
``` 

## listProject
#### 方法描述:
``` 
列出MaxCloud项目组的项目

	arg1:
		项目组ID， 登陆后使用listTeam()进行查询

	返回值：
		项目名字、用户组和项目ID列表
```

#### 示例:
``` 
listProject(arg1)
``` 

## listResource
#### 方法描述:
``` 
指定资源类型后可以获取上面指定集群命名空间下的所有资源 
		可以只传入一个类型参数，也可以传入第二个参数作为临时命名空间（不会覆盖之前useCluster设置的命名空间）
		example
			listResource(bj_demo_crazywolf, "deployment")

	参数1：
		集群环境变量
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

	参数2：
		资源类型
		目前支持的资源为：
			
			deployment
			job
			cronjob
			daemonset
			statefulset
			service
			ingress
			persistentvolumeclaim
			configmap
			secret
			gateway
			namespace
			pod
			horizontalpodautoscaler
			serviceaccount
			replicaset
			poddisruptionbudget
			node
			storageclass
```

#### 示例:
``` 
listResource(参数1, 参数2)
``` 

## listSubnets
#### 方法描述:
``` 
查询已有的subnets
		credential = "aliCredit"
		provider = "aliyun"// aliyun, aws, huawei
		region = "cn-beijing"
		vpcID = "xxxdfsdfsdf"	
		setCredential(credential, "keyid", <<password>>)
		subnets = listSubnets(credential, provider, region, vpcID)
		subnets[0]
		+-----------------------------------------------+
		| Summary                                       |
		+----------+---------------------------+--------+
		| NAME     | ID                        | TYPE   |
		+----------+---------------------------+--------+
		| vswitch2 | vsw-2zeiz27mngyi7jxnotu5f | subnet |
		| vswitch1 | vsw-2zeu4oq1vx9ffjso35sde | subnet |
		+----------+---------------------------+--------+
```

#### 示例:
``` 
listSubnets(credential, provider, region, vpcID)
``` 

## listTeam
#### 方法描述:
``` 
列出用户有权限的MaxCloud 组

	返回值：
		项目组名字和ID列表
```

#### 示例:
``` 
listTeam()
``` 

## listVPCs
#### 方法描述:
``` 
查看现有VPCs
		credential = "aliCredit"
		provider = "aliyun"// aliyun, aws, huawei
		region = "cn-beijing"
		vpcName = "test"	
		setCredential(credential, "keyid", <<password>>)
		listVPCs(credential, provider, region) // 查询region里所有的VPC
		listVPCs(credential, provider, region, vpcName) // 查询名字是vpcName， 在region的VPC

		vpcs = listVPCs(credential, provider, region)
		vpcs[0]

		testVPC = listVPCs(credential, provider, region, vpcName)
		vpcID = testVPC[1]["ID"]
		vpcID

	返回数组类型，
		
		数组第一个元素是Summary列表
		数组第2个元素开始是相应的Object， 可以进行操作
```

#### 示例:
``` 
listVPCs(credential, provider, region)
		listVPCs(credential, provider, region, vpcName)
``` 

## listZones
#### 方法描述:
``` 
查看现有Zones
		credential = "aliCredit"
		provider = "aliyun"// aliyun, aws, huawei
		region = "cn-beijing"
		vpcName = "test"	
		setCredential(credential, "keyid", <<password>>)
		listZones(credential, provider, region) 
		
	返回数组类型，
		
		数组第一个元素是Summary列表
		数组第2个元素开始是相应的Object， 可以进行操作
```

#### 示例:
``` 
listZones(credential, provider, region)
``` 

## lockASG
#### 方法描述:
``` 
锁定ASG容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：云商 aliyun, aws, huawei

		参数3：region
		
		参数4：asgName
		
		参数5：锁定值
		
		如果参数4锁定值小于1，则最小值会被修改为当前的期望值 
		如果参数4大于最大值，则最大值会被修改为锁定值 
		如果期望值小于参数4锁定值，则期望值修改为所定值

		lockASG("credential", "us-west-2", "asgName", 10)
```

#### 示例:
``` 
lockASG(参数1,参数2,参数3,参数4,参数5)
``` 

## lockAliASG
#### 方法描述:
``` 
锁定ASG容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName
		
		参数4：锁定值
		
			如果参数4锁定值小于1，则最小值会被修改为当前的期望值 
			如果参数4大于最大值，则最大值会被修改为锁定值 
			如果期望值小于参数4锁定值，则期望值修改为所定值
		lockAliASG("credential", "us-west-2", "asgName", 10)
```

#### 示例:
``` 
lockAliASG(参数1,参数2,参数3,参数4)
``` 

## lockAwsASG
#### 方法描述:
``` 
锁定ASG容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName
		
		参数4：锁定值
		
		如果参数4锁定值小于1，则最小值会被修改为当前的期望值 如果参数4大于最大值，则最大值会被修改为锁定值 如果期望值小于参数4锁定值，则期望值修改为所定值
		lockAwsASG("credential", "us-west-2", "asgName", 10)
```

#### 示例:
``` 
lockAwsASG(参数1,参数2,参数3,参数4)
``` 

## lockHpa
#### 方法描述:
``` 
锁定HPA
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		lockHpa(bj_demo_crazywolf, "gjw-test", 1)

		参数1：当前集群环境 
		参数2：HPA 名称 
		参数3：minReplicas

		设置minReplicas值，默认MaxReplicas不变，
		如果当前MaxReplicas小于要设置的minReplicas则修改 MaxReplicas为minReplicas一样 

		例如：
			demo-hap
			minReplicas: 2
			maxReplicas: 5
			调用 localHpa(env, "demo-hpa", 3)，锁定为3则执行后结果为

			demo-hap
			minReplicas: 3
			maxReplicas: 5
			如果再次调用调用 localHpa(env, "demo-hpa", 10)，锁定为10则执行后结果为

			demo-hap
			minReplicas: 10
			maxReplicas: 10
```

#### 示例:
``` 
lockHpa(参数1, 参数2， 参数3)
``` 

## lockHwASG
#### 方法描述:
``` 
锁定ASG容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName
		
		参数4：锁定值
		
		如果参数4锁定值小于1，则最小值会被修改为当前的期望值 
		如果参数4大于最大值，则最大值会被修改为锁定值 
		如果期望值小于参数4锁定值，则期望值修改为所定值

		lockHwASG("credential", "us-west-2", "asgName", 10)
```

#### 示例:
``` 
lockHwASG(参数1,参数2,参数3,参数4)
``` 

## loginMaxcloud
#### 方法描述:
``` 
登陆MaxCloud

	参数1： 
		配置名字， 搭配以下函数使用
		setCredential("maxcloudab", "username", <<password>>)
		updateCredential("awsCredential", "key_xxxxxx", <<password>>)
		example
		loginMaxcloud("maxcloudab")

	返回值：
		TRUE/ error Object
```

#### 示例:
``` 
loginMaxcloud( arg1 )
``` 

## mock_print
#### 方法描述:
``` 
测试表格打印
```

#### 示例:
``` 
mock_print()
``` 

## mock_print
#### 方法描述:
``` 
测试表格打印
```

#### 示例:
``` 
mock_print()
``` 

## newBucketDir
#### 方法描述:
``` 
新建Bucket的文件“
		参数1：credential  请先试用setCredential(name, key, value)设置
		参数2：云商provider aliyun、aws、huawei
		参数3：bucketName
		参数4：dirName
		参数5：endpoint(aliyun的时候必传)
```

#### 示例:
``` 
newBucketDir(参数1,参数2,参数3,参数4,参数5)
``` 

## nslookup
#### 方法描述:
``` 
解析域名
		根据给定域名解析出IP或CName， 同时查找Aws Route53 对 A 类型的别名进行查找
		
		使用方式：
		nslookup(credential, "data.mintegral.com.")
		example
		Route53 中 的一条记录如下， 正常的nslookup无法返回dualstack.....这个域名， 因为Route53并不是标准的DNS服务器
		
		de01.mintegral.com    A    简单    - dualstack.adn-tktracking-frankfurt-13341082.eu-central-1.elb.amazonaws.com.
		detailroi.mintegral.com    A    简单    -    47.93.30.190
		使用Playbook中的nslookup会返回如下结果
		
		[
		de01.mintegral.com. in A NAME: 3.67.205.211, 
		de01.mintegral.com. in A NAME: 18.198.96.205, 
		de01.mintegral.com. in A NAME: 3.126.117.230, 
		de01.mintegral.com. in A NAME: 3.65.53.117, 
		de01.mintegral.com. in A NAME: 18.184.234.38, 
		de01.mintegral.com. in A NAME: 3.125.187.240, 
		de01.mintegral.com. in A NAME: 3.120.59.220, 
		de01.mintegral.com. in A NAME: 3.120.47.234, 
		======records from aws route53=====, 
		de01.mintegral.com. A   dualstack.adn-tktracking-frankfurt-13341082.eu-central-1.elb.amazonaws.com.
		]
```

#### 示例:
``` 
nslookup(credential, "data.mintegral.com.")
``` 

## ntos
#### 方法描述:
``` 
conver number to string 

	arg1:
		number object

	return:
		string format of the number object
```

#### 示例:
``` 
ntos( arg1 )
``` 

## openMysql
#### 方法描述:
``` 
打开数据库连接
	example 
		host="spotmaxxxxxx.mazonaws.com"
		user="admin"
		password=<<password>>
		port=3306
		dbName="maxcloud_group"
		openMysql(host, port, dbName, user, password)
		sql="select * from db.table where limit 1";
		execSql(sql)
```

#### 示例:
``` 
execSql(参数1)
``` 

## podExecShell
#### 方法描述:
``` 
在pod里面执行shell
```

#### 示例:
``` 
podExecShell(env,"podName","container",["sh","-c","ls -al"])
``` 

## print
#### 方法描述:
``` 
output the args to Stdout

	arg1, .....:
		0 or more element to output

	return:
		the print output string
```

#### 示例:
``` 
print(arg1, ....)
``` 

## print_bundle_group
#### 方法描述:
``` 
根据团队ID打印bundleGroup列表
```

#### 示例:
``` 
print_bundle_group(teamId)
``` 

## print_bundle_group
#### 方法描述:
``` 
根据团队ID打印bundleGroup列表
```

#### 示例:
``` 
print_bundle_group(teamId)
``` 

## print_bundle_group_by_plan
#### 方法描述:
``` 
基于伸缩计划，进行伸缩
```

#### 示例:
``` 
print_bundle_group_by_plan(plan)
``` 

## print_bundle_group_by_plan
#### 方法描述:
``` 
基于伸缩计划，进行伸缩
```

#### 示例:
``` 
print_bundle_group_by_plan(plan)
``` 

## print_bundle_group_health
#### 方法描述:
``` 
根据团队ID和BundleGroupId打印链路监控状态
```

#### 示例:
``` 
print_bundle_group_health({"team_id":3,"bundle_group_id":7})
``` 

## print_bundle_group_health
#### 方法描述:
``` 
根据团队ID和BundleGroupId打印链路监控状态
```

#### 示例:
``` 
print_bundle_group_health({"team_id":3,"bundle_group_id":7})
``` 

## print_teams
#### 方法描述:
``` 
打印团队列表
```

#### 示例:
``` 
print_teams()
``` 

## print_teams
#### 方法描述:
``` 
打印团队列表
```

#### 示例:
``` 
print_teams()
``` 

## println
#### 方法描述:
``` 
output the args to Stdout with newline at the end

	arg1, .....:
		0 or more element to output

	return:
		the print output string with new line at the end
```

#### 示例:
``` 
println(arg1, ....)
``` 

## push
#### 方法描述:
``` 
append arg2 to array arg1 return the new array

	arg1:
		Array to append element

	arg2:
		element to append to the array

	return:
		the new array
```

#### 示例:
``` 
rest(arg1, arg2)
``` 

## put
#### 方法描述:
``` 

```

#### 示例:
``` 

``` 

## randStr
#### 方法描述:
``` 
generate random string with length = arg1

	arg1:
		number object, length of random string
		example 
		randStr(6)

	return:
		output the generated string
```

#### 示例:
``` 
randStr( arg1 )
``` 

## rest
#### 方法描述:
``` 
return last element of array

	arg1: Array
	return null if arg1 element count <= 1
```

#### 示例:
``` 
rest(arg1)
``` 

## scaleDeployment
#### 方法描述:
``` 
Scale Deployment
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		scaleDeployment(bj_demo_crazywolf, "ngxin-dep-0", 1)

		参数1：集群环境变量

		参数2：Deployment 名称

		参数3： Replicas 数量
```

#### 示例:
``` 
scaleDeployment(参数1, 参数2， 参数3)
``` 

## scaleNodeGroup
#### 方法描述:
``` 
Scale nodegroup机器数量

		scaleNodeGroup(credential, provider, region, clusterID, nodeGroupID, newSize)
		
		也可以使用一下ASG参数进行操作
		
		listAliASGs(credential, region)
		
		updateAliASG(credential, "us-west-2", "kmax-demo-asg-small", 2, 2, 2)
		
		lockAliASG(credential, "us-west-2"，"asgName"，10)
		
		具体使用方法见 MaxLang MaxCloud.ipynb
```

#### 示例:
``` 
scaleNodeGroup(credential, provider, region, clusterID, nodegroupID, newSize)
``` 

## scaleStatefulset
#### 方法描述:
``` 
Scale Statefulset
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		scaleStatefulset(bj_demo_crazywolf, "xxxx", 2)

		参数1：集群环境变量

		参数2：Deployment 名称

		参数3： Replicas 数量
```

#### 示例:
``` 
scaleStatefulset(参数1, 参数2， 参数3)
``` 

## setCredential
#### 方法描述:
``` 
新增Credential
		setCredential(name, key, value)
		
		参数1：credential 唯一名称
		
		参数2：credential key，如果是Aws credential则为 aws_access_key_id
		
		参数3：credential value，如果是Aws credential则为 aws_secret_access_key
		
		PS：不能重复设置，如需修改请使用updateCredential
```

#### 示例:
``` 
setCredential(name, key, value)
``` 

## setHpaReplicas
#### 方法描述:
``` 
锁定HPA
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}
		setHpaReplicas(bj_demo_crazywolf, "gjw-test", 1, 2)

		参数1：当前集群环境 
		参数2：HPA名称
		参数3：minReplicas
		参数4：maxReplicas
```

#### 示例:
``` 
lockHpa(参数1, 参数2, 参数3, 参数4)
``` 

## sharePlaybook
#### 方法描述:
``` 
分享Playbook 文件给其他人
		sharePlaybook("filename") && sharePlaybook("filename","user@mobvista.com")
		参数1：文件名
		参数2：用户 (可选，如果不填则公开给所有MaxCloud用户)
```

#### 示例:
``` 
sharePlaybook("filename") && sharePlaybook("filename","user@mobvista.com")
``` 

## sleep
#### 方法描述:
``` 
等待N秒
		sleep(second)
		
		参数1：休眠秒数
```

#### 示例:
``` 
sleep(second)
``` 

## ston
#### 方法描述:
``` 
conver string to number 

	arg1:
		string object

	return:
		number object of the input string
		or
		error object
```

#### 示例:
``` 
ston( arg1 )
``` 

## syncPlaybook
#### 方法描述:
``` 
同步所有公共PlayBook 和 分享个给我的PlayBook
```

#### 示例:
``` 
syncPlaybook()
``` 

## toBase64
#### 方法描述:
``` 
对string进行Base64编码
		toBase64("mobvista")
		输出 bW9idmlzdGE
```

#### 示例:
``` 
toBase64(string)
``` 

## toJson
#### 方法描述:
``` 
把Maxlang Map/Array 对象转换成Json

		mapObj = {
			"name" : "CrazyWolf",
			"age" : 18,
			"address" : "beiijng"
		}
		toJson(mapObj)

		arrayObj = [1, true, "stringObj"]
		toJson(arrayObj)
```

#### 示例:
``` 
toJson(参数1)
``` 

## trigger
#### 方法描述:
``` 
如果您需要外部触发执行某个PlayBook脚本，可以执行 trigger 方法把PlayBook文件公布为可外部触发的，然后按照输出提示触发执行
```

#### 示例:
``` 
trigger("filename")
``` 

## uninstallReleaseByName
#### 方法描述:
``` 
Helm 卸载Release

		参数1：指定集群环境
		example bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

		参数2：ReleaseName
```

#### 示例:
``` 
uninstallReleaseByName(参数1, 参数2)
``` 

## updateASG
#### 方法描述:
``` 
更改ASG的最小容量、最大容量、所需容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)

		参数2：云商 aliyun, aws, huawei
		
		参数3：region
		
		参数4：asgName
		
		参数5：最小
		
		参数6：最大
		
		参数7：期望值
		
		updateASG("credential", "us-west-2", "asgName" ,1, 100, 50)
```

#### 示例:
``` 
updateASG(参数1,参数2,参数3,参数4,参数5,参数6,参数7)
``` 

## updateAliASG
#### 方法描述:
``` 
更改ASG的最小容量、最大容量、所需容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName
		
		参数4：最小
		
		参数5：最大
		
		参数6：期望值
		
		updateAliASG("credential", "us-west-2", "asgName", 1, 100, 50)
```

#### 示例:
``` 
updateAliASG(参数1,参数2,参数3,参数4,参数5,参数6)
``` 

## updateAwsASG
#### 方法描述:
``` 
更改ASG的最小容量、最大容量、所需容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName
		
		参数4：最小
		
		参数5：最大
		
		参数6：期望值
		
		updateAwsASG("credential", "us-west-2", "asgName", 1, 100, 50)
```

#### 示例:
``` 
updateAwsASG(参数1,参数2,参数3,参数4,参数5,参数6)
``` 

## updateCredential
#### 方法描述:
``` 
修改Credential
		updateCredential(name, key, value)
		
		参数1：credential 唯一名称
		
		参数2：credential key，如果是Aws credential则为 aws_access_key_id
		
		参数3：credential value，如果是Aws credential则为 aws_secret_access_key
```

#### 示例:
``` 
updateCredential(name, key, value)
``` 

## updateHwASG
#### 方法描述:
``` 
更改ASG的最小容量、最大容量、所需容量
		参数1：云商credential ，请先试用setCredential(name, key, value 设置)
		
		参数2：region
		
		参数3：asgName
		
		参数4：最小
		
		参数5：最大
		
		参数6：期望值
		
		updateHwASG("credential", "us-west-2", "asgName" ,1, 100, 50)
```

#### 示例:
``` 
updateHwASG(参数1,参数2,参数3,参数4,参数5,参数6)
``` 

## useCluster
#### 方法描述:
``` 
切换操作上下文到MaxCloud集群

	参数1:
		HashTable，可以从MaxCloud项目管理页面复制
		bj_demo_crazywolf = {
			"teamId":1,
			"projectId":79, 
			"clusterId":69, 
			"namespace":"crazywolf"
		}

	返回值：
		TRUE/错误信息
```

#### 示例:
``` 
useCluster(arg1)
``` 

## values
#### 方法描述:
``` 
get values of HashTable as array

	arg1:
		HashTable object
		example 
		dic = {1:"one","one":1,"inc":fn(x){x+1}, "arr":[1,2,3,5], "table":{2:"two","sub":fn(x){x-1}}}

	return:
		keys as array of the HashTable
		example ["one", 1, fn(x){x+1}, [1,2,3,5], {2:"two","sub":fn(x){x-1}}]
```

#### 示例:
``` 
values( arg1 )
``` 


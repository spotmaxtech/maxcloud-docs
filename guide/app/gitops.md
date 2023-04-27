---
sidebarDepth: 2
---

## 使用GitOps功能与jenkins集成完成自动部署

进入”应用个管理“， 找到Website bundle 点击 ”Gitops“

![gitopsButton.png](../../images/app/gitopsButton.png)

点击”Resource“选择要用Gitops方式控制部署的资源

![gitops_chooseresource.png](../../images/app/gitops_chooseresource.png)

MaxCloud会自动生成curl格式的发布示例

![gitops_publish.png](../../images/app/gitops_publish.png)

和进度查询示例

![gitops_progress.png](../../images/app/gitops_progress.png)

可以使用jenkins等CI/CD工具， 集成部署过程
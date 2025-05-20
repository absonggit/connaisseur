## CONNAISSEUR - 验证 Kubernetes 中的容器镜像签名

Kubernetes 的准入控制器将容器镜像签名验证和信任固定集成到集群中，以确保仅部署有效的镜像 - 简单、灵活、安全。

## Connaisseur 是什么？

Connaisseur 确保 Kubernetes 集群中容器镜像的完整性和来源真实性。
为此，它会拦截发送到 Kubernetes 集群的资源创建或更新请求，识别所有容器镜像，并根据预先配置的公钥验证其签名。
根据验证结果，它会接受或拒绝这些请求。

要了解有关 Connaisseur 的更多信息，请访问[完整文档](https://sse-secure-systems.github.io/connaisseur/)。


## 开始使用

首先，在本地添加 Connaisseur [Helm](https://helm.sh/) 存储库

```console
helm repo add connaisseur https://sse-secure-systems.github.io/connaisseur/charts
```

然后安装 Connaisseur Helm chart：

```console
helm install connaisseur connaisseur/connaisseur --atomic --create-namespace --namespace connaisseur
```

Connaisseur 的默认配置包含 Docker 官方镜像的公共根密钥，因此运行像 `hello-world` 这样的官方 Docker 镜像应该会成功

```console
kubectl run hello-world --image=docker.io/hello-world
```

因为 Connaisseur 将成功验证 `hello-world` 图像与预配置公钥的签名，同时运行没有任何签名的图像

```
kubectl run unsigned --image=docker.io/securesystemsengineering/testimage:unsigned
```
或者运行签名与固定根密钥不匹配的图像将会失败。

```
kubectl run foreignsignature --image=bitnami/postgresql
```

##讨论、支持和反馈
我们希望以社区需求为导向，推动 Connaisseur 的开发，期待您的反馈，如果您需要支持，我们很乐意为您提供帮助！欢迎通过 [GitHub 讨论区](https://github.com/sse-secure-systems/connaisseur/discussions) 与我们联系。

## 联系

您可以通过电子邮件 [connaisseur@securesystems.dev](mailto:connaisseur@securesystems.dev) 联系我们。

## CONNAISSEUR - 验证 Kubernetes 中的容器镜像签名

Kubernetes 的准入控制器将容器镜像签名验证和信任固定集成到集群中，以确保仅部署有效的镜像 - 简单、灵活、安全。

## Connaisseur 是什么？

Connaisseur 确保 Kubernetes 集群中容器镜像的完整性和来源真实性。
为此，它会拦截发送到 Kubernetes 集群的资源创建或更新请求，识别所有容器镜像，并根据预先配置的公钥验证其签名。
根据验证结果，它会接受或拒绝这些请求。

要了解有关 Connaisseur 的更多信息，请访问[完整文档](https://sse-secure-systems.github.io/connaisseur/)。


## Get started

To get started, locally add the Connaisseur [Helm](https://helm.sh/) repository 

```console
helm repo add connaisseur https://sse-secure-systems.github.io/connaisseur/charts
```

and install the Connaisseur Helm chart from there:

```console
helm install connaisseur connaisseur/connaisseur --atomic --create-namespace --namespace connaisseur
```

The default configuration of Connaisseur holds the public root key for [Docker official images](https://docs.docker.com/docker-hub/official_images/), so running such an official Docker image like the `hello-world` should succeed

```console
kubectl run hello-world --image=docker.io/hello-world
```

as Connaisseur will successfully validate the signature of the `hello-world` image against the pre-configured public key, while running an image without any signature

```
kubectl run unsigned --image=docker.io/securesystemsengineering/testimage:unsigned
```
or running an image with a signature not matching (one of) the pinned root keys

```
kubectl run foreignsignature --image=bitnami/postgresql
```

will fail.

## Discussions, support & feedback
We hope to steer development of Connaisseur from demand of the community, are excited about your feedback and happy to help if you need support! So feel free to connect with us via [GitHub Discussions](https://github.com/sse-secure-systems/connaisseur/discussions).

## Contact

You can reach us via email under [connaisseur@securesystems.dev](mailto:connaisseur@securesystems.dev).

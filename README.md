# KubeSDW

Kubernetes Deployment Solution for Stable Diffusion Web UI

这个项目是为了快速将 stable-diffusion-webui 项目 [https://github.com/AUTOMATIC1111/stable-diffusion-webui/master]() 部署到集群中，以方便使用虚拟GPU进行配额。

## 快速入门

第一步：克隆 stable-diffusion-webui 项目到本地目录；

```sh
git clone https://github.com/AUTOMATIC1111/stable-diffusion-webui.git
```

第二步：将本项目中的 Dockerfile 移动到 stable-diffusion-webui 项目中；

```sh
mv KubeSDW/dockerfile/Dockerfile stable-diffusion-webui/
```

第三步：制作Docker镜像；

```sh
cd stable-diffusion-webui/
docker build -t stable-diffusion-webui:v1.10.0 .
```

第四步：部署，可以选择deployment或者Helm中的任一方式；

```sh
kubectl create ns stable-diffusion
cd KubeSDW/deployments/
kubectl create -f pvc.yaml 
kubectl create -f deployment -f service.yaml
```
或者
```sh
cd KubeSDW/helm-charts/
helm install sd-webui . -n stable-diffusion
```
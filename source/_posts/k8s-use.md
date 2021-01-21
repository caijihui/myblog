---
title: k8s-use
date: 2021-01-07 10:31:59
tags:
---

## 操作

#### mac 开启k8

## 配置config map
 - 把配置文件放在config 目录下
kubectl create configmap test-conf --from-file=config -n test

## deployment
 创建- 搞好配置

## 暴露 expose 创建了service
kubectl expose deployment test --port=80 --target-port=80 -n test

或
kubectl expose deployment hello-world --type=LoadBalancer --name=my-service

## 映射本地 端口
kubectl port-forward services/test 10080:80 -n test

通过端口映射就能访问。
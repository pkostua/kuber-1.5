# Решение домашнего задания к занятию «Сетевое взаимодействие в K8S. Часть 2»
https://github.com/netology-code/kuber-homeworks/blob/main/1.5/1.5.md
## Задание 1. Создать Deployment приложений backend и frontend
### 1. Deployment приложения frontend
```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: depl-front
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:1.24.0
          ports:
            - name: http-nginx
              containerPort: 80
```
### 2. Deployment приложения backend
```
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: depl-back
spec:
  replicas: 1
  selector:
    matchLabels:
      app: multitool
  template:
    metadata:
      labels:
        app: multitool
    spec:
      containers:
        - name: multitool
          image: praqma/network-multitool:alpine-extra
          env:
            - name: HTTP_PORT
              value: "8080"
          ports:
            - name: http-multitool
              containerPort: 8080
              protocol: TCP

```
### 3. Манифест сервисов
```
---
apiVersion: v1
kind: Service
metadata:
  name: svc-front
spec:
  selector:
    app: nginx
  type: ClusterIP
  ports:
    - name: nginx
      port: 80
      targetPort: http-nginx
```
```
---
apiVersion: v1
kind: Service
metadata:
  name: svc-back
spec:
  selector:
    app: multitool
  type: ClusterIP
  ports:
    - name: multitool
      port: 80
      targetPort: http-multitool
```
### 4. Проверка связи
![image](https://github.com/user-attachments/assets/14a73076-6389-4d76-8f3e-19d2ddc88b47)

## Задание 2. Создать Ingress и обеспечить доступ к приложениям снаружи кластера
### 1. Включение Ingress-controller в MicroK8S.
![image](https://github.com/user-attachments/assets/52fcf2a1-416c-41c7-94b4-30193df016c1)
### 2. Манифетс Ingress
### 3. Проверка связи




# Демонстрація встановлення ArgoCD на локальний кластер `minikube`
[![asciicast](https://asciinema.org/a/653598.svg)](https://asciinema.org/a/653598)


Встановити ArgoCD:
```sh
$ minikube start

$ kubectl create namespace argocd

$ kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Отримати пароль до ArgoCD UI:
```sh
$ kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```

Ще один спосіб отримати пароль до ArgoCD UI:
```sh
$ kubectl -n argocd get po
NAME                                                READY   STATUS    RESTARTS   AGE
argocd-application-controller-0                     1/1     Running   0          2m9s
argocd-applicationset-controller-6c8fbc69b5-zqdrb   1/1     Running   0          2m9s
argocd-dex-server-59bd76d76-zd4lr                   1/1     Running   0          2m9s
argocd-notifications-controller-6b66d47b45-6njrs    1/1     Running   0          2m9s
argocd-redis-66d9777b78-lh7mp                       1/1     Running   0          2m9s
argocd-repo-server-b9957974f-d6t82                  1/1     Running   0          2m9s
argocd-server-5d8d58455f-fdrpv                      1/1     Running   0          2m9s


$ kubectl exec --stdin --tty argocd-server-5d8d58455f-fdrpv -n argocd -- /bin/bash

argocd@argocd-server-5d8d58455f-fdrpv:~$ argocd admin initial-password -n argocd
MHFJEmoz6lGcfPii

 This password must be only used for first time login. We strongly recommend you update the password using `argocd account update-password`.
```

Прокинути порт ArgoCD серверу на локальний інтерфейс:
```sh
$ kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Тепер ArgoCD UI буде доступний за адресою https://localhost:8080. 

```
User: admin
Password: <password>
```

# Порівняння інструментів для запуску локального кластеру Kubernetes

## minikube
Minikube - інструмент, який дозволяє запустити Kubernetes кластер з однієї ноди у віртуальній машині на персональному комп'ютері.


### Pros
- Легко працювати з віддаленими registry з приватним доступом (за допомогою плагінів).
- Можна задати специфічну версію Kubernetes API.
- Підтримує кілька рантаймів (containerd, cri-o, docker).
- В якості драйвера може використовуватись Podman, але його підтримка наразі в експериментальній стадії.

### Cons
- Споживання ресурсів найбільше серед конкурентів


## K3d
k3d is a lightweight wrapper to run k3s (Rancher Lab’s minimal Kubernetes distribution) in docker.

k3d makes it very easy to create single- and multi-node k3s clusters in docker, e.g. for local development on Kubernetes.


### Pros
- Конфігурація кластера зберігається в конфігу. Можна зберігати у VCS і відтворити точні налаштування кластеру на інших машинах.
- В якості драйвера може використовуватись Podman, але його підтримка наразі в експериментальній стадії.
- Ощадливе споживання ресурсів.
- Підходить для IoT.

### Cons
- Щоб працювати з аутентифікацією для віддалених registry, треба розібратись з налаштуваннями.
- Підтримує тільки один рантайм -- docker.

## kind
TODO

## Висновки
TODO

## Демонстрація

Я продемонструю роботу локального кластера і запущу на ньому додаток [pbitty/hello-from](https://hub.docker.com/r/pbitty/hello-from).

Створено на основі туторіалу з документації `minikube` [Using Multi-Node Clusters](https://minikube.sigs.k8s.io/docs/tutorials/multi_node/)

[![asciicast](https://asciinema.org/a/j98S4TD9TP19ceXXhX4y38h7e.svg)](https://asciinema.org/a/j98S4TD9TP19ceXXhX4y38h7e)

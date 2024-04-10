# Порівняння інструментів для запуску локального кластеру Kubernetes

|                                     | minikube                                                                                                                | kind                                                                       | k3d                                                               |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Підтримка ОС                        | Linux, macOS, Windows                                                                                                   | Linux, macOS and Windows                                                   | Linux, macOS, Windows                                             |
| Підтримка архітектур                | x86-64, ARM64, ARMv7, ppc64, S390x                                                                                      | x86_64, ARM64                                                              | x86_64, ARM                                                       |
| Стабільна версія                    | так, v1.32.0                                                                                                            | нижче першої версії, v0.22.0                                               | так, v5.6.2                                                       |
| GiHub Actions                       | так, https://github.com/minikube-ci/examples                                                                            | так, https://github.com/kind-ci/examples                                   | так, https://github.com/nolar/setup-k3d-k3s                       |
| Podman Driver                       | experimental support                                                                                                    | так                                                                         | experimental support                                              |
| Документація                        | ок, досить детальна                                                                                                     | не завжди повна і актуальна, є список посилань на зовнішні ресурси https://kind.sigs.k8s.io/docs/user/resources/ | ок                                                                |
| Supported Runtimes                  | containerd, cri-o, docker                                                                                               | docker                                                                     | docker                                                            |
| Multi-node Cluster support          | так                                                                                                                     | так                                                                        | так                                                               |
| Робота з віддаленими реєстрами      | Плагін, який дозволяє налаштувати роботу з GCR/ECR/ACR/Docker                                                           |                                                                            |                                                                   |
| Можна додавати ноди                 | так                                                                                                                     |                                                                            | так                                                               |
| GitHub stars                        | 28k                                                                                                                     | 12k                                                                        | 5k                                                                |
| Споживання ресурсів                 | Середнє                                                                                                                 |                                                                            | Низьке                                                            |

## minikube
Minikube - інструмент, який дозволяє запустити Kubernetes кластер з однієї або кількох нод у віртуальній машині на персональному комп'ютері.


### Pros
- Легко працювати з віддаленими registry з приватним доступом (за допомогою плагінів).
- Можна задати специфічну версію Kubernetes API.
- Підтримує кілька рантаймів (containerd, cri-o, docker).
- В якості драйвера може використовуватись Podman, але його підтримка наразі в експериментальній стадії.
- Вбудований Kubernetes Dashboard, який запускається однією командою і не вимагає додаткових налаштувань.

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

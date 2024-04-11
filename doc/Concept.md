# Порівняння інструментів для запуску локального кластеру Kubernetes

|                                     | minikube                                                                                                                | kind                                                                       | k3d                                                               |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------- | ----------------------------------------------------------------- |
| Підтримка ОС                        | Linux, macOS, Windows                                                                                                   | Linux, macOS and Windows                                                   | Linux, macOS, Windows                                             |
| Підтримка архітектур                | x86-64, ARM64, ARMv7, ppc64, S390x                                                                                      | x86_64, ARM64                                                              | x86_64, ARM                                                       |
| Стабільна версія                    | так, v1.32.0                                                                                                            | нижче першої версії, v0.22.0                                               | так, v5.6.2                                                       |
| GiHub Actions                       | так, https://github.com/minikube-ci/examples                                                                            | так, https://github.com/kind-ci/examples                                   | так, https://github.com/nolar/setup-k3d-k3s                       |
| Podman Driver                       | experimental support                                                                                                    | так                                                                         | experimental support                                              |
| Документація                        | ок, досить детальна                                                                                                     | не завжди повна і актуальна, є список посилань на зовнішні ресурси https://kind.sigs.k8s.io/docs/user/resources/ | ок                                                                |
| Supported Runtimes                  | containerd, cri-o, docker                                                                                               | docker                                                                     | containerd (default), можливо docker (є документація, як встановити k3s з docker runtime, але невідомо, чи можна це зробити в k3d)                                                            |
| Multi-node Cluster support          | так                                                                                                                     | так                                                                        | так                                                               |
| Робота з віддаленими реєстрами      | Плагін, який дозволяє налаштувати роботу з GCR/ECR/ACR/Docker                                                           |                                                                            | Доступ до реєстрів налаштовується через конфіг-файл, а інструкцію, як це зробити для конкретного реєстру, треба ще пошукати в інтернеті                                                                  |
| Можна додавати ноди                 | так                                                                                                                     |                                                                            | так                                                               |
| GitHub stars                        | 28k                                                                                                                     | 12k                                                                        | 5k                                                                |
| Споживання ресурсів                 | Середнє                                                                                                                 |                                                                            | Низьке                                                            |
| Persistent Volumes | PersistentVolumes типу `hostPath` | | k3s підтримує persistent volume claims і Longhorn |
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
- Підтримка Podman в експериментальній фазі.


## K3d
> k3d is a lightweight wrapper to run k3s (Rancher Lab’s minimal Kubernetes distribution) in docker.
> k3d makes it very easy to create single- and multi-node k3s clusters in docker, e.g. for local development on Kubernetes.


### Pros
- Конфігурація кластера зберігається в конфігу. Можна зберігати у VCS і відтворити точні налаштування кластеру на інших машинах.
- В якості драйвера може використовуватись Podman, але його підтримка наразі в експериментальній стадії.
- Ощадливе споживання ресурсів.
- Підходить для IoT.

### Cons
- Щоб працювати з аутентифікацією для віддалених registry, треба розібратись з налаштуваннями.
- Підтримка Podman в експериментальній фазі.

## kind
> kind is a tool for running local Kubernetes clusters using Docker container “nodes”. kind was primarily designed for testing Kubernetes itself, but may be used for local development or CI.

### Pros
- Конфігурацію кластеру можна зберігати у файлі.
- Підтримує Podman.

### Cons
- Інструмент тільки на шляху до версії `1.0`.
- Не завжди повна і актуальна документація.


## Висновки
Поки що не розглядаю kind. Не подобається не завжди повна і актуальна документація. Розробники самі кажуть про документацію `Though this will eternally be “In Progress”!` А також не подобається, що найбільша мажорна версія -- нульова. Хоча розробники вже на шляху до `1.0`.

Рекомендую використовувати `k3d` або `minikube`. `k3d` приваблює своїм ощадливим споживанням ресурсів і можливістю зберігати конфігурацію кластеру у файлі. Але я особисто буду в подальшому використовувати `minikube` з тієї простої причини, що з `k3d` у мене не вийшло задеплоїти додаток [den-vasyliev/go-demo-app](https://github.com/den-vasyliev/go-demo-app), не стартували `ambassador` і один з подів `nats`, а з `minikube` усе спрацювало одразу з першого разу.


## Демонстрація

Я продемонструю роботу локального кластера і запущу на ньому додаток [pbitty/hello-from](https://hub.docker.com/r/pbitty/hello-from).

Створено на основі туторіалу з документації `minikube` [Using Multi-Node Clusters](https://minikube.sigs.k8s.io/docs/tutorials/multi_node/)

[![asciicast](https://asciinema.org/a/j98S4TD9TP19ceXXhX4y38h7e.svg)](https://asciinema.org/a/j98S4TD9TP19ceXXhX4y38h7e)

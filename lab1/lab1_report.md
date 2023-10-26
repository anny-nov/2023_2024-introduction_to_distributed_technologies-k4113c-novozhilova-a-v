<p> University: [ITMO University](https://itmo.ru/ru/)
<p> Faculty: [FICT](https://fict.itmo.ru)
<p> Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
<p> Year: 2023/2024
<p> Group: K4113c
<p> Author: Novozhilova Anna Vladimirovna
<p> Lab: Lab1
<p> Date of create: 17.10.2023
<p> Date of finished: 26.10.2023

<h4>Отчёт о выполнении лабораторной работы</h4>

1. Для начала работы над лабораторной необходимо было скачать Docker и minikube. Docker уже был установлен на машине, minikube был установлен с помощью дистрибутива.

2. Был создан контейнер в docker, в котором запущен кластер из одного узла.  
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/1.png">
Рисунок 1 - Развертывание кластера

3. Затем был написан манифест, декларирующий существование пода (набор контейнеров), который должен состоять из одного контейнера vault-container с исходным образом hashicorp/vault:1.13.3. Полный текст манифеста находится в файле vault.yaml.

4. Этот манифест был применен с помощью команды kubectl apply. Спустя какое-то время в списке подов отобразился запущенный под vault.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/7.png">
Рисунок 2 - Создание пода vault

5. Изначально поды доступны только внутри кластера по внутренним адресам. Поэтому далее был создан сервис, который обеспечивает доступ к подам с именем vault снаружи кластера при подключении к порту 8200.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/6.png">
Рисунок 3 - Создание сервиса

6. Чтобы получить доступ с компьютера, без необходимости заходить в кластер, был прокинут порт локального компьютера на порт сервиса, по которому доступно приложение.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/5.png">
Рисунок 4 - Форвардинг портов

7. Теперь приложение Vault стало доступно по адресу http://localhost:8200.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/4.png">
Рисунок 5 - Приложение, установленное в контейнере

8. Для авторизации в Vault необходим был авторизационный токен, который отображается в логах при запуске приложения. Для того, чтобы посмотреть логи пода, была использована команда kubectl logs vault.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/8.png">
Рисунок 6 - Просмотр логов и поиск токена

9. После введения токена в окно авторизации, был успешно получен доступ к функциям приложения.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/9.png">
Рисунок 7 - Vault после авторизации

10. После завершения авторизации контейнер с кластером был остановлен с помощью команды minikube stop.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/10.png">
Рисунок 8 - Остановка кластера

11. Была составлена схема организации контейнеров и серверов.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab1/img/11.png">

**Выводы**: В ходе выполнения лабораторной работы в контейнере докер был запущен кластер kubernetes, состоящий из одной ноды. Были освоены такие понятия, как кластер, нода, под и сервис. Также был написан манифест для создания пода и сервис, позволяющий получить к поду доступ с локальной машины.

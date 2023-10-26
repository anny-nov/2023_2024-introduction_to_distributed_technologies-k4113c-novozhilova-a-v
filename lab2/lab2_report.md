<p> University: [ITMO University](https://itmo.ru/ru/)
<p> Faculty: [FICT](https://fict.itmo.ru)
<p> Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
<p> Year: 2023/2024
<p> Group: K4113c
<p> Author: Novozhilova Anna Vladimirovna
<p> Lab: Lab1
<p> Date of create: 21.10.2023
<p> Date of finished: 26.10.2023

<h4>Отчёт о выполнении лабораторной работы</h4>

1. Был написан манифест, декларирующий существование деплоймента, в который входит два пода (количество подов контрлируется репликасетом). В подах размещен контейнер с приложением itdt-contained-frontend. Текст манифеста находится в файле deployment.yaml.

2. С помощью поля env для контейнеров в подах определены переменные REACT_APP_USERNAME и REACT_APP_COMPANY_NAME.

3. С помощью команды minikube kubectl apply манифест был применен. Как только создается деплоймент, репликасет поднимает нужное количество подов, дополнительных действий не требуется.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab2/img/1.png">
Рисунок 1 - Создание deployment

4. Для доступа к приложению был создан сервис, который делает доступным созданный ранее deployment, прокидывая в контейнер порт 3000 (на этом порту в контейнере расположено приложение).
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab2/img/2.png">
Рисунок 2 - Создание сервиса

5. Был прокинут 3000 порт локального компьютера с помощью port-forwarding, чтобы иметь доступ к приложению с локального адреса.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab2/img/3.png">
Рисунок 3 - Форвардинг портов

6. Теперь приложение стало доступно по адресу http://localhost:3000. На сайте отображаются значения переменных и имя контейнера, который прислал данные. Переменные неизменны, так как они задавались при создании подов и применяются ко всем созданным контейнерам. Имя контейнера же может меняться, так как внутри deployment расположены два пода, они равноправны и оба могут отзываться на запросы.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab2/img/4.png">
Рисунок 5 - Приложение, установленное в контейнере

8. Логи для каждого отдельного контейнера можно посмотреть с помощью команды minikube kubectl logs с параметром -с (в параметр передается имя контейнера).
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab2/img/5.png">
Рисунок 6 - Просмотр логов контейнеров

9. Была составлена схема организации контейнеров и серверов.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab2/img/6.png">

**Выводы**: В результате выполнения лабораторной работы были изучены и применены на практике deployment и replicaset, позволяющие осуществлять управление несколькими подами одновременно.

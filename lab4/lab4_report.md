<p> University: [ITMO University](https://itmo.ru/ru/)
<p> Faculty: [FICT](https://fict.itmo.ru)
<p> Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
<p> Year: 2023/2024
<p> Group: K4113c
<p> Author: Novozhilova Anna Vladimirovna
<p> Lab: Lab4
<p> Date of create: 05.11.2023
<p> Date of finished: 16.11.2023

<h4>Отчёт о выполнении лабораторной работы</h4>

1. Был создан и запущен новый кластер со следующими указанными параметрами: количество нод, имя кластера и плагин, использующийся для работы с сетью (в данной лабораторной работе это calico).
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/1.png">
Рисунок 1 - Запуск кластера

2. После того, как необходимые пакеты были загружены и кластер стал доступен для использования, было проверено, что обе ноды запустились и в статусе Ready, а также что обе ноды находятся под управлением calico.  
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/2.png">
Рисунок 2 - Проверка корректности запуска

3. Затем каждой ноде был присвоен label "zone" с различными значениями. Эти лейблы имитируют разное географическое положение нод: предположим, одна физически находится в Санкт-Петербурге, а вторая - в Москве.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/3.png">
Рисунок 3 - Маркировка нод

4. Эта маркировка была использована для создания пулов IP-адресов, чтобы объектам в нодах адреса назначались из разных подсетей, исходя из их географиеского положения. Для ноды, которая находится в Санкт-Петербурге - адреса из подсети 10.0.10.0/24, а для Московской - 10.0.20.0/24. Перед применением манифеста, который деклаирует существование таких пулов, был удален дефолтный пул адресов, из которого назначаются адреса на все немаркированные ноды.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/4.png">
Рисунок 4 - Создание пулов IP-адресов

5. Затем в кластере был создан deployment, аналогичный тому, что создавался во 2ой лабораторной работе: с репликасетом, гарантирующим наличие двух подов, в которых созданных контейнеры с приложением itdt-contained-frontend. В контейнер при создании передаются переменные REACT_APP_USERNAME и REACT_APP_COMPANY_NAME, определенные в манифесте.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/5.png">
Рисунок 5 - Создание deployment

6. Для доступа к приложению был создан сервис, который делает доступным созданный ранее deployment, прокидывая в контейнер порт 3000 (на этом порту в контейнере расположено приложение).
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/6.png">
Рисунок 6 - Создание сервиса

7. После проброса портов приложение стало доступно в браузере по адресу localhost:3000. Переменные, переданные в контейнеры при создании, остаются неизменными, однако имя контейнера и его IP-адрес могут меняться, в зависимости от того, на какой из двух подов был перенаправлен запрос. Так как поды были созданы на разных нодах (благодаря механизму балансировки нагрузки между всеми нодами), один из них имеет адрес 10.0.10.66, а второй - 10.0.20.194, принадлежащий другой подсети.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/7.png">
Рисунок 7 - Приложение

8. Помимо IP-адресов каждому поду при создании присваивается FQDN. По умолчанию этот адрес формируется по следующему шаблону: pod-ip-address.my-namespace.pod.cluster-domain. Было проверено, что оба пода доступны друг другу по этим адресам.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/8.png">
Рисунок 8 - Пинг с первого пода
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/9.png">
Рисунок 9 - Пинг со второго пода

10. Была составлена схема организации контейнеров и серверов.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab4/img/10.png">
Рисунок 10 - Схема

**Выводы**: В ходе выполнения лабораторной работы была рассмотрена возможность подключения Calico в качестве подключаемого плагина для упрвления сетью в kubernetes, что значительно увеличивает гибкость настроек сети. Был настроен кластер из двух нод, IP-адреса в котором выдавались из двух разных пулов, исходя из географической принадлежности нод. Так же рассмотрена работа coreDNS, а именно формирование дефолтных FQDN имен для объектов kubernetes и их связь между собой по этому имени.

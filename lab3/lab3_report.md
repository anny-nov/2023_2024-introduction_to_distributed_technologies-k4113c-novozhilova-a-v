<p> University: [ITMO University](https://itmo.ru/ru/)
<p> Faculty: [FICT](https://fict.itmo.ru)
<p> Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies)
<p> Year: 2023/2024
<p> Group: K4113c
<p> Author: Novozhilova Anna Vladimirovna
<p> Lab: Lab3
<p> Date of create: 17.10.2023
<p> Date of finished: 16.11.2023

<h4>Отчёт о выполнении лабораторной работы</h4>

1. Был написан манифест для создания configmap, в котором хранятся значения переменных REACT_APP_USERNAME и REACT_APP_COMPANY_NAME. Конфигмапы удобно использовать при разработке больших проектов, где переменные могут использоваться в различных конфигурациях и манифестах, потому что они обеспечивают единую точку для изменений.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/8.png">
Рисунок 1 - Создание конфигмапа

2. Затем был создан replicaset, обеспечивающий существование двух подов с лейблом app=lab3 и содержащих в себе контейнер с приложением. Переменные среды в контейнер передаются с помощью созданного ранее конфигмапа.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/9.png">
Рисунок 2 - Создание replicaset

3. Для доступа к подам необходим сервис, прокидывающий порт 3000 (на котором в контейнере находится приложение) на случайный порт ноды. Был написан и применен манифест, декларирующий существование такого сервиса.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/10.png">
Рисунок 3 - Создание сервиса

4. Затем с помощью утилиты openssl был выпущен сертификат, выпущенный на FQDN, по которому дальше будет доступно приложение.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/1.png">
Рисунок 4 - Выпуск сертификата

5. Сертификат и ключ к нему импортированы в кластер kubernetes в виде специального типа объектов - секрета.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/4.png">
Рисунок 5 - Создание секрета

6. Имя созданного в прошлом пункте секрета было указано в манифесте, деклрирующем существование ингресса. Ингресс - это тип ресурса Kubernetes, представляющий собой набор правил, по которым сервис будет получать и обрабатывать входящие пакеты. Помимо сертификата в манифесте также было указано доменное имя anyaoi-lab3.ru и сервис, которому будет передаваться трафик, приходящий на этот домен.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/5.png">
Рисунок 6 - Создание ингресса

7. Так как работа выполянлась в операционной системе Windows, для доступа к игрессу необходимо было открыть туннель командой minikube tunnel.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/11.png">
Рисунок 7 - Туннель

8. Также в файл hosts была добалена строка, сопоставляющая доменное имя anyaoi-lab3.ru и адрес локального компьютера 127.0.0.1

9. После всех приготовлений по адерсу anyaoi-lab3.ru запускается страничка с приложением на React.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/7.png">
Рисунок 8 - Открывающийся сайт

10. Также если открыть подробную ифнормацию о сертфикате, можно увидеть, что данные соответствуют тем, что были введены при выпуске сертификата.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/6.png">
Рисунок 9 - Сертификат

11. Была составлена схема организации контейнеров и серверов.
<image src="https://github.com/anny-nov/2023_2024-introduction_to_distributed_technologies-k4113c-novozhilova-a-v/blob/main/lab3/img/12.png">
Рисунок 10 - Схема

**Выводы**: В результате выполнения лабораторной работы был настроен веб-сайт, данные которого хранятся в кластере minikube, а доступ осуществляется по доменному имени; были освоены основы работы с ingress, сертификатами и секретами.

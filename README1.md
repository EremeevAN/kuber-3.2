### Домашнее задание к занятию «Установка Kubernetes»
### Задание 1. Установить кластер k8s с 1 master node
Подготовка работы кластера из 5 нод: 1 мастер и 4 рабочие ноды.
В качестве CRI — containerd.
Запуск etcd производить на мастере.
Способ установки выбрать самостоятельно.
Результат:

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/1.png)

Ответы на вопросы:

Вижу что почти доделали, хотел убедиться, а вы какой CNI выбрали для кластера?
Flannel

Я решил пересоздать все виртуальные машины
что по характеристикам(в прошлый раз было 2 CPU):

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/2.png)

Инстукцию использовал эту:

https://netology.ru/profile/program/shkuber-17/lessons/508229/lesson_items/2752960

проверяем порт

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/3.png)

Установка основных компонент:

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/4.png)

Инициализация master-ноды:

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/5.png)

Первая установка Flannel(спойлер фейл)

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/6.png)

пересоздаем ноду и сразу же ставим Flannel

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/7.png)

Установка прошла успешно 

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/8.png)

Нюанс. Для запуска Flannel требуется модуль br_netfilter, и начиная с версии 1.30 kubeadm не проверяет, установлен ли этот модуль, поэтому Flannel не запустится корректно, если модуль отсутствует.(Это не было учтено при первой установке и в инструкции про это ни слова)

Настройка воркеров и подключение к ноде

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/9.png)

Нода ушла в сбой.

![image](https://github.com/EremeevAN/kuber-3.2/blob/main/10.png)

И с тем же самым я столкнулся и в прошлый раз.  Вопрос: как получилось тогда подключить? Ответ: иногда спасал перезапуск службы kubelet или она сама поднималась

Вот как то так получается:


![image](https://github.com/EremeevAN/kuber-3.2/blob/main/11.png)

И причина мне не ясна

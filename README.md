## Отчет

### Работу выполнил Степанов Роман Андреевич, студент группы БПИ227

### Вариант 33

### Условие:

Пляшущие человечки. На тайном собрании глав преступного
мира города Лондона председатель собрания профессор Мориарти постановил: отныне вся переписка между преступниками должна
вестись тайнописью. В качестве стандарта были выбраны «пляшущие человечки», шифр, в котором каждой букве латинского
алфавита соответствует хитроумный значок.
Реализовать клиент–серверное приложение, шифрующее
исходный текст (в качестве ключа используется кодовая
таблица, устанавливающая однозначное соответствие
между каждой буквой и каким–нибудь числом).
Каждый процесс–шифровальщик является клиентом. Он кодирует свои кусочки общего текста. При решении использовать
парадигму портфеля задач. клиенты работают асинхронно, формируя свой закодированный фрагмент в случайное время.
Следовательно, при занесении информации в портфель–сервер необходимо проводить упорядочение фрагментов.
В программе необходимо вывести исходный текст, закодированные
фрагменты по мере их формирования, окончательный закодированный текст.

### Сценарий:

Решение по своей структуре максимально схоже с решением предыдущего идз. Интересное различие - рассылка логов третьей
стороне

Программа сервер получает на вход сообщение, которое должно быть зашифровано, делит его на части и отдает клиентам.
Клиенты, после получения части сообщения, шифруют его и отправляют обратно на сервер

### Об аргументах:

Сервер принимает на вход: <ip> <port> <number> <message>.
number - число клиентов, которые будут шифровать сообщения.
Клиент принимает на вход: <ip> <port>, по которому клиент должен постучаться, чтобы попасть на сервер

# Предполагаемая оценка - 8 баллов

На каждую оценку разработана отдельная программа, которая является модификацией предыдущей. Базовые понятия описаны в
решении на 4-5 баллов, далее в каждом критерии указан список изменений

# Критерии на 4-5 баллов:

## Решение:

В папке 4-5 два файла: server.cpp и client.cpp.

server.cpp - сервер, который должен быть запущен первым. Принимает на вход ip, port, n, message. Ждет подключения n
клиентов, которые подтвердят свой статус шифровальщиков сообщением "worker". Делит message на части,
динной ```TASK_SIZE``` (#define в файле lib.h) и отправляет их клиентов. Отправление работает следующим образом: сервер
обходит список рабочих и отдает им кусок сообщения. Если список закончился - то сервер продолжает отсылать сообщения,
обнулив при этом счетчик списке клиентов. Далее сервер получает ответы от клиентов - в конфигруации на оценку 4-5
баллов, сервер синхронно собирает ответы.
После того как сервер собрал все ответы, он выводит их на экран в правильном порядке.
client.cpp - клиент, который должен быть запущен только после запуска сервера (иначе, он не сможет с ним соединиться).
Получает на вход ip адрес и порт сервар. После принятия сервером, отсылает ему сообщение "worker". Получает от сервера
сообщения, которые шифрует при помощи метода encode (из файла encode.h). Для этого метода используется словарь, который
находится в том же .h файле. Перед использованием - его надо проинициализировать. Функция инициализации позволяет при
отсутствии переданных аргументов сделать стандартную иницилазицию - каждому символу сопоставят символ, аски код которого
больше его самого на SHIFT (#define в lib.h) (в случае, если полученное число больше 128 - берется остаток от этого
числа по модулю 128). Словарь типа <char, char>, для дого чтобы длина задания и ответа совпадала - возможно
уницицированное чтение пакетов.
файлы lib.h и lib.cpp содержат определения и реализацию важных функций, используемых в программе.

# Критерии на 6-7 баллов:

В рамках оценивания, на 6-7 и 8 баллов сдана одна программа, т. к. изначальное самое просто решение удовлетворяет как
критериям на 6-7 баллов, так и критерям на 8 баллов (В прошлой идз преподаватель разрешил совместить работу на 6-7-8
баллов с данным условием. В рамках данного идз различие между программами на 6-7 и 8 баллов так же отсутствует т.к.
реализована многоадресная передача датаграмм).

Создан отдельный файл observer с такими же параметрами запуска, как и обычный клиент. Для рассылки сообщений
наблюдателями использована система multicast.
Для рассылки выбран ip 224.0.0.0 и порт 8081. Наблюдателю надо сообщить этот ip и порт

# Критерии на 8 баллов:

В силу того, как работает multicast рассылка, можно подключать любое число шифровальщиков (в любой момент работы
программы - достаточно лишь подписаться на рассылку)

В прошлом идз я отправлял фото моей кошки, теперь ей уже больше 3х месяцев!!!!
Она уже очень сильно выросла и не думает останавливаться....
![cat1](Cat/1.jpg)

![cat2](Cat/2.jpg)

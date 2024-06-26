# hping3Manual

=============================================
-c - кількість пакетів
-i - інтервал між пакетами (наприклад, -i u1000 = 100 пакетів за секунду, -i u10000 = 10 пакетів за секунду)
--flood - надсилання пакетів максимально швидко
-q - тихий режим (без виведення на екран)
-I - ім'я мережевого інтерфейсу
-V - детальна інформація
=============================================
Режими роботи:
-0 - RAW IP режим
-1 - ICMP режим (ping)
-2 - UDP режим
-8 - сканування портів
-9 - прослуховування
Стандартний режим - TCP !!!
=============================================
Маніпуляції з IP:
-a - підміна вихідної IP-адреси
--rand-dest - випадкова IP-адреса призначення
--rand-source - випадкова IP-адреса джерела
=============================================
Приклади команд:
Приклад 1:
Відправка 5 пакетів на порт 80 хосту 192.168.1.5 через інтерфейс eth0:

hping3 192.168.1.5 -I eth0 -p 80 -s 4545 -c 5 -V -S
Інтерфейс: eth0
Порт призначення: 80
Порт джерела: 4545
Кількість пакетів: 5
Детальна інформація: так
SYN прапорець
=============================================
Приклад 2:
Відстеження маршруту до хосту 192.168.1.5:

hping3 192.168.1.5 -T 1 --traceroute

=============================================

Приклад 3:
Сканування TCP SYN на порту 80:

hping3 -S 192.168.1.5 -p 80
Сканування ACK на порту 80:

hping3 -A 192.168.1.5 -p 80
Сканування UDP на порту 80:

hping3 -2 192.168.1.5 -p 80
SYN-сканування портів від 50 до 60:

hping3 -8 50-60 -S 192.168.1.5 -V
Сканування портів FIN, PUSH та URG на порту 80:

hping3 -F -P -U 192.168.1.5 -p 80
Сканування всієї підмережі для знаходження живих хостів:

hping3 -1 192.168.1.x --rand-dest -I eth0

=============================================

Приклад 4:
Вставлення в пакети вмісту текстового файлу:

hping3 192.168.1.5 -p 80 -d 50 -E hello.txt
Розмір даних: 50 байт
Файл: hello.txt

=============================================

Приклад 5:
Генерація унікальних ехо-запитів:

hping3 --rand-source 192.168.1.5
Додавання параметра --flood для надсилання в режимі реального часу:


hping3 --rand-source --flood 192.168.1.5

=============================================

Приклад 6:
Прослуховування трафіку з сигнатурою HTTP:

hping3 -9 HTTP -I eth0

=============================================

Приклад 7:
SYN-флуд на порт 22 з підробленою IP-адресою:

hping3 -S 192.168.1.5 -a 192.168.1.254 -p 22 --flood
Підміна IP-адреси: 192.168.1.254

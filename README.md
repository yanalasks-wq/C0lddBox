### C0lddBox

## Короткий огляд кроків вирішення CTF
Отримати IP-адресу цільової машини (netdiscover).
Просканувати відкриті порти цільової машини (nmap).
Перевірити HTTP-сервіс та знайти підказки.
Зробити підвищення привілеїв


## Крок 1. Спочетку дізнаємося сво IP за допомогою команди ip a:

<img width="845" height="354" alt="image" src="https://github.com/user-attachments/assets/05b84d2b-6d7d-4f8f-b671-f4126a14a9a1" />

## Крок 2. Вводимо команду sudo netdiscover -r 192.168.0.0/24

<img width="652" height="220" alt="image" src="https://github.com/user-attachments/assets/56a75698-8fb4-48be-8b92-2d6ea7756a01" />

192.168.0.106 — IP Systemtechnik GmbH, визначається через префікс MAC-адреси 08:00:27.
За допомогою цієї IP переходимо на сайт ColddBox

<img width="1563" height="837" alt="image" src="https://github.com/user-attachments/assets/92c3eeff-0726-44a8-b4cd-cecf521a4e31" />

## Крок 3. Пробуємо залогінитись, але у нас не виходить 

<img width="438" height="526" alt="image" src="https://github.com/user-attachments/assets/43cc4f02-dd36-4fe8-9bdc-dcb167698437" />

## Крок 4. Вводимо у термінал команду wpscan --url http://192.168.0.106 -e u ,щоб просканувати сайт на базі WordPress та автоматично знайти логіни, які потім можна використати для подальшого тестування на проникнення чи підбору паролів.

<img width="846" height="455" alt="image" src="https://github.com/user-attachments/assets/66b56562-2d1f-440a-8351-553de22a41b8" />

Команда знайшла чотири логіни:
1)the cold in person 
2)philip
3)c0ldd
4)hugo

## Крок 5. Для брутфорсу використовуватиму команду wpscan
Вводжу у термінал wpscan --url http://$IP -U logins -P /usr/share/wordlists/rockyou.txt
Знайши пароль

<img width="1000" height="504" alt="image" src="https://github.com/user-attachments/assets/3eb06488-d8eb-4994-805e-e0e48bfd4180" />

[SUCCESS] - c0ldd / 9876543210

Вводимо пароль 

<img width="323" height="264" alt="image" src="https://github.com/user-attachments/assets/d032490b-7b86-4fbd-8dce-7873f8284e5a" />

І успішно заходимо

<img width="1907" height="834" alt="image" src="https://github.com/user-attachments/assets/a0031d72-69c9-4a20-b44c-499ff6ad5576" />

## Крок 6.
Заходжу у вкладку Apearence, потім у Editor і у вкладку Footer. Модифікує наявний код за допомогою репозиторію на ГітХабі і записую свою IP і порт.

<img width="1187" height="473" alt="image" src="https://github.com/user-attachments/assets/583b41a1-6390-437a-b8f2-ed7c3352f0d3" />

І не забуваємо активувати цей порт nc -lvnp 8080 

<img width="240" height="48" alt="image" src="https://github.com/user-attachments/assets/fbbf35fc-cd8a-49ae-8d13-3dd52424e93a" />

<img width="928" height="185" alt="image" src="https://github.com/user-attachments/assets/b1d944ca-eb64-4324-9282-2299c30b4589" />

<img width="902" height="603" alt="image" src="https://github.com/user-attachments/assets/eca59bf7-27c6-409d-8303-2938db70473b" />

<img width="1045" height="547" alt="image" src="https://github.com/user-attachments/assets/55791840-27e8-422b-a774-af0f87adb79d" />

Ми знайшли облікові дані для бази даних,які також підходять для системного користувача:
Користувач: c0ldd
Пароль: cybersecurity

Пробуємо зайти в систему, як c0ldd

<img width="509" height="171" alt="image" src="https://github.com/user-attachments/assets/c966d1d7-a44c-4755-8cf9-edb21f4a8249" />

Виконуємо команду для перевірки доступних прав

<img width="798" height="210" alt="image" src="https://github.com/user-attachments/assets/cf668ff2-1d56-425c-b939-2391fe69de57" />

Користувач c0ldd може виконувати від імені root три команди без введення пароля:
/usr/bin/vim
/bin/chmod
/usr/bin/ftp

<img width="956" height="392" alt="image" src="https://github.com/user-attachments/assets/68f4c42e-94ad-4129-b20c-115476d49bd0" />

Ось відповідь: root
wqFGZWxpY2lkYWRlcywgbcOhcXVpbmEgY29tcGxldGFkYSE=
Декодуємо за допомогою www.base64decode.org та отримуємо такий результат-привітання:

<img width="1235" height="665" alt="image" src="https://github.com/user-attachments/assets/5360c787-f2b4-49e4-adf4-f7c68e90e006" />

Перевіряю доступ

<img width="755" height="165" alt="image" src="https://github.com/user-attachments/assets/131f8e51-cea5-4f93-b0af-7e25cbea27ed" />

Доступ є до всього, для цього я використала ftp, запустивши її з правами sudo.Всередині інтерактивного середовища ftp вкладається виконання системної оболонки через знак оклику !/bin/sh. Оскільки сама програма ftp виконувалася з правами root, викликана з неї оболонка також автоматично успадкувала ці максимальні привілеї.







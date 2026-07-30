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






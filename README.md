# Практическая работа №5 - Threat Hunting

**Выполнил студент группы ББМО-01-23 Росляков В.А.**

Для выполнения работы был использован стенд, аналогичный стенду из практической работы 3

Всего 3 виртуальные машины
1) Ubuntu с агентом Wazuh
2) Ubuntu с сервером Wazuh
3) Kali Linux

С хоста, с настроенным агентом имеем доступ по сети к хосту с сервером. Видим подключённый агент.

![Image](https://github.com/user-attachments/assets/aaa18a93-82cc-4e65-9eae-04cd09f88be9)

# IDS Suricata

### Развернем дополнительно на защищаемом хосте IDS Suricata

### Добавляем репозитории suricata

![Image](https://github.com/user-attachments/assets/b4544f04-fa1d-4f9e-8723-9930733c5a25)

### Устанавливаем

![Image](https://github.com/user-attachments/assets/a3eb2906-79c3-4d91-927a-0fd6e2dd9353)

### Также загружаем правила

![Image](https://github.com/user-attachments/assets/8fe160e4-4fb5-48d0-9135-142bcd099fe7)

### Модифицируем конфиг

![Image](https://github.com/user-attachments/assets/2211430d-b2cd-43cf-af2d-6ae33417b46f)

### Внесем сбор логов сурикаты в конфиг Wazuh

![Image](https://github.com/user-attachments/assets/adbf5d2c-a89b-41cf-a7d9-217c76bec304)

### Перезапускаем агент

![Image](https://github.com/user-attachments/assets/73ab5d53-b642-4604-af00-6161c8b02471)

### После пробуем пропинговать хост с агентом и видим события от сурикаты

![Image](https://github.com/user-attachments/assets/b1bfea56-bd17-40fb-8e76-f1b7253ae6de)

# Web-приложение

### На защищаемом клиенте поднято пустое веб-приложение Apache

![Image](https://github.com/user-attachments/assets/71d5b7c3-213e-4e45-907d-a59ea0386226)

![Image](https://github.com/user-attachments/assets/92ca5314-f1f7-40a3-a75a-e8ea84537ec9)

# Сканер уязвимостей Nikto

### Запустим сканер уязвимостей Nikto с Kali

![Image](https://github.com/user-attachments/assets/8352da99-dc51-4a22-91c8-3cce2b094b30)

### Также видим события от сурикаты

![Image](https://github.com/user-attachments/assets/6c092874-ebd5-4728-a845-a2cad77e1938)

![Image](https://github.com/user-attachments/assets/f25fbeda-5109-4d7a-88d1-410240b1c172)

# YARA

### Скачивание, компиляция и установка YARA

![Image](https://github.com/user-attachments/assets/66820493-b2a3-4f0d-bc5f-f3de2f3636e3)

![Image](https://github.com/user-attachments/assets/1bd90739-5235-41eb-be73-64da61d8bc0d)

### Проверяем, что установка прошла успешно

![Image](https://github.com/user-attachments/assets/d9fa748e-731d-4c83-acad-8c8443a878be)

### Загружаем правила

![Image](https://github.com/user-attachments/assets/d3fd3691-d37d-4581-9360-14139e52751d)

### Создаём скрипт и устанавливаем привилегии в соответствии с документацией

![Image](https://github.com/user-attachments/assets/5973bb32-3187-4658-acc6-84ee615de193)

### Редактируем ossec конфиг

![Image](https://github.com/user-attachments/assets/8d276e8d-10ee-4e7f-8c83-89c87c639a6b)

### На сервере также настраиваем всё необходимое

### Настраиваем правила для отслеживания изменений и срабатывания YARA-правил

![Image](https://github.com/user-attachments/assets/46fe78d7-9bfa-40cb-b45f-697da01a4427)

### Настраиваем декодер

![Image](https://github.com/user-attachments/assets/c0e52542-8145-4d0c-a92b-ce2db9bdeb4a)

### Настраиваем команды для сканирования

![Image](https://github.com/user-attachments/assets/65c5df1e-8c8c-4f37-bc69-61f036c3b6a6)

### Срабатывание правил Yara

### Для проверки был создан реверс-шелл с помощью msfvenom. После его исполнения на хосте с агентом, получили доступ на кали

![Image](https://github.com/user-attachments/assets/fb28217b-0c64-435a-b40e-cbd9f1ce63c8)

### Также видим срабатывание правил в Wazuh

![Image](https://github.com/user-attachments/assets/ea16d72d-2067-48ec-815f-e2833eb1bf44)

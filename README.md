# Практическая работа №5 - Threat Hunting

**Выполнил студент группы ББМО-01-23 Росляков В.А.**

Для выполнения работы был использован стенд, аналогичный стенду из практической работы 3

Всего 3 виртуальные машины
1) Ubuntu с агентом Wazuh
2) Ubuntu с сервером Wazuh
3) Kali Linux

С хоста, с настроенным агентом имеем доступ по сети к хосту с сервером. Видим подключённый агент.

![Image](https://github.com/user-attachments/assets/dd34bdc8-23f7-409a-a65f-4d991f423199)

# IDS Suricata

### Развернем дополнительно на защищаемом хосте IDS Suricata

### Добавляем репозитории suricata

![Image](https://github.com/user-attachments/assets/940f993e-b152-496a-b056-8603d0e3dbca)

### Устанавливаем

![Image](https://github.com/user-attachments/assets/4779693e-ff8e-4ab9-9aa1-a75e9cc8c7d5)

### Также загружаем правила

![Image](https://github.com/user-attachments/assets/905084e6-2224-4008-a2d2-9b25bb90d2a0)

### Модифицируем конфиг

![Image](https://github.com/user-attachments/assets/9a3df026-0d86-47ec-9b87-8fa2d269a8a1)

### Внесем сбор логов сурикаты в конфиг Wazuh

![Image](https://github.com/user-attachments/assets/6844d4d9-67da-43b9-a38f-9438710d7793)

### Перезапускаем агент

![Image](https://github.com/user-attachments/assets/c918350b-dbd9-4b6b-bbf8-5cc7fb27067f)

### После пробуем пропинговать хост с агентом и видим события от сурикаты

![Image](https://github.com/user-attachments/assets/8fa76ad1-f383-412f-9ea1-97d7fd83f5e0)

# Web-приложение

### На защищаемом клиенте поднято пустое веб-приложение Apache

![Image](https://github.com/user-attachments/assets/437af555-19d3-4a77-aa09-16b5358df243)

![Image](https://github.com/user-attachments/assets/b28744db-bc8f-4b4b-affb-5f430ff1ac48)

# Сканер уязвимостей Nikto

### Запустим сканер уязвимостей Nikto с Kali

![Image](https://github.com/user-attachments/assets/b4e1689c-2914-4453-a15d-062809d603a4)

### Также видим события от сурикаты

![Image](https://github.com/user-attachments/assets/801a0cf9-bb6f-4ed0-8ca6-3f67e06f3d93)

![Image](https://github.com/user-attachments/assets/57e6c02b-47d9-4450-9d72-80ebd76968b9)

# YARA

### Скачивание, компиляция и установка YARA

![Image](https://github.com/user-attachments/assets/02d903cd-6482-40e8-8f6b-22b9e43246ad)

![Image](https://github.com/user-attachments/assets/c912a9a3-8355-4c2b-ba3b-966d5d97169d)

### Проверяем, что установка прошла успешно

![Image](https://github.com/user-attachments/assets/9001a935-0a12-48a1-ab38-d6179a3c3f6e)

### Загружаем правила

![Image](https://github.com/user-attachments/assets/fdaa4311-2829-445b-89a3-c30a99e8a7ed)

### Создаём скрипт и устанавливаем привилегии в соответствии с документацией

![Image](https://github.com/user-attachments/assets/57de6dc8-7c36-403c-83f5-ef27479396a2)

### Редактируем ossec конфиг

![Image](https://github.com/user-attachments/assets/e67e432e-3d6c-40b6-9c8e-4c4db2054ccb)

### На сервере также настраиваем всё необходимое

### Настраиваем правила для отслеживания изменений и срабатывания YARA-правил

![Image](https://github.com/user-attachments/assets/49983872-dce4-497e-84c5-9d666a37e378)

### Настраиваем декодер

![Image](https://github.com/user-attachments/assets/b6e04b6e-e502-4b8b-8ad7-31c4e9f02036)

### Настраиваем команды для сканирования

![Image](https://github.com/user-attachments/assets/6caf1931-7e54-453e-a0eb-569a501a643c)

### Срабатывание правил Yara

### Для проверки был создан реверс-шелл с помощью msfvenom. После его исполнения на хосте с агентом, получили доступ на кали

![Image](https://github.com/user-attachments/assets/078b3f5a-7ad2-4664-a5fb-d59f65d79792)

### Также видим срабатывание правил в Wazuh

![Image](https://github.com/user-attachments/assets/d41eb1cc-ca62-4ce2-9ac7-0839e29db790)

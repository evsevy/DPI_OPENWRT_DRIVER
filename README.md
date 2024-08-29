

## Описание

Данный проект представляет собой программу на C, которая иллюстрирует процесс обработки и сохранения пакетов данных. Программа использует многопоточность, шифрование AES и формат JSON для сохранения данных. Основной ее задачей является безопасное хранение пакетов, при этом она защищает некоторые виды данных от записи (в данном случае "опасные" пакеты).

## Функционал

1. **Генерация ключа AES**: Программа генерирует случайный ключ для шифрования данных.
2. **Обработка пакетов**: Создается отдельный поток, который имитирует получение пакетов данных.
3. **Шифрование данных**: Пакеты данных шифруются перед записью в файл.
4. **Формат хранения**: Данные сохраняются в формате JSON в указанном файле.
5. **Обнаружение опасных пакетов**: Программа проверяет содержание пакетов и исключает "опасные" пакеты из записи.

## Системные требования

- Компилятор C (например, GCC)
- Библиотека OpenSSL
- Библиотека cJSON
- POSIX-системы для работы с потоками

## Установка

1. Убедитесь, что у вас установлены библиотеки OpenSSL и cJSON. Установите их, если это не так.

   Пример установки на Ubuntu:
   ```bash
   sudo apt-get install libssl-dev
   sudo apt-get install libcjson-dev
   ```

2. Скомпилируйте программу, используя следующий команду:

   ```bash
   gcc -o packet_handler packet_handler.c -lcjson -lssl -lcrypto -lpthread
   ```

3. Запустите программу с привилегиями суперпользователя (для записи в `/etc/data.json`):

   ```bash
   sudo ./packet_handler
   ```

## Использование

После запуска программы она начнет генерировать пакеты данных в отдельном потоке. Через 10 секунд (или после получения 10 пакетов) данные будут сохранены в указанный файл (`/etc/data.json`). 

Для просмотра сохраненных данных откройте файл в текстовом редакторе.

## Примечания

- Вы можете изменить путь сохранения файла, изменив переменную в строке `const char *filename = "/etc/data.json";`.
- Добавление или изменение логики обработки пакетов возможно в функции `packet_handler`.
- При наличии "опасных" пакетов они будут логироваться в консоль, но не будут записаны в файл.

## Замечания по безопасности

- Использование слабых или недостаточно случайных ключей может сделать шифрование уязвимым. Убедитесь, что системный генератор случайных чисел работает корректно.
- Обработка неправильных данных не осуществляется, и стоит рассмотреть дополнительную валидацию входящих пакетов.

## Лицензия

Этот проект имеет схему лицензии MIT, предоставляя пользователям право изменять и распространять его, при условии указания автора оригинальной работы.

Программист разработчик: Меркулов Е. В. 2024

# Работа с CtrlQ

## Подготовка к работе

### Сохранить сертификаты

- Открыть QMC,  раздел **CONFIGURE SYSTEM / Certificates**

- В поле *Add machine name* добавляем имя хоста, к которому обращаются hub/qmc/dev-hub, например: *qliksense.domain.example*

- В поле *Export file format for certificates* выбираем *Platform independent PEM-format*

- Нажимаем *Export Certificates*, путь для экспорта будет указан ниже: *Certificates will be exported to this disk location on the server: C:\ProgramData\Qlik\Sense\Repository\Exported Certificates*

### Установить CtrlQ

- Скачать установщик с сайта <https://ctrl-q.ptarmiganlabs.com>
- Установить его для пользователя, от которого будут запускаться задания или всех пользователей системы в каталог, где у этого пользователя будут права на чтение встроенных подкаталогов
- Создать каталог **cert** в каталоге, где находится установленный *Ctrl-q.exe*, скопировать туда файлы *client.pem , client_key.pem, root.pem*
>[!Tip]
>Производитель не рекомендует обращаться к сертификатам, находящимся в каталоге для выгрузки по умолчанию

## Использование

### Документация

<https://ctrl-q.ptarmiganlabs.com/docs/command/qseow/>

### Примеры наиболее востребованых операций

#### Проверка корректности настроек соединения CtrlQ с сервером QlikSense

`ctrl-q.exe qseow connection-test --host qliksense.domain.example --virtual-proxy "" --auth-user-dir DOMAIN --auth-user-id sa_qliksense`

#### Сохранение всех опубликованных приложений в QVF файлы без данных (только скрипты и визуализации) с дополнительным файлом мета-данных в каталог с номером дня (удобно для создания ежедневных бэкапов глубиной в 1 месяц)

`ctrl-q.exe qseow app-export --host qliksense.domain.example --virtual-proxy "" --auth-user-dir DOMAIN --auth-user-id sa_qliksense --output-dir "D:\QlikData\QVF\%date:~0,2%" --metadata-file-create --metadata-file-overwrite --exclude-app-data true --qvf-overwrite`

#### Вывести перечень и статус заданий в виде дерева

`ctrl-q.exe qseow task-get --host  qliksense.domain.example --virtual-proxy "" --auth-user-dir DOMAIN --auth-user-id sa_qliksense  --tree-icons`

#### Сохранить перечень и статус заданий в виде дерева в JSON файл

`ctrl-q.exe qseow task-get --host qliksense.domain.example --virtual-proxy "" --auth-user-dir DOMAIN --auth-user-id sa_qliksense  --tree-icons --output-format tree --output-dest file --tree-details appname --output-file-name tasktree.json --output-file-format json`

#### Вывести скрипт приложения в консоль (можно использовать для сохранения во внешний файл)

`ctrl-q.exe qseow script-get --host qliksense.domain.example --virtual-proxy "" --auth-user-dir DOMAIN --auth-user-id sa_qliksense --app-id 90aa0973-78d3-44a0-88f9-d702dcb98f30`

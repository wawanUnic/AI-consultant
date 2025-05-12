# AI-consultant

## The setup is done for the machine

- OS: Ubuntu 24.04.2 LTS
- Platform: x86_64
- Processor: Intel(R) Core(TM) i5-6500 CPU @ 3.20GHz (4 cores)
- RAM: 32GB DDR4 2133 MHz
- Storage: SSD 120GB

## Ports used:
- 8088 - dozzle (for docker monitoring)
- 7756 - PostgreSQL database (for storing customer communication chains)
- 7757 - Admin (for working with PostgreSQL manually)
- 7766 - MySQL database (for storing the sitemap)
- 7767 - Admin (for working with MySQL manually)
- 8000 - Supabase (vector storage for the database) knowledge)
- 5001 - Crawl4AI (for web page crawling)
- 5678 - n8n (for automation service)
- 8089 - gotify (for logging service)

## Install Docker
```
apt update
apt install docker.io
docker --version
systemctl start docker
systemctl enable docker
systemctl status docker
```

## Install Docker-compose
```
curl -L "https://github.com/docker/compose/releases/latest/download/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

## Install Dozzle
This is a lightweight open-source an application with a web interface designed to monitor Docker container logs in real time. It allows you to track events in logs without having to access the file system.

[Dozzle](https://github.com/wawanUnic/AI-consultant/blob/main/dozzle.md)

## Installing PostgreSQL (+Admin)
This is an open-source object-relational database management system. It will be used to store correspondence with clients. For each new browser session, a new chain of communication will be created in the database.

[PostgreSQL+Админер](https://github.com/wawanUnic/AI-consultant/blob/main/postgresql.md)

## Install MySQL (+Admin)
This is a popular open source relational database management system. It is used to store, manage and organize data. It will be used to store the site map on which the AI ​​consultant works.

[MySQL+Админер](https://github.com/wawanUnic/AI-consultant/blob/main/mysql.md)

## Install Supabase
This is an open source platform. Supabase provides a full set of application development tools, including Postgres Database - a reliable relational database. It will house the vector storage for the knowledge base.

[Supabase](https://github.com/wawanUnic/AI-consultant/blob/main/supabase.md)

## Installing Crawl4AI
This is a web crawling and data extraction tool specifically designed to work with large language models (LLM), AI agents, and data pipelines. This is an open source project.

[Crawl4AI](https://github.com/wawanUnic/AI-consultant/blob/main/crawl4ai.md)

## Installing n8n
This is an open source workflow automation platform. It allows you to create complex automations without the need for deep programming knowledge. The core processes of the AI ​​consultant will work in it.

[n8n](https://github.com/wawanUnic/AI-consultant/blob/main/n8n.md)

- Воркфлоу для общения с ИИ-консультантом. Должен быть включен всегда. [NeroBY_chat](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/n8n/NeroBY_chat.json)

- Воркфлоу для обхода всех старниц сайта. Добавлены автоматические дообучение, дозабвение, дообновление. Пишет логи в gotify. Должен быть включен всегда. [NeroBY_page](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/n8n/NeroBY_page.json)

2025-04-08. Смена версии n8n на 1.85.4 привела к ошибке в ноде поиска данных в базе знаний (ветка обновления данных). Воркфлоу NeroBY_page обновлен.

Важно. При добавлении или обновлении страниц, их адреса будут видны последними в таблице NeroBY_table2 (MySQL), а также знания по этим страницам поадают в конец таблицы nero_by (supabase)

- Воркфлоу для анализа одной страницы сайта. Должен быть отключен! Он вызывается автоматически из NeroBY_page. [NeroBY_scrab](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/n8n/NeroBY_scrab.json)

- Воркфлоу для учета статистики. Пишет логи в gotify. Должен быть включен всегда. [NeroBY_stats](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/n8n/Nero_BY_stats.json)

- Основной (системный) промпт включен в воркфлов NeroBY_chat. [Системный промпт](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/systemPrompt.txt)

## Installing the widget on the site
The widget code is inserted into the HTML of the site page. The insertion point is before the closing </BODU> tag (this allows the page content to load faster without blocking rendering). See the script.html file

Также для правильного отображения символов кирилицы нужна смена кодировки.  Место вставки - перед закрывающим тегом </ХЕАД>. См. файл charset.html

[Код для виджета](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/tree/dev/html)

Скрины:

[Закрытый виджет](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/html/screen1.png) - [Открытый виджет](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/html/screen2.png) - [Диалог с пользователем](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/html/screen3.png)


Можно использовать вариант скрипта с предыдущей историей переписки с клиентом. Этот вариант требует размещения на сервере файла стилей (в папке SCC) и бибилотеки (в папке JS). Необходимо настроить кэширование, что-бы эти файлы не передавались по сети, а были в кеше у клиента.

[Код для виджета2](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/tree/dev/html2)

При это нужно внести измения и в воркфлоу. Необходимо подключить память для истории переписки.

[Код входной части воркфлоу](https://gitlab.neroelectronics.by/v.ponomarchuk/ai-consultant/-/blob/dev/n8n/NeroBY_chat_withHistory.json)

## Installing a Log Service
This is a self-hosted notification server that allows you to send and receive messages. It is designed to simplify the work with notifications and provides a convenient interface for managing them.

[gotify](https://github.com/wawanUnic/AI-consultant/blob/main/gotify.md)

## 
The software must adhere to 12 design principles for building scalable and reliable applications (The Twelve-Factor App by Heroku):
1. Codebase. The application must have a single codebase managed by a version control system (Git). From this codebase, it is possible to deploy to different environments (test, staging, production). Each deployment is simply an instance of the same codebase.
2. Dependencies. All application dependencies (libraries, frameworks) must be explicitly declared and installed via package managers (pip). This helps to avoid hidden or local dependencies and provides isolation.
3. Configuration. Configurations such as API keys, databases, URLs, and environment variables should not be part of the code. Instead, they should be stored in the environment so that it is easy to switch between environments without changing the code.
4. Support services. External services (databases, APIs) should be treated as interchangeable resources. This makes it easier to replace or migrate them if a provider change is required.
5. Build, Release, Run. The separation should be strict. Build: Transform source code into an executable form. Release: Merge the build with the configuration. Run: Execute releases in worker processes.
6. Processes. Applications should run as one or more stateless processes. This means that the state should not be stored in the application's memory, but in external resources such as databases.
7. Port binding. The application should be self-contained and expose its services through ports (for example, an HTTP server on port 8080). This simplifies deployment and integration with other components.
8. Concurrency. The application should be able to scale horizontally by increasing the number of processes (more server instances).
9. Disposability. Application processes should be disposable: start quickly and terminate safely. This increases resilience to failures and simplifies upgrades.
10. Parity between development and production. Development, testing, and production environments should be as similar as possible to avoid unexpected errors during deployment.
11. Logs. Application logs should be treated as event streams that can be routed to centralized systems for processing, storage, or analysis.
12. Administrative processes. Administration should be performed as one-off processes with the same code as the main application.

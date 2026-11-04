# BankSpring — Config Repository

Этот репозиторий содержит конфигурационные файлы для всех микросервисов проекта **BankSpring**. 

## 🗂 Что здесь лежит

В корне репозитория лежат файлы вида `<имя-сервиса>.properties`:

- `account-service.properties`
- `api-gateway.properties`
- `auth-service.properties`
- `customer-service.properties`
- `loan-service.properties`
- `notification-service.properties`
- `transaction-service.properties`

*Примечание: файлы для `audit-service` и `eureka-server` могут отсутствовать, если их настройки заданы локально, либо могут быть добавлены позже.*

## 🎯 Зачем это нужно

В проекте используется **Spring Cloud Config Server**. Это значит, что все настройки (порты, подключения к базам данных, параметры Circuit Breaker и т.д.) хранятся **не внутри самих сервисов**, а в этом репозитории.

При запуске каждый микросервис обращается к Config Server (порт `8888`), который читает этот репозиторий и отдаёт сервису его настройки.

## 🚀 Как это использовать

1. **Склонируйте** этот репозиторий (или скачайте архив) на свой компьютер.
2. **Настройте Config Server**, чтобы он читал файлы из локальной папки. В файле `application.properties` (или `application.yml`) сервиса `config-server` должно быть указано:
   ```properties
   spring.profiles.active=native
   spring.cloud.config.server.native.search-locations=file:/путь/к/папке/config-repo

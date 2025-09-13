# Инструкция
Реализация REST API на Golang с использованием Chi, GORM, JWT и PostgreSQL.

## Реализовано:
- Регистрация и авторизация пользователей (JWT access/refresh токены);
- Создание и обновление документов с учётом занятости папок;
- Атомарные операции (транзакции) при перемещении документов;
- Конфигурация через `config.yml`;
- Все роуты, кроме `/register` и `/login`, защищены JWT;
- Обработка ошибок в формате JSON;
- Проверка свободного места в папке при создании/перемещении;
- Автомиграция БД через GORM: таблицы `users`, `folders`, `documents` создаются автоматически;
- Документ может быть без привязки к папке (`folder_id = NULL`).

## Как запустить проект:
### 1. Установите:
- Go 1.20+
- PostgreSQL 12+
### 2. Запустите PostgreSQL
### 3. Создайте базу данных
Откройте PostgreSQL и создайте БД:
CREATE DATABASE folders;
### 4. Настройте файл config.yml
Отредактируйте config.yml, указав свои данные (пароль бд)
### 5. Запустите сервер в терминале (VS code, например)
go run cmd/api/main.go
### 6. Примеры запросов (через curl)
Создание документа:
curl -X POST http://localhost:8080/documents \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer YOUR_JWT_TOKEN" \
  -d '{"title":"Test Doc","sheets_count":150,"folder_id":1}'

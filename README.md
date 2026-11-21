# DbStationary Architecture Documentation

**Repository:** `ekatmoz88-alt/dbstationary-architecture-docs`
**Source:** Extracted and analyzed from technical documentation at `/home/kate/technical-docs-library/03_API/`
**Status:** Draft — based on extracted source code and requirements documents
**Anonymization:** All customer names, organization names, project ciphers, specific years, internal IP addresses, and DB connection strings replaced with placeholders.

---

## Обзор / Overview

DbStationary — это C# фреймворк для работы с базами данных SQLite. Фреймворк предоставляет набор классов для управления соединениями, выполнения команд и чтения данных через провайдеры данных.

### Основные компоненты / Main Components

- **ConnectionFactory** — фабрика соединений, возвращает singleton SQLiteConnection
- **SQLiteCommandEx** — расширенная команда с поддержкой маппинга результатов
- **SQLiteDataReaderEx** — типизированный доступ к значениям, возвращаемому reader'ом
- **SQLiteMaps** — маппинг значений из DataReader в приложение модели

### Технологический стек / Technology Stack

- Язык программирования: C#
- База данных: SQLite (встраиваемая БД)
- Фреймворк: .NET
- Архитектура: layered architecture с разделением на модули

### Стройка проекта / Project Structure

```
/dbstationary-architecture-docs
│
├── README.md
├── ARCHITECTURE.md      # Архитектурный обзор
├── API_REFERENCE.md     # Справочник API
└── openapi.yaml         # Спецификация REST API (если применимо)
```

---

## Anonymization Notice

Все названия заказчиков, реальные организации, ФИО, серийные номера, ключи и внутренние адреса заменены на обобщённые обозначения. Этот документ prepared based on extracted facts only, without guessing missing parameters.

---

## Ссылки на источники

- Источник: `/home/kate/technical-docs-library/03_API/`
- Связанные исходники: `/home/kate/deshifrator-docs/sources/DbStationary.Data/`
- Оригинальные требования: `/home/kate/technical-docs-library/03_API/Дискриптор-Требования.doc`
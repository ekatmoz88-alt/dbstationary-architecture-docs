---
title: DbStationary Architecture Overview
---

# DbStationary Architecture Overview / Обзор архитектуры DbStationary

**Repository:** `ekatmoz88-alt/dbstationary-architecture-docs`  
**Source:** Extracted from `/home/kate/technical-docs-library/03_API/` and `/home/kate/deshifrator-docs/sources/DbStationary.Data/`  
**Anonymization:** All real names, organization names, project ciphers, specific years, and internal connection strings replaced with placeholders.

---

## 1. Контекстная схема (C4 Context) / C4 Context Diagram

### RU

Показывает границы системы и внешних акторов.

```mermaid
flowchart TD
    subgraph External["Внешняя среда / External Environment"]
        TransportSystem["Транспортная система / Transport System"]
        ExternalDatabase["Внешняя база данных / External Database"]
        User["Оператор / Operator"]
    end

    subgraph System["DbStationary Framework / Фреймворк DbStationary"]
        LocalDatabase["База данных / Database — SQLite"]
    end

    TransportSystem -->|Данные транзакций / Transaction Data| LocalDatabase
    User -->|Управление / Management| LocalDatabase
```

### EN

Shows system boundaries and external actors.

```mermaid
flowchart TD
    subgraph External["External Environment"]
        TransportSystem["Transport System"]
        ExternalDatabase["External Database"]
        User["Operator"]
    end

    subgraph System["DbStationary Framework"]
        LocalDatabase["Database — SQLite"]
    end

    TransportSystem -->|Transaction Data| LocalDatabase
    User -->|Management| LocalDatabase
```

---

## 2. Контейнерная схема (C4 Container) / C4 Container Diagram

### RU

Внутренняя структура фреймворка: компоненты и их взаимодействие.

```mermaid
flowchart TD
    ConnectionFactory["ConnectionFactory / Connection Factory"]
    SQLiteCommandEx["SQLiteCommandEx / Command with Mapping"]
    SQLiteDataReaderEx["SQLiteDataReaderEx / Data Reader"]
    SQLiteMaps["SQLiteMaps / Object Mapping"]
    Database["SQLite Database"]

    ConnectionFactory -->|Creates Connection| Database
    SQLiteCommandEx -->|Uses Connection| ConnectionFactory
    SQLiteDataReaderEx -->|Query Result| SQLiteCommandEx
    SQLiteMaps -->|Object Mapping| SQLiteDataReaderEx
```

### EN

Internal structure of the framework: components and their interaction.

```mermaid
flowchart TD
    ConnectionFactory["ConnectionFactory / Connection Factory"]
    SQLiteCommandEx["SQLiteCommandEx / Command with Mapping"]
    SQLiteDataReaderEx["SQLiteDataReaderEx / Data Reader"]
    SQLiteMaps["SQLiteMaps / Object Mapping"]
    Database["SQLite Database"]

    ConnectionFactory -->|Creates Connection| Database
    SQLiteCommandEx -->|Uses Connection| ConnectionFactory
    SQLiteDataReaderEx -->|Query Result| SQLiteCommandEx
    SQLiteMaps -->|Object Mapping| SQLiteDataReaderEx
```

---

## 3. Схема потоков данных / Data Flow Diagram

### RU

Показывает поток данных через компоненты при выполнении запроса.

```mermaid
flowchart TD
    RequestNode["Запрос / Request"]
    ConnectionNode["ConnectionFactory.GetConnection()"]
    CommandTextNode["SQLiteCommandEx.SetCommandText()"]
    ExecuteReaderNode["SQLiteCommandEx.ExecuteReader()"]
    ReaderNode["SQLiteDataReaderEx.Read()"]
    MappingNode["SQLiteMaps.MapToObject()"]
    ResultNode["Результат / Result"]

    RequestNode --> ConnectionNode
    ConnectionNode --> CommandTextNode
    CommandTextNode --> ExecuteReaderNode
    ExecuteReaderNode --> ReaderNode
    ReaderNode --> MappingNode
    MappingNode --> ResultNode

    style RequestNode fill:#e1f5e1
    style ResultNode fill:#ffcccc
```

### EN

Shows data flow through components during query execution.

```mermaid
flowchart TD
    RequestNode["Request"]
    ConnectionNode["ConnectionFactory.GetConnection()"]
    CommandTextNode["SQLiteCommandEx.SetCommandText()"]
    ExecuteReaderNode["SQLiteCommandEx.ExecuteReader()"]
    ReaderNode["SQLiteDataReaderEx.Read()"]
    MappingNode["SQLiteMaps.MapToObject()"]
    ResultNode["Result"]

    RequestNode --> ConnectionNode
    ConnectionNode --> CommandTextNode
    CommandTextNode --> ExecuteReaderNode
    ExecuteReaderNode --> ReaderNode
    ReaderNode --> MappingNode
    MappingNode --> ResultNode

    style RequestNode fill:#e1f5e1
    style ResultNode fill:#ffcccc
```

---

## 4. Требования к структуре данных / Data Structure Requirements

### RU

Основные требования к хранению данных, взятые из технического задания.

| Параметр | Значение / Value |
|---|---|
| База данных | SQLite (встраиваемая БД) |
| Структура таблиц | Определяется в приложении № 3 к ТЗ |
| Индексы | Не менее 2 независимых внешних дисковых массива в горячем резерве |
| Резервное копирование | Физически отделено от места установки |

### EN

Data storage requirements from the technical specification.

| Parameter | Value |
|---|---|
| Database | SQLite (embedded DB) |
| Table Structure | Defined in Application Appendix № 3 to TZ |
| Indexes | At least 2 independent external disk arrays in hot reserve |
| Backup | Physically separated from installation location |

---

## 5. Анонимность / Anonymization Notice

Все реальные названия организаций, проектов, ФИО, годы и внутренние идентификаторы заменены на обобщённые обозначения. Документ подготовлен на основе извлечённых фактов без домыслов об отсутствующих параметрах.

---

## Ссылки на источники

- Требования: `/home/kate/technical-docs-library/03_API/Дискриптор-Требования.doc`
- Техническое задание: `/home/kate/technical-docs-library/03_API/тз.doc`
- Исходный код: `/home/kate/deshifrator-docs/sources/DbStationary.Data/`
- Диаграмма алгоритма: `/tmp/dbstationary_schemes/03_26 Алгоритм ПО модуля MC24RT.png`

---

*Документ подготовлен на основе извлечённых фактов без домыслов отсутствующих параметров.*  
*Document prepared based on extracted facts only, without guessing missing parameters.*

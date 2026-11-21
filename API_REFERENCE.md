# DbStationary API Reference / Справочник API DbStationary

**Repository:** `ekatmoz88-alt/dbstationary-architecture-docs`
**Source:** Extracted from `/home/kate/deshifrator-docs/sources/DbStationary.Data/`
**Anonymization:** All connection strings, parameter names exposing internal details replaced with placeholders.

---

## 1. Введение / Introduction

DbStationary — это C# фреймворк для работы с базами данных SQLite. Фреймворк предоставляет набор классов для управления соединениями, выполнения SQL-команд и чтения данных с маппингом на объекты приложения.

---

## 2. Классы и методы / Classes and Methods

### RU

#### 2.1. ConnectionFactory / Фабрика соединений

**Назначение:** Создание и управление singleton-экземпляром SQLiteConnection.

**Ключевой метод:**

| Метод | Описание |
|-------|----------|
| `GetConnection()` | Возвращает экземпляру соединения (singleton pattern) |

**Важное примечание:** Внедрение строки подключения через поле `ConnectionString`, которая в изначальном коде содержала путь к файлу базы данных. В анонимизированной версии путь к БД заменен на placeholder.

#### 2.2. SQLiteCommandEx / Расширенная команда

**Назначение:** Класс для выполнения SQL-команд с поддержкой маппинга результатов на объекты.

**Основные методы:**

| Метод | Описание |
|-------|----------|
| `SetCommandText(string cmd)` | Установка текста SQL-запроса |
| `ExecuteReader()` | Выполнение запроса и возврат данных для чтения |
| `SetMap(ResultMapDelegate resultMapDelegate)` | Настройка маппинга результата в объект |
| `SetTransaction(DbTransaction transaction)` | Установка транзакции |
| `SetConnection(DbConnection connection)` | Установка соединения |

**Делегат маппинга:**

```csharp
public delegate T ResultMapDelegate(SQLiteDataReaderEx reader);
```

#### 2.3. SQLiteDataReaderEx / Чтение данных

**Назначение:** Типизированный доступ к значениям, возвращаемым SQLiteDataReader.

**Основные методы чтения:**

| Метод | Описание |
|-------|----------|
| `Read()` | Переход к следующему ряду данных |
| Получение значений по индексу или имени колонки |

#### 2.4. SQLiteMaps / Маппинг моделей

**Назначение:** Маппинг значений из SQLiteDataReader в объекты приложения.

**Ключевой метод:** Настройка делегата маппинга для преобразования данных.

---

## 3. Примеры использования / Usage Examples

### RU

#### Пример 1: Получение соединения

```csharp
// Получение соединения через фабрику
var connection = ConnectionFactory.GetConnection();
```

#### Пример 2: Выполнение запроса с маппингом

```csharp
var cmd = new SQLiteCommandEx("SELECT * FROM users");
cmd.SetMap(reader => 
{
    return new UserModel
    {
        Id = reader.GetInt32(0),
        Name = reader.GetString(1)
    });
});
var result = cmd.ExecuteReader();
```

### EN

#### Example 1: Getting a Connection

```csharp
// Get connection via factory
var connection = ConnectionFactory.GetConnection();
```

#### Example 2: Executing a Query with Mapping

```csharp
var cmd = new SQLiteCommandEx("SELECT * FROM users");
cmd.SetMap(reader => 
{
    return new UserModel
    {
        Id = reader.GetInt32(0),
        Name = reader.GetString(1)
    });
});
var result = cmd.ExecuteReader();
```

---

## 4. Требования к использованию / Usage Requirements

### RU

- ConnectionString настраивается перед первым использованием фабрики
- Singleton-паттерн ConnectionFactory гарантирует одно соединение на весь lifecycle приложения
- SQLite database file должна быть доступна из рабочей директории приложения
- Для параллельного доступа рекомендуется настройка горячего резерва (см. требования в ARCHITECTURE.md)

### EN

- ConnectionString is configured before first use of the factory
- Singleton pattern ensures one connection for the entire application lifecycle
- SQLite database file must be accessible from the application working directory
- For parallel access, hot reserve configuration is recommended (see ARCHITECTURE.md)

---

## 5. Аннонимность / Anonymization Notice

Все строки подключения (ConnectionString), имена файлов базы данных, конкретные пути и внутренние идентификаторы заменены на обобщённые обозначения. Документ подготовлен на основе извлечённых фактов без домыслов об отсутствующих параметрах.

---
*Документ prepared based on extracted facts only, without guessing missing parameters.*
*Document prepared based on extracted facts only, without guessing missing parameters.*
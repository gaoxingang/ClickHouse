# SHOW Queries

## SHOW CREATE TABLE

```sql
SHOW CREATE [TEMPORARY] TABLE [db.]table [INTO OUTFILE filename] [FORMAT format]
```

Возвращает один столбец типа `String` с именем statement, содержащий одно значение — запрос `CREATE TABLE`, с помощью которого была создана указанная таблица.

## SHOW DATABASES {#show-databases}

```sql
SHOW DATABASES [INTO OUTFILE filename] [FORMAT format]
```

Выводит список всех баз данных.
Запрос полностью аналогичен запросу `SELECT name FROM system.databases [INTO OUTFILE filename] [FORMAT format]`.

## SHOW PROCESSLIST

```sql
SHOW PROCESSLIST [INTO OUTFILE filename] [FORMAT format]
```

Выводит содержимое таблицы [system.processes](../operations/system_tables.md#system_tables-processes), которая содержит список запросов, выполняющихся в данный момент времени, кроме самих запросов `SHOW PROCESSLIST`.

Запрос `SELECT * FROM system.processes` возвращает данные обо всех текущих запросах.

Полезный совет (выполните в консоли):

```bash
$ watch -n1 "clickhouse-client --query='SHOW PROCESSLIST'"
```

## SHOW TABLES

Выводит список таблиц.

```sql
SHOW [TEMPORARY] TABLES [FROM <db>] [LIKE '<pattern>'] [LIMIT <N>] [INTO OUTFILE <filename>] [FORMAT <format>]
```

Если секция `FROM` не используется, то запрос возвращает список таблиц из текущей базы данных.

Результат, идентичный тому, что выдаёт запрос `SHOW TABLES` можно получить также запросом следующего вида:

```sql
SELECT name FROM system.tables WHERE database = <db> [AND name LIKE <pattern>] [LIMIT <N>] [INTO OUTFILE <filename>] [FORMAT <format>]
```

**Пример**

Следующий запрос выбирает первые две строки из списка таблиц в базе данных `system`, чьи имена содержат `co`.

```sql
SHOW TABLES FROM system LIKE '%co%' LIMIT 2
```
```text
┌─name───────────────────────────┐
│ aggregate_function_combinators │
│ collations                     │
└────────────────────────────────┘
```

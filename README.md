## Подготовка PostgreSQL  
Перед запуском экспортера необходимо включить расширение `pg_stat_statements`  
Расширение включается в той базе данных, к которой планируется подключение (например, `postgres`)  
Создаем расширение:
```sql
CREATE EXTENSION IF NOT EXISTS pg_stat_statements;
```
В `postgresql.conf` добавить:

```conf
shared_preload_libraries = 'pg_stat_statements'
```
Путь к конфигу можно посмотреть выполнив команду в PostgreSQL:
```sql
SHOW config_file;
```
⚠️ После изменения требуется перезапуск PostgreSQL.

### Экспортер
- Склонировать проект на ВМ  
- В `pgscv.yaml` указать параметры подключения к БД

### Настройка Explain
shared_preload_libraries = 'pg_stat_statements, auto_explain'
```conf
#------------------------------------------------------------------------------
# EXPLAIN
#------------------------------------------------------------------------------
# Логировать всё, что дольше 3 сек
auto_explain.log_min_duration = 3000
# Добавляет к уже существующему плану выполнения фактические измерения выполнения
auto_explain.log_analyze = on
# Добавляет в лог информацию о том, какие буферы (RAM/кэш/диск) использовал запрос
auto_explain.log_buffers = on
# Логирование вложенных запросов внутри основного SQL-запроса
auto_explain.log_nested_statements = on

#------------------------------------------------------------------------------
# REPORTING AND LOGGING
#------------------------------------------------------------------------------
logging_collector = on
log_directory = 'log'
log_filename = 'postgresql-%Y-%m-%d.log'
```
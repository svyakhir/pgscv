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

### 3. Экспортер
- Склонировать проект на ВМ  
- В `pgscv.yaml` указать параметры подключения к БД

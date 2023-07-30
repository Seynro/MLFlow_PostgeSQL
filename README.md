
<<<<<<< HEAD
## Documentation for the automatic tracking script for changes in PostgreSQL using MLflow

### Description

This script is designed to automatically track and log changes in the `test_data3` table of the PostgreSQL database. Upon detecting changes, the script saves metrics and data in MLflow and also exports the data to Excel format.

### Prerequisites

- PostgreSQL
- MLflow
- Python (with installed libraries: `time`, `mlflow`, `pandas`, `sqlalchemy`, `os`, `tempfile`, `subprocess`)

### Functions

1. **save_csv_to_postgresql(csv_filename, db_url, table_name)**
   Saves a CSV file to a PostgreSQL database.
   
2. **save_mlflow_data_to_excel(experiment_id, output_filename)**
   Saves MLflow metrics to an Excel file.

3. **log_dataframe_as_artifact(data, artifact_name)**
   Logs a DataFrame in MLflow as an artifact.

4. **log_change_and_metrics_to_excel(change, data)**
   Records information about changes and metrics to an Excel file.

### Installation and Launch

1. Ensure you have all the necessary libraries and tools installed.
2. Set up the connection to the PostgreSQL database by specifying the correct parameters in the connection string.
3. Run the script.

### Usage Example

After starting the script, it will automatically start tracking changes in the `test_data3` table. As soon as changes are detected, the script will save the corresponding metrics and data.

### Setting up a Trigger and Function in PostgreSQL

#### Creating a Function

Before creating a trigger, you need to create a function that will be called by the trigger during a specific event:

```sql
CREATE OR REPLACE FUNCTION log_change()
RETURNS TRIGGER AS $$
BEGIN
    IF (TG_OP = 'DELETE') THEN
        INSERT INTO changes_log (operation, changed_data) VALUES ('DELETE', OLD::text);
        RETURN OLD;
    ELSIF (TG_OP = 'UPDATE') THEN
        INSERT INTO changes_log (operation, changed_data) VALUES ('UPDATE', NEW::text);
        RETURN NEW;
    ELSIF (TG_OP = 'INSERT') THEN
        INSERT INTO changes_log (operation, changed_data) VALUES ('INSERT', NEW::text);
        RETURN NEW;
    END IF;
    RETURN NULL;
END;
$$ LANGUAGE plpgsql;
```

#### Creating a Trigger

After creating the function, you can create a trigger:
=======
## Документация к скрипту автоматического отслеживания изменений в PostgreSQL с использованием MLflow

### Описание

Этот скрипт предназначен для автоматического отслеживания и логирования изменений в таблице `test_data3` базы данных PostgreSQL. При обнаружении изменений скрипт сохраняет метрики и данные в MLflow, а также экспортирует данные в формате Excel.

### Предварительные требования

- PostgreSQL
- MLflow
- Python (с установленными библиотеками: `time`, `mlflow`, `pandas`, `sqlalchemy`, `os`, `tempfile`, `subprocess`)

### Функции

1. **save_csv_to_postgresql(csv_filename, db_url, table_name)**
   Сохраняет CSV-файл в базе данных PostgreSQL.
   
2. **save_mlflow_data_to_excel(experiment_id, output_filename)**
   Сохраняет метрики MLflow в файл Excel.

3. **log_dataframe_as_artifact(data, artifact_name)**
   Логирует DataFrame в MLflow в качестве артефакта.

4. **log_change_and_metrics_to_excel(change, data)**
   Записывает информацию об изменениях и метриках в файл Excel.

### Установка и запуск

1. Убедитесь, что у вас установлены все необходимые библиотеки и инструменты.
2. Настройте соединение с базой данных PostgreSQL, указав корректные параметры в строке подключения.
3. Запустите скрипт.

### Пример использования

После запуска скрипта он автоматически начнет отслеживать изменения в таблице `test_data3`. Как только обнаружатся изменения, скрипт сохранит соответствующие метрики и данные.

### Настройка триггера и функции в PostgreSQL

#### Создание функции

Перед созданием триггера вам нужно создать функцию, которая будет вызываться триггером при определенном событии:

```sql
CREATE OR REPLACE FUNCTION log_change()
...
```

#### Создание триггера

После создания функции вы можете создать триггер:
>>>>>>> 84527301a22cc3bd93e57a5c91c356c7065337ae

- **INSERT**:
```sql
CREATE TRIGGER changes_after_insert
<<<<<<< HEAD
AFTER INSERT ON test_data3
FOR EACH ROW
EXECUTE FUNCTION log_change();
=======
...
>>>>>>> 84527301a22cc3bd93e57a5c91c356c7065337ae
```

- **UPDATE**:
```sql
CREATE TRIGGER changes_after_update
<<<<<<< HEAD
AFTER UPDATE ON test_data3
FOR EACH ROW
EXECUTE FUNCTION log_change();
=======
...
>>>>>>> 84527301a22cc3bd93e57a5c91c356c7065337ae
```

- **DELETE**:
```sql
CREATE TRIGGER changes_after_delete
<<<<<<< HEAD
AFTER DELETE ON test_data3
FOR EACH ROW
EXECUTE FUNCTION log_change();
```

#### Verifying the Operation

Perform INSERT, UPDATE, or DELETE operations on the `test_data3` table and ensure that the `log_change` function correctly logs these events.
=======
...
```

#### Проверка работы

Выполните операции INSERT, UPDATE или DELETE в таблице `test_data3` и убедитесь, что функция `log_change` корректно логирует эти события.
>>>>>>> 84527301a22cc3bd93e57a5c91c356c7065337ae

---


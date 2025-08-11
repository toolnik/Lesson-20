# 📦 My Python DB Project

Этот проект на **Python** подключается к базе данных, выполняет операции чтения и записи, и демонстрирует базовые/продвинутые техники работы с SQL.

## 🚀 Возможности
- Подключение к базе данных (PostgreSQL / MySQL / SQLite — выберите нужное)
- Выполнение SQL-запросов (SELECT, INSERT, UPDATE, DELETE)
- Чтение данных в удобные структуры Python (dict, pandas.DataFrame)
- Обработка ошибок подключения и запросов
- Настраиваемые параметры подключения через `.env` или конфигурационный файл

## 🛠 Технологии
- **Python** 3.10+
- [SQLAlchemy](https://www.sqlalchemy.org/) или [psycopg2](https://www.psycopg.org/)
- [python-dotenv](https://pypi.org/project/python-dotenv/) для загрузки конфигураций
- (Опционально) [pandas](https://pandas.pydata.org/) для анализа данных

## 📂 Структура проекта
```
my\_db\_project/
│
├── app/
│   ├── main.py          # Точка входа в приложение
│   ├── database.py      # Логика подключения к БД
│   ├── queries.py       # SQL-запросы или ORM-модели
│   └── utils.py         # Вспомогательные функции
│
├── .env                 # Конфигурация подключения (не коммитить!)
├── requirements.txt     # Зависимости
└── README.md
````

## ⚙️ Установка и запуск

1. **Клонируйте репозиторий**
```bash
git clone https://github.com/username/my_db_project.git
cd my_db_project
````

2. **Создайте виртуальное окружение и установите зависимости**

```bash
python -m venv venv
source venv/bin/activate   # Linux / macOS
venv\Scripts\activate      # Windows

pip install -r requirements.txt
```

3. **Создайте файл `.env`**

```env
DB_HOST=localhost
DB_PORT=5432
DB_NAME=my_database
DB_USER=my_user
DB_PASSWORD=my_password
```

4. **Запустите проект**

```bash
python app/main.py
```

## 📖 Пример подключения (database.py)

```python
import os
from sqlalchemy import create_engine
from dotenv import load_dotenv

load_dotenv()

DB_HOST = os.getenv("DB_HOST")
DB_PORT = os.getenv("DB_PORT")
DB_NAME = os.getenv("DB_NAME")
DB_USER = os.getenv("DB_USER")
DB_PASSWORD = os.getenv("DB_PASSWORD")

DATABASE_URL = f"postgresql://{DB_USER}:{DB_PASSWORD}@{DB_HOST}:{DB_PORT}/{DB_NAME}"

engine = create_engine(DATABASE_URL)

def test_connection():
    try:
        with engine.connect() as conn:
            result = conn.execute("SELECT 1")
            print("✅ Подключение успешно:", result.scalar())
    except Exception as e:
        print("❌ Ошибка подключения:", e)
```

## 🧪 Тестирование

```bash
pytest
```
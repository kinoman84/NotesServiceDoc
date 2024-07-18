### Таблицы

- **users**: Хранение информации о пользователях.
- **notes**: Хранение заметок, привязанных к пользователям.

### Таблица `users`

| Поле       | Тип данных   | Описание                               |
|------------|--------------|----------------------------------------|
| id         | UUID         | Уникальный идентификатор пользователя (первичный ключ) |
| login      | VARCHAR(255) | Логин пользователя                     |
| password   | VARCHAR(255) | Хэшированный пароль пользователя       |
| created_at | TIMESTAMP    | Дата и время создания пользователя     |
| updated_at | TIMESTAMP    | Дата и время последнего обновления     |

### Таблица `notes`

| Поле        | Тип данных   | Описание                               |
|-------------|--------------|----------------------------------------|
| id          | UUID         | Уникальный идентификатор заметки (первичный ключ) |
| user_id     | UUID         | Уникальный идентификатор пользователя (внешний ключ) |
| title       | VARCHAR(255) | Заголовок заметки                      |
| description | TEXT         | Описание заметки                       |
| status      | VARCHAR(50)  | Статус заметки (актуальна, архивная)   |
| created_at  | TIMESTAMP    | Дата и время создания заметки          |
| updated_at  | TIMESTAMP    | Дата и время последнего обновления     |

### SQL запросы для создания таблиц

```sql
-- Создание таблицы users
CREATE TABLE users (
    id UUID PRIMARY KEY,
    login VARCHAR(255) NOT NULL UNIQUE,
    password VARCHAR(255) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Создание таблицы notes
CREATE TABLE notes (
    id UUID PRIMARY KEY,
    user_id UUID REFERENCES users(id) ON DELETE CASCADE,
    title VARCHAR(255) NOT NULL,
    description TEXT NOT NULL,
    status VARCHAR(50) NOT NULL DEFAULT 'актуальна',
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Описание
- **users**: Таблица содержит информацию о пользователях, включая уникальный идентификатор, логин, хэшированный пароль и временные метки для создания и обновления записей.
- **notes**: Таблица содержит заметки, привязанные к пользователям через внешний ключ `user_id`. Заметка включает уникальный идентификатор, заголовок, описание, статус и временные метки для создания и обновления записей. Статус по умолчанию устанавливается как "актуальна".
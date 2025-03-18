# Database Structure

*Note: Associative tables are not explicitly listed but are implied where necessary.    
Polymorphic relationships are assumed where a `content_id` can reference multiple tables.*  
  
---  
  
## Table `users`  
**Description:** Users table.  
  
| Field        | Type        | Description                             |
| ------------ | ----------- | --------------------------------------- |
| `id`         | `INT`       | Primary key                             |
| `email`      | `STRING`    | Email (if provider provides us with it) |
| `name`       | `STRING`    | Name                                    |
| `avatar`     | `STRING`    | Link to avatar                          |
| `provider`   | `STRING`    | Google or GitHub provider               |
| `created_at` | `TIMESTAMP` | Time when the user registered           |
| `is_admin`   | `BOOLEAN`   | Is user an administrator?               |
| `is_active`  | `BOOLEAN`   | Is user active?                         |
  
**Relationships:**  
- `M:N` with `users` (friendship)  
- `M:N` with `chats`  
- `1:N` with `chat_messages`  
- `1:N` with `comments`  
- `1:N` with `favorites`  
- `1:N` with `playlists`  
- `1:N` with `collections` (if administrator)  
- `1:N` with `watch_parties` (owner)  
- `M:N` with `watch_parties` (participants)  
- `1:N` with `watch_parties_messages`  
- `1:N` with `watch_history`  

---  

## Table `chats`  
**Description:** Chats between users.  
  
| Field      | Type      | Description                    |
| ---------- | --------- | ------------------------------ |
| `id`       | `INT`     | Primary key                    |
| `name`     | `STRING`  | Chat name                      |
| `owner_id` | `INT`     | Foreign key to `users` (owner) |
| `is_group` | `BOOLEAN` | Whether this is a group chat   |
  
**Relationships:**  
- `1:N` with `chat_messages` (one chat has multiple messages)  
- `N:1` with `users` (owner)  
- `M:N` with `users` (participants)  
  
---  
  
## Table `chat_messages`  
**Description:** Chat messages.  
  
| Field       | Type        | Description                    |
| ----------- | ----------- | ------------------------------ |
| `id`        | `INT`       | Primary key                    |
| `chat_id`   | `INT`       | Foreign key to `chats`         |
| `sender_id` | `INT`       | Foreign key to `users`         |
| `text`      | `TEXT`      | Message text                   |
| `sent_at`   | `TIMESTAMP` | Time when the message was sent |
  
**Relationships:**  
- `N:1` with `users`  
- `N:1` with `chats`  
  
---  

## Table `comments`  
**Description:** Comments on films and TV series.  
  
| Field        | Type   | Description                        |
| ------------ | ------ | ---------------------------------- |
| `id`         | `INT`  | Primary key                        |
| `user_id`    | `INT`  | Foreign key to `users`             |
| `content_id` | `INT`  | Foreign key to `films` or `series` |
| `text`       | `TEXT` | Commentary text                    |
  
**Relationships:**  
- `N:1` with `users`  
- `N:1` with `films` or `series` (each comment belongs to one film/series)  
  
---  
  
## Table `favorites`  
**Description:** Featured movies and TV series from users.  
  
| Field     | Type  | Description            |
| --------- | ----- | ---------------------- |
| `id`      | `INT` | Primary key            |
| `user_id` | `INT` | Foreign key to `users` |
  
**Relationships:**  
- `N:1` with `users`  
- `M:N` with `films` or `series` (many favorites can contain many films and series)  
  
---  
  
## Table `playlists`  
**Description:** User playlists.  
  
| Field     | Type     | Description            |
| --------- | -------- | ---------------------- |
| `id`      | `INT`    | Primary key            |
| `user_id` | `INT`    | Foreign key to `users` |
| `name`    | `STRING` | Playlist name          |
  
**Relationships:**  
- `N:1` with `users`  
- `M:N` with `films` or `series` (many playlists can contain many films and series)  

---  

## Table `watch_parties`  
**Description:** User watch parties.  
  
| Field        | Type     | Description                        |
| ------------ | -------- | ---------------------------------- |
| `id`         | `INT`    | Primary key                        |
| `owner_id`   | `INT`    | Foreign key to `users`             |
| `content_id` | `INT`    | Foreign key to `films` or `series` |
| `name`       | `STRING` | Watch party name                   |

**Relationships:**  
- `N:1` with `users` (owner)  
- `M:N` with `users` (participants)  
- `N:1` with `films` or `series`  
- `1:N` with `watch_parties_messages`  
  
---  
  
## Table `watch_parties_messages`  
**Description:** Watch parties messages.  
  
| Field       | Type        | Description                    |
| ----------- | ----------- | ------------------------------ |
| `id`        | `INT`       | Primary key                    |
| `sender_id` | `INT`       | Foreign key to `users`         |
| `party_id`  | `INT`       | Foreign key to `watch_parties` |
| `text`      | `TEXT`      | Message text                   |
| `sent_at`   | `TIMESTAMP` | Time when the message was sent |
  
**Relationships:**  
- `N:1` with `users`  
- `N:1` with `watch_parties`  
  
---  
  
## Table `films`  
**Description:** Films table.  
  
| Field          | Type           | Description              |
| -------------- | -------------- | ------------------------ |
| `id`           | `INT`          | Primary key              |
| `title`        | `STRING`       | Film title               |
| `description`  | `STRING`       | Description              |
| `release_year` | `DATE`         | Year of release          |
| `rating`       | `DECIMAL(3,1)` | Rating                   |
| `duration`     | `INT`          | Film duration in minutes |
| `file_id`      | `INT`          | Foreign key to `files`   |
| `cover_id`     | `INT`          | Foreign key to `files`   |
  
**Relationships:**  
- `M:N` with `genres`  
- `1:N` with `comments`  
- `M:N` with `favorites`  
- `M:N` with `playlists`  
- `M:N` with `collections`  
- `1:N` with `watch_parties`  
- `1:1` with `files`
  
---  
  
## Table `genres`  
**Description:** Film genres.  
  
| Field  | Type     | Description |
| ------ | -------- | ----------- |
| `id`   | `INT`    | Primary key |
| `name` | `STRING` | Genre title |
  
**Relationships:**  
- `M:N` with `films` or `series` (each genre belongs to many films/series)  
  
---  
  
## Table `series`  
**Description:** TV series table.  
  
| Field          | Type           | Description     |
| -------------- | -------------- | --------------- |
| `id`           | `INT`          | Primary key     |
| `title`        | `STRING`       | Series title    |
| `description`  | `STRING`       | Description     |
| `release_year` | `DATE`         | Year of release |
| `rating`       | `DECIMAL(3,1)` | Rating          |

**Relationships:**  
- `M:N` with `genres`  
- `1:N` with `seasons`  
- `1:N` with `comments`  
- `M:N` with `favorites`  
- `M:N` with `playlists`  
- `M:N` with `collections`  
- `1:N` with `watch_parties`  

---  

## Table `seasons`  
**Description:** TV series seasons.  
  
| Field           | Type     | Description             |
| --------------- | -------- | ----------------------- |
| `id`            | `INT`    | Primary key             |
| `series_id`     | `INT`    | Foreign key to `series` |
| `title`         | `STRING` | Season title            |
| `season_number` | `INT`    | Season number           |
| `cover_id`      | `INT`    | Foreign key to `files`  |

**Relationships:**  
- `N:1` with `series`  
- `1:N` with `episodes`  
- `1:1` with `files`

---  
  
## Table `episodes`  
**Description:** Episodes of TV series.  
  
| Field            | Type     | Description                  |
| ---------------- | -------- | ---------------------------- |
| `id`             | `INT`    | Primary key                  |
| `season_id`      | `INT`    | Foreign key to `seasons`     |
| `title`          | `STRING` | Episode Title                |
| `episode_number` | `INT`    | Episode number in the season |
| `duration`       | `INT`    | Episode duration in minutes  |
| `file_id`        | `INT`    | Foreign key to `files`       |
  
**Relationships:**  
- `N:1` with `seasons`  
- `1:1` with `files`

---  
  
## Table `collections`  
**Description:** Stores films' and series' collections.  
  
| Field        | Type     | Description                        |
| ------------ | -------- | ---------------------------------- |
| `id`         | `INT`    | Primary key                        |
| `content_id` | `INT`    | Foreign key to `films` or `series` |
| `title`      | `STRING` | Collection title                   |
  
**Relationships:**  
- `N:1` with `users`  
- `M:N` with `films` or `series` (many collections can contain many films and series)  
  
---  
  
## Table `watch_history`  
**Description:** Stores users' watch history.  
  
| Field        | Type        | Description                          |
| ------------ | ----------- | ------------------------------------ |
| `id`         | `INT`       | Primary key                          |
| `user_id`    | `INT`       | Foreign key to `users`               |
| `content_id` | `INT`       | Foreign key to `films` or `series`   |
| `watched_at` | `TIMESTAMP` | Timestamp of when it was watched     |
| `progress`   | `INT`       | Watch progress in seconds (optional) |
  
**Relationships:**  
- `N:1` with `users` (each user has multiple watched items)  
- `N:1` with `films` or `series` (each watched item belongs to one film/series)  
  
---

## Table `files`  
**Description:** Stores films', series' and images' files information.

| Field        | Type        | Description                    |
| ------------ | ----------- | ------------------------------ |
| `id`         | `INT`       | Primary key                    |
| `url`        | `STRING`    | File path                      |
| `type`       | `STRING`    | File type (`video` or `image`) |
| `size`       | `INT`       | File size (in bytes)           |
| `created_at` | `TIMESTAMP` | Upload date                    |

**Relationships:**  
- `1:1` with `films`
- `1:1` with `seasons`
- `1:1` with `episodes`

# Warspaceman --- Git & Team Workflow

## Общий глоссарий и шпаргалка для Backend + Frontend

> Проект: `hack-84d3de81-warspaceman`\
> Backend: Python + Django REST Framework\
> Frontend: JavaScript + React\
> GitHub: общий удалённый репозиторий

------------------------------------------------------------------------

# 1. Наша базовая схема

Мы работаем в одном репозитории, но каждый разрабатывает в своей ветке:

``` text
                         GitHub
                           │
                    ┌──────┴──────┐
                    │             │
                  main       рабочие ветки
                                │
                         ┌──────┴──────┐
                         │             │
                 feature/backend  feature/frontend
                         │             │
                       Django         React
                         │             │
                         └──── API ────┘
```

### Что означает

-   `main` --- общая стабильная ветка.
-   `feature/backend` --- рабочая ветка backend-разработчика.
-   `feature/frontend` --- рабочая ветка frontend-разработчика.
-   Backend и frontend находятся в одном репозитории, но каждый работает
    в своей части проекта.
-   Не нужно каждый раз заново клонировать репозиторий.
-   `push` отправляет изменения в GitHub.
-   `pull` получает изменения из GitHub.
-   `merge` объединяет ветки.
-   `rebase` переносит текущие изменения поверх свежего состояния другой
    ветки.

------------------------------------------------------------------------

# 2. Главное правило

## Перед началом работы

Сначала убедиться, что ты находишься в своей ветке:

``` bash
git branch --show-current
```

Backend должен увидеть:

``` text
feature/backend
```

Frontend должен увидеть:

``` text
feature/frontend
```

Если находишься не там:

``` bash
git checkout feature/backend
```

или для frontend:

``` bash
git checkout feature/frontend
```

------------------------------------------------------------------------

# 3. Основные команды Git

## `git status`

Показывает текущее состояние проекта.

``` bash
git status
```

Использовать постоянно.

Показывает:

-   изменённые файлы;
-   новые файлы;
-   что уже добавлено в commit;
-   текущую ветку;
-   есть ли изменения, которые ещё не закоммичены.

------------------------------------------------------------------------

## `git branch`

Показывает локальные ветки:

``` bash
git branch
```

Текущая ветка отмечается `*`.

------------------------------------------------------------------------

## `git branch -a`

Показывает локальные и удалённые ветки:

``` bash
git branch -a
```

Например:

``` text
* feature/backend
  main
  remotes/origin/main
  remotes/origin/feature/frontend
  remotes/origin/feature/backend
```

------------------------------------------------------------------------

## `git branch --show-current`

Быстро узнать текущую ветку:

``` bash
git branch --show-current
```

------------------------------------------------------------------------

# 4. Clone

## `git clone`

Используется ОДИН РАЗ, когда человек ещё не скачал проект:

``` bash
git clone https://github.com/BAITC-Hacks/hack-84d3de81-warspaceman.git
```

После этого повторно клонировать проект не нужно.

Если проект уже есть на компьютере:

``` bash
cd hack-84d3de81-warspaceman
```

и дальше используется `pull`.

------------------------------------------------------------------------

# 5. Remote

## `git remote -v`

Проверяет, к какому GitHub-репозиторию подключён проект:

``` bash
git remote -v
```

Ожидается:

``` text
origin  https://github.com/BAITC-Hacks/hack-84d3de81-warspaceman.git (fetch)
origin  https://github.com/BAITC-Hacks/hack-84d3de81-warspaceman.git (push)
```

`origin` --- короткое имя нашего GitHub-репозитория.

------------------------------------------------------------------------

# 6. Fetch

## `git fetch`

Получает информацию о новых изменениях и ветках с GitHub, но не изменяет
текущие файлы:

``` bash
git fetch origin
```

Полезно перед проверкой состояния удалённых веток.

Пример:

``` bash
git fetch origin
git branch -a
```

------------------------------------------------------------------------

# 7. Pull

## `git pull`

Получает изменения из удалённой ветки и применяет их к текущей ветке.

Например:

``` bash
git pull origin main
```

Это значит:

> Получить свежий `main` с GitHub и применить его к текущей ветке.

### Важно

`git pull` НЕ означает:

> "получить вообще всё из GitHub".

Он работает с указанной веткой/настройкой upstream.

------------------------------------------------------------------------

# 8. Push

## `git push`

Отправляет наши commits на GitHub.

Например:

``` bash
git push origin feature/backend
```

Для frontend:

``` bash
git push origin feature/frontend
```

После этого другие участники смогут получить эти изменения.

------------------------------------------------------------------------

# 9. Commit

## `git commit`

Создаёт локальную точку сохранения изменений.

Обычно:

``` bash
git add .
git commit -m "feat: add authentication API"
```

Commit НЕ отправляет код на GitHub.

После commit ещё нужен:

``` bash
git push
```

------------------------------------------------------------------------

# 10. Add

## `git add`

Подготавливает изменения для commit.

Все изменения:

``` bash
git add .
```

Конкретный файл:

``` bash
git add backend/users/views.py
```

Проверить результат:

``` bash
git status
```

------------------------------------------------------------------------

# 11. Типичный цикл работы

Обычная работа:

``` bash
git status

# пишем код

git status
git add .
git commit -m "feat: add products API"
git push origin feature/backend
```

Для frontend:

``` bash
git status

# пишем код

git status
git add .
git commit -m "feat: add products page"
git push origin feature/frontend
```

------------------------------------------------------------------------

# 12. Commit message

Рекомендуемый формат:

``` text
type: description
```

Основные типы:

``` text
feat      новая функциональность
fix       исправление ошибки
refactor  изменение структуры без изменения поведения
docs      документация
test      тесты
chore     технические изменения
style     форматирование
```

Примеры:

``` bash
git commit -m "feat: add authentication API"
git commit -m "feat: add login page"
git commit -m "fix: correct user serializer"
git commit -m "fix: handle API error on login"
git commit -m "docs: update API documentation"
git commit -m "test: add authentication tests"
git commit -m "chore: update dependencies"
```

------------------------------------------------------------------------

# 13. Ветки

## Создание новой ветки

Например:

``` bash
git checkout -b feature/backend
```

Но если ветка уже существует, создавать её повторно не нужно.

------------------------------------------------------------------------

## Переключение ветки

``` bash
git checkout feature/backend
```

или:

``` bash
git checkout feature/frontend
```

------------------------------------------------------------------------

# 14. Наш обычный workflow

## Backend

Backend-разработчик:

``` bash
git checkout feature/backend
git status
```

Пишет Django/DRF.

После завершения части работы:

``` bash
git add .
git commit -m "feat: add users API"
git push origin feature/backend
```

------------------------------------------------------------------------

## Frontend

Frontend-разработчик:

``` bash
git checkout feature/frontend
git status
```

Пишет React.

После завершения части работы:

``` bash
git add .
git commit -m "feat: add users page"
git push origin feature/frontend
```

------------------------------------------------------------------------

# 15. Как получить изменения из `main`

Допустим, в `main` уже попали изменения backend/frontend.

Мы хотим обновить свою рабочую ветку.

### Backend

``` bash
git checkout feature/backend
git pull origin main --rebase
```

### Frontend

``` bash
git checkout feature/frontend
git pull origin main --rebase
```

После этого рабочая ветка содержит свежий `main`.

------------------------------------------------------------------------

# 16. Что означает `--rebase`

Команда:

``` bash
git pull origin main --rebase
```

означает:

> Возьми свежий `main` и аккуратно поставь мои локальные commits поверх
> него.

Упрощённо:

До:

``` text
main:             A---B---C
                         \
backend:                  D---E
```

После rebase:

``` text
main:             A---B---C
                         \
backend:                  D'---E'
```

История получается более линейной.

### Не использовать rebase без понимания

Особенно осторожно с rebase веток, которые уже активно используют другие
люди.

Для нашей схемы безопасный типичный случай:

``` bash
git checkout feature/backend
git pull origin main --rebase
```

когда мы хотим обновить свою рабочую ветку свежим `main`.

------------------------------------------------------------------------

# 17. Merge

## Что такое merge

Merge объединяет одну ветку с другой.

Например:

``` text
feature/backend
       ↓
      main
```

Когда backend готов, создаём Pull Request:

``` text
feature/backend → main
```

После проверки изменения объединяются с `main`.

То же самое:

``` text
feature/frontend → main
```

------------------------------------------------------------------------

# 18. Pull Request

Pull Request (PR) --- предложение:

> "Я закончил свою часть. Давайте добавим её в общую ветку."

Например:

``` text
feature/backend
        ↓
      Pull Request
        ↓
       main
```

PR удобен потому, что перед merge можно:

-   посмотреть изменения;
-   обсудить код;
-   найти ошибки;
-   проверить тесты;
-   убедиться, что ничего лишнего не добавлено.

------------------------------------------------------------------------

# 19. Как синхронизироваться после merge

Допустим:

``` text
feature/backend → main
```

был успешно merged.

Теперь frontend-разработчик хочет получить backend.

Он НЕ делает clone.

Он делает:

``` bash
git checkout feature/frontend
git pull origin main --rebase
```

Теперь:

``` text
feature/frontend
       ↑
       │
       └── содержит свежий main
```

Аналогично backend получает изменения frontend:

``` bash
git checkout feature/backend
git pull origin main --rebase
```

------------------------------------------------------------------------

# 20. Как тестировать backend + frontend вместе

Git не нужен для каждого API-запроса.

Обычно каждый запускает свою часть проекта.

## Backend

Например:

``` bash
uv run python manage.py runserver
```

Django:

``` text
http://127.0.0.1:8000/
```

API:

``` text
http://127.0.0.1:8000/api/
```

## Frontend

Например:

``` bash
npm run dev
```

React/Vite:

``` text
http://localhost:5173/
```

Получается:

``` text
React
localhost:5173
     │
     │ HTTP request
     ↓
Django REST API
localhost:8000
     │
     ↓
Database
```

То есть frontend обращается к локальному backend через HTTP.

------------------------------------------------------------------------

# 21. API Contract

Backend и frontend должны заранее договориться, какие API существуют.

Например:

``` text
POST /api/auth/login/
```

Request:

``` json
{
    "username": "test",
    "password": "password"
}
```

Response:

``` json
{
    "access": "...",
    "refresh": "...",
    "user": {
        "id": 1,
        "username": "test"
    }
}
```

Frontend может разрабатывать интерфейс под этот контракт.

### Главное правило

Не менять формат API молча.

Если backend меняет:

``` json
{
    "username": "test"
}
```

на:

``` json
{
    "user_name": "test"
}
```

frontend должен об этом знать.

------------------------------------------------------------------------

# 22. CORS

Если frontend:

``` text
localhost:5173
```

а backend:

``` text
localhost:8000
```

браузер считает это разными origins.

Поэтому Django должен разрешить frontend обращаться к API.

Для этого используется CORS.

Обычно проект использует `django-cors-headers`.

Не путать:

``` text
CORS ≠ Git
CORS ≠ API
CORS = правило браузера, разрешающее frontend обращаться к backend
```

------------------------------------------------------------------------

# 23. Что НЕ нужно делать

## Не нужно постоянно клонировать проект

Плохо:

``` text
написал код
↓
git clone
↓
снова git clone
↓
снова git clone
```

Нормально:

``` text
один раз git clone
↓
работа
↓
git pull
↓
работа
↓
git push
```

------------------------------------------------------------------------

## Не нужно передавать друг другу файлы через Telegram/архивы

Не:

``` text
backend.zip
frontend.zip
backend_final.zip
frontend_final_2.zip
```

GitHub должен быть источником общего кода.

------------------------------------------------------------------------

## Не нужно работать напрямую в `main`

По возможности:

``` text
main
 ├── feature/backend
 └── feature/frontend
```

------------------------------------------------------------------------

## Не нужно коммитить `.env`

Не:

``` text
.env
```

В `.gitignore` уже есть:

``` gitignore
.env
.env.*
!.env.example
```

Можно хранить:

``` text
.env.example
```

с примером переменных без настоящих секретов.

------------------------------------------------------------------------

# 24. Что должно попасть в Git

Обычно коммитим:

``` text
backend source code
frontend source code
Django migrations
pyproject.toml
uv.lock
package.json
package-lock.json
README.md
.env.example
```

Не коммитим:

``` text
.venv/
venv/
env/
__pycache__/
node_modules/
.env
*.sqlite3
*.log
.idea/
.vscode/
dist/
build/
```

------------------------------------------------------------------------

# 25. Django migrations

Для командной работы миграции обычно **коммитятся**.

Поэтому НЕ включаем:

``` gitignore
*/migrations/*.py
```

Ваш текущий `.gitignore` правильно оставляет эти строки
закомментированными:

``` gitignore
# */migrations/*.py
# !*/migrations/__init__.py
```

Когда backend меняет модели:

``` bash
uv run python manage.py makemigrations
uv run python manage.py migrate
```

После этого migration-файлы нужно добавить в Git:

``` bash
git add .
git commit -m "feat: add product model"
git push origin feature/backend
```

------------------------------------------------------------------------

# 26. Если появились изменения у другого человека

Ситуация:

Друг добавил изменения в `main`.

Ты продолжаешь работать в:

``` text
feature/backend
```

Перед началом следующей работы:

``` bash
git checkout feature/backend
git pull origin main --rebase
```

После этого продолжаешь работу.

------------------------------------------------------------------------

# 27. Если Git сообщает о конфликте

Например:

``` text
CONFLICT
```

Не паниковать и НЕ делать случайные команды.

Сначала:

``` bash
git status
```

Git покажет конфликтующие файлы.

В конфликтующем файле может быть:

``` text
<<<<<<< HEAD
твой вариант
=======
вариант из другой ветки
>>>>>>> ...
```

Нужно вручную решить, какой код должен остаться.

После исправления:

``` bash
git add <файл>
```

Если конфликт возник во время rebase:

``` bash
git rebase --continue
```

Если стало непонятно, как продолжать:

``` bash
git status
```

И сначала разобраться со статусом.

### Отмена rebase

Если rebase пошёл не так:

``` bash
git rebase --abort
```

Это возвращает состояние до начала rebase.

------------------------------------------------------------------------

# 28. Если случайно изменили не тот файл

Сначала:

``` bash
git status
```

Если изменение ещё не закоммичено, не использовать команды удаления
вслепую.

Для безопасной работы сначала посмотреть diff:

``` bash
git diff
```

------------------------------------------------------------------------

# 29. Посмотреть изменения

``` bash
git diff
```

Показывает незакоммиченные изменения.

После `git add`:

``` bash
git diff --staged
```

Показывает то, что попадёт в commit.

------------------------------------------------------------------------

# 30. Посмотреть историю

Короткая история:

``` bash
git log --oneline
```

Удобный вариант:

``` bash
git log --oneline --graph --decorate --all
```

------------------------------------------------------------------------

# 31. Быстрый чек-лист перед commit

``` bash
git status
git diff
git add .
git diff --staged
git commit -m "..."
git push origin <your-branch>
```

Не обязательно каждый раз использовать абсолютно все команды, но перед
важным commit полезно проверить diff.

------------------------------------------------------------------------

# 32. Быстрый чек-лист перед началом работы

``` bash
git checkout feature/backend
git pull origin main --rebase
git status
```

Для frontend:

``` bash
git checkout feature/frontend
git pull origin main --rebase
git status
```

После этого работать.

------------------------------------------------------------------------

# 33. Быстрый чек-лист после работы

``` bash
git status
git add .
git commit -m "feat: ..."
git push origin <your-branch>
```

------------------------------------------------------------------------

# 34. Полный пример: Backend

``` bash
# 1. Перейти в свою ветку
git checkout feature/backend

# 2. Получить свежий main
git pull origin main --rebase

# 3. Проверить состояние
git status

# 4. Пишем Django/DRF код

# 5. Проверяем изменения
git diff

# 6. Добавляем
git add .

# 7. Commit
git commit -m "feat: add authentication API"

# 8. Отправляем на GitHub
git push origin feature/backend
```

------------------------------------------------------------------------

# 35. Полный пример: Frontend

``` bash
# 1. Перейти в свою ветку
git checkout feature/frontend

# 2. Получить свежий main
git pull origin main --rebase

# 3. Проверить состояние
git status

# 4. Пишем React код

# 5. Проверяем изменения
git diff

# 6. Добавляем
git add .

# 7. Commit
git commit -m "feat: add login page"

# 8. Отправляем на GitHub
git push origin feature/frontend
```

------------------------------------------------------------------------

# 36. Когда backend готов для frontend

Backend-разработчик:

``` bash
git add .
git commit -m "feat: add products API"
git push origin feature/backend
```

После этого сообщает frontend-разработчику:

``` text
Products API готов.
Endpoint: GET /api/products/
```

Если API уже нужно использовать в общей версии проекта:

``` text
feature/backend
       ↓
      PR
       ↓
      main
```

После merge frontend получает изменения:

``` bash
git checkout feature/frontend
git pull origin main --rebase
```

------------------------------------------------------------------------

# 37. Когда frontend готов

Аналогично:

``` text
feature/frontend
       ↓
      PR
       ↓
      main
```

После merge backend получает изменения:

``` bash
git checkout feature/backend
git pull origin main --rebase
```

------------------------------------------------------------------------

# 38. Частые команды в одной таблице

  Команда                           Для чего
  --------------------------------- ---------------------------------------
  `git status`                      Посмотреть состояние
  `git branch`                      Посмотреть локальные ветки
  `git branch -a`                   Посмотреть все ветки
  `git branch --show-current`       Узнать текущую ветку
  `git checkout <branch>`           Переключить ветку
  `git checkout -b <branch>`        Создать и сразу переключить ветку
  `git clone <url>`                 Скачать репозиторий первый раз
  `git fetch origin`                Получить информацию с GitHub
  `git pull`                        Получить изменения
  `git pull origin main --rebase`   Обновить свою ветку свежим main
  `git add .`                       Подготовить изменения
  `git diff`                        Посмотреть изменения
  `git diff --staged`               Посмотреть подготовленные изменения
  `git commit -m "..."`             Создать commit
  `git push`                        Отправить commit на GitHub
  `git push origin <branch>`        Отправить конкретную ветку
  `git log --oneline`               Посмотреть историю
  `git merge <branch>`              Объединить ветки
  `git rebase <branch>`             Перенести commits поверх другой ветки
  `git rebase --abort`              Отменить текущий rebase
  `git remote -v`                   Посмотреть GitHub remote

------------------------------------------------------------------------

# 39. Самая короткая шпаргалка

## Начало дня

``` bash
git checkout feature/backend
git pull origin main --rebase
git status
```

или:

``` bash
git checkout feature/frontend
git pull origin main --rebase
git status
```

## Закончил фичу

``` bash
git add .
git commit -m "feat: description"
git push origin <your-branch>
```

## Нужно отправить код другому

``` text
push → GitHub → PR/merge → main → pull
```

## Нужно получить изменения друга

После его merge в `main`:

``` bash
git pull origin main --rebase
```

## Не нужно

``` text
git clone после каждого изменения
```

------------------------------------------------------------------------

# 40. Правило для хакатона

Когда начнётся активная разработка, держите в голове четыре уровня:

``` text
1. CODE
   ↓
2. COMMIT
   ↓
3. PUSH
   ↓
4. GITHUB / PR / MERGE
```

А для совместного тестирования:

``` text
React
localhost:5173
      ↓
     API
      ↓
Django REST Framework
localhost:8000
      ↓
   Database
```

Git отвечает за **код и его версионность**.

HTTP/API отвечает за **связь frontend ↔ backend**.

CORS отвечает за **разрешение браузеру делать такие запросы**.

Docker/CI/CD и другие инструменты можно добавить позже, если они реально
понадобятся.

------------------------------------------------------------------------

# 41. Текущий статус нашего проекта

На данный момент:

``` text
main
  └── .gitignore добавлен и отправлен на GitHub

feature/backend
  └── обновлена из main через rebase/fast-forward
```

Следующее действие:

``` bash
git status
git branch --show-current
```

Ожидаем:

``` text
feature/backend
```

После этого можно спокойно начинать backend-разработку.

------------------------------------------------------------------------

# 42. Золотые правила

1.  Один репозиторий --- не значит одна рабочая ветка.
2.  Каждый работает в своей feature-ветке.
3.  `main` держим максимально стабильным.
4.  Не клонируем проект заново после каждого push.
5.  Перед началом работы обновляем свою ветку из `main`.
6.  Перед push делаем commit.
7.  Не коммитим `.env`, `.venv`, `node_modules` и секреты.
8.  Django migrations обычно коммитим.
9.  Backend и frontend заранее согласуют API-контракт.
10. Если Git показывает `CONFLICT`, сначала `git status`, потом
    исправление, а не случайные команды.

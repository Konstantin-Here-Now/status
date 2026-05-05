# Server status site

Минималистичный сайт со статусом сервера и лентой новостей для GitHub Pages (Jekyll).

## Локальная проверка (Docker, Windows + Git Bash)

Запускать из корня проекта:

```bash
MSYS_NO_PATHCONV=1 docker run --rm -it \
  -p 4000:4000 \
  -v "/d/Programming/status:/srv/jekyll" \
  -w /srv/jekyll \
  jekyll/jekyll:latest \
  sh -lc "gem install webrick -N && jekyll serve --host 0.0.0.0 --port 4000 --livereload --no-watch"
```

Открыть в браузере: `http://127.0.0.1:4000`

Примечание: `MSYS_NO_PATHCONV=1` нужен, чтобы Git Bash не преобразовывал Linux-пути Docker в Windows-пути.

## Как добавить новость

Новости хранятся в файле `_data/news.yml`.

Добавьте новый элемент в начало или конец списка в формате:

```yml
- date: 2026-05-05 22:30
  title: Заголовок новости
  text: |
    Первая строка текста.
    Вторая строка текста.
  tags:
    - maintenance
    - network
```

Поля:
- `date` - дата и время в формате `YYYY-MM-DD HH:MM`
- `title` - заголовок новости
- `text` - основной текст (многострочный блок через `|`)
- `tags` - необязательный список меток

## Деплой в GitHub Pages

Сайт публикуется из ветки `master` через GitHub Pages.

Базовый процесс:
1. Проверить локально через Docker (команда выше)
2. Закоммитить изменения в `master`
3. Отправить изменения: `git push origin master`
4. Дождаться обновления страницы на GitHub Pages

URL проекта задан в `_config.yml`: `https://konstantin-here-now.github.io`


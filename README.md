# Email → AB группа (1–100)

Мини-тул для детерминированного разбиения e‑mail на бакеты 1–100 для A/B‑тестов.
Работает целиком в браузере (SHA‑256 через Web Crypto), сервер не нужен.

## Быстрый деплой (без CLI)

### Вариант A — Netlify (drag & drop)
1. Зайдите на https://app.netlify.com/ → Sites → **Add new site** → **Deploy manually**.
2. Перетащите файл `index.html` на страницу — сайт развернётся сразу.

### Вариант B — Cloudflare Pages
1. Зайдите на https://dash.cloudflare.com → **Pages** → **Create a project** → **Upload assets**.
2. Загрузите `index.html`. Framework preset: **None**.

### Вариант C — GitHub Pages (через репозиторий)
1. Создайте публичный репозиторий, добавьте `index.html` в корень, закоммитьте и запушьте.
2. В **Settings → Pages** выберите:
   - Build and deployment: **Deploy from a branch**
   - Branch: **main** / folder: **/** (root).
3. Дождитесь публикации, страница будет доступна по `https://<user>.github.io/<repo>/`.

## Локальный запуск
Просто откройте `index.html` двойным кликом — всё работает офлайн.

## Как это работает
- Нормализация: `trim → lowerCase`.
- Хэш: `SHA‑256` (Web Crypto), fallback — `FNV‑1a`.
- Маппинг: `(hash % 100) + 1` → диапазон 1..100.
- Параметр `key` (seed) меняет разбиение между экспериментами.

## Встраивание в ваш код
Скопируйте функцию через кнопку «Копия функции» на странице
или используйте:

```js
export async function abBucket(email, key = "") { /* см. index.html */ }
```

Удачных экспериментов!

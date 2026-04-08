# 🗺️ Новостной дашборд регионов России

Интерактивный дашборд для мониторинга региональных новостей России с агрегацией RSS-лент и Telegram-каналов.

## 🚀 Деплой на GitHub Pages

### Быстрый старт

1. **Создайте репозиторий** на GitHub (например, `russia-regions-dashboard`)

2. **Загрузите файлы:**
   ```bash
   git clone https://github.com/ВАШ_НИК/russia-regions-dashboard.git
   cd russia-regions-dashboard
   cp /path/to/index.html .
   git add .
   git commit -m "Initial dashboard"
   git push origin main
   ```

3. **Включите GitHub Pages:**
   - Settings → Pages → Source: `Deploy from branch`
   - Branch: `main` / `/ (root)`
   - Save

4. Дашборд будет доступен по адресу:
   `https://ВАШ_НИК.github.io/russia-regions-dashboard/`

---

## 📡 RSS-источники

### Федеральные СМИ
| Издание | RSS URL |
|---------|---------|
| ТАСС | `https://tass.ru/rss/v2.xml` |
| РИА Новости | `https://ria.ru/export/rss2/archive/index.xml` |
| Коммерсант | `https://www.kommersant.ru/RSS/main.xml` |
| Известия | `https://iz.ru/xml/rss/all.xml` |
| Интерфакс | `https://www.interfax.ru/rss.asp` |
| Российская газета | `https://rg.ru/xml/index.xml` |

### Государственные ведомства
| Ведомство | RSS URL |
|-----------|---------|
| Kremlin.ru | `http://kremlin.ru/events/all/feed` |
| Правительство РФ | `http://government.ru/all/rss/` |
| Минэкономразвития | `https://economy.gov.ru/material/rss.xml` |
| Минфин | `https://minfin.gov.ru/ru/press-center/rss/` |
| Минздрав | `https://minzdrav.gov.ru/news/feed` |
| Роспотребнадзор | `https://rospotrebnadzor.ru/rss` |
| Росстат | `https://rosstat.gov.ru/rss` |

### Региональные порталы
| Регион | СМИ / RSS | Госпортал / RSS |
|--------|-----------|-----------------|
| Москва | M24 — `https://www.m24.ru/rss.xml` | `https://www.mos.ru/news/rss.xml` |
| СПб | Фонтанка — `https://www.fontanka.ru/fontanka.rss` | `https://www.gov.spb.ru/rss/` |
| Новосибирск | NSK.ru — `https://nsk.ru/rss` | `https://www.nso.ru/rss` |
| Екатеринбург | Е1.ру — `https://www.e1.ru/export/rss.xml` | `https://midural.ru/rss` |
| Краснодар | НГ-Кубань — `https://ngkuban.ru/rss` | `https://admkrai.krasnodar.ru/rss` |
| Красноярск | NGS24 — `https://ngs24.ru/rss/all` | `https://www.krskstate.ru/rss` |
| Казань | KazanFirst — `https://kazanfirst.ru/rss` | `https://tatarstan.ru/rss` |
| Ростов-на-Дону | Donnews — `https://www.donnews.ru/rss.xml` | `https://www.donland.ru/rss` |
| Нижний Новгород | NN.ru — `https://nn.ru/rss` | `https://government-nnov.ru/rss` |
| Самара | 63.ru — `https://63.ru/rss/all` | `https://www.samregion.ru/rss` |

---

## ✈️ Telegram-каналы

### Федеральные
- `@vchkogpu` — ВЧК-ОГПУ
- `@readovkanews` — Readovka
- `@russica2` — НЕЗЫГАРЬ
- `@bazabazon` — Baza
- `@breakingmash` — Mash

### Региональные
- `@eoblast` — Е-область (Свердловская)
- `@tatarstan24` — Татарстан 24
- `@yugru` — Юг.ру (Краснодар)
- `@govoritmsk` — Говорит Москва
- `@piterofficial` — Питер Online
- `@novosibirsk_online` — НовосибирскОнлайн

---

## ⚙️ Расширенная интеграция (опционально)

Для получения реальных RSS-данных в браузере (из-за CORS) используйте прокси:

### Вариант 1: RSS2JSON API (бесплатно)
```javascript
const proxy = 'https://api.rss2json.com/v1/api.json?rss_url=';
const feed = await fetch(proxy + encodeURIComponent(RSS_URL));
const data = await feed.json();
```

### Вариант 2: allorigins.win
```javascript
const proxy = 'https://api.allorigins.win/get?url=';
const response = await fetch(proxy + encodeURIComponent(RSS_URL));
```

### Вариант 3: GitHub Actions (автообновление)
Создайте `.github/workflows/update-news.yml` для периодического сбора новостей:
```yaml
name: Update News
on:
  schedule:
    - cron: '*/30 * * * *'  # каждые 30 минут
  workflow_dispatch:
jobs:
  fetch:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Fetch RSS
        run: node scripts/fetch-rss.js
      - name: Commit data
        run: |
          git config --global user.email "bot@github.com"
          git config --global user.name "News Bot"
          git add data/
          git diff --staged --quiet || git commit -m "Update news data"
          git push
```

---

## 📁 Структура проекта

```
russia-regions-dashboard/
├── index.html              # Главный дашборд
├── README.md               # Этот файл
├── data/
│   └── news.json           # Кешированные новости (опционально)
├── scripts/
│   └── fetch-rss.js        # Node.js скрипт для сбора RSS
└── .github/
    └── workflows/
        └── update-news.yml # Автообновление
```

---

## 🛠️ Технологии

- Чистый HTML/CSS/JS — без фреймворков
- Работает как статический сайт на GitHub Pages
- SVG-карта регионов
- Встроенные RSS-источники + Telegram-каналы
- Адаптивный дизайн

---

## 📄 Лицензия

MIT

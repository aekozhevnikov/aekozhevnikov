# README.md Updater Skill

## Назначение
Этот скилл автоматически генерирует и обновляет файл README.md в репозитории github_profile на основе данных о стеке технологий и контактах, хранящихся в конфигурации портфолио.

## Источник данных
Файл конфигурации портфолио:
- Путь: /Users/antonkozevnikov/development/TypeScript/portfolio/src/config/site.config.ts
- Экспортируемые данные:
  - skills - объект с полем categories (массив SkillCategory)
  - socials - массив соцсетей (SocialLink[])
  - email - строка с email-адресом

## Выходной файл
- Путь: /Users/antonkozevnikov/development/github_profile/README.md

## Инструкции для агента

### 1. Чтение конфигурации
1. Прочитать файл /Users/antonkozevnikov/development/TypeScript/portfolio/src/config/site.config.ts
2. Извлечь:
   - Массив skills.categories - каждая категория содержит category (ключ локализации) и skills (массив объектов с language, icon, variant, level)
   - Массив socials - каждая запись содержит name, icon, color, link
   - Переменную email

### 2. Сопоставление категорий
Преобразовывать ключи категорий в заголовки секций:
- expertise.programmingLanguages -> Programming Languages
- expertise.frontend -> Frontend & Mobile
- expertise.backend -> Backend & Frameworks
- expertise.databases -> Databases
- expertise.devops -> Infrastructure & DevOps
- expertise.testing -> Testing & QA
- expertise.cicd -> CI/CD & Automation

### 3. Сопоставление уровней навыков
Преобразовывать уровни в текст для badge:
- expert -> Expert
- advanced -> Advanced
- intermediate -> Intermediate
- beginner -> Beginner

### 4. Сопоставление иконок и цветов
Использовать соответствие из текущего README.md для badge цветов и имен иконок (логотипов).
Полный список цветов и иконок для каждого навыка определен в таблице ниже:

| Навык | Цвет | Иконка |
|---|---|---|
| JavaScript | #F7DF1E | javascript |
| TypeScript | #3178C6 | typescript |
| Python | #3776AB | python |
| Bash | #4EAA25 | gnu-bash |
| HTML5 | #E34F26 | html5 |
| CSS3 | #1572B6 | css3 |
| SCSS | #CC6699 | sass |
| Swift | #FA7343 | swift |
| Dart | #0175C2 | dart |
| Go | #00ADD8 | go |
| Google App Script | #4285F4 | google |
| Vue.js | #4FC08D | vuedotjs |
| Quasar | #1976D2 | quasar |
| React | #61DAFB | react |
| Next.js | #000000 | nextdotjs |
| Flutter | #02569B | flutter |
| Tailwind CSS | #06B6D4 | tailwindcss |
| React Native | #61DAFB | react |
| Node.js | #339933 | nodedotjs |
| Express | #000000 | express |
| FastAPI | #009688 | fastapi |
| Prisma | #2D3748 | prisma |
| SQLAlchemy | #D71F00 | sqlalchemy |
| NATS | #23B5AF | nats |
| Deno | #000000 | deno |
| Aiogram | #2CA5E0 | telegram |
| OpenAPI | #6BA539 | openapiinitiative |
| PostgreSQL | #4169E1 | postgresql |
| SQLite | #003B57 | sqlite |
| Firebase | #FFCA28 | firebase |
| Redis | #DC382D | redis |
| S3 | #569A31 | amazons3 |
| Git | #F05032 | git |
| Docker | #2496ED | docker |
| AWS | #232F3E | amazonwebservices |
| GCP | #4285F4 | googlecloud |
| Azure | #0078D4 | microsoftazure |
| Vercel | #000000 | vercel |
| Netlify | #00C7B7 | netlify |
| Supabase | #3ECF8E | supabase |
| Yandex Cloud | #FFCC00 | yandexcloud |
| Kubernetes | #326CE5 | kubernetes |
| Puppeteer | #40B5A4 | puppeteer |
| Traefik | #24A1C1 | traefikproxy |
| NGINX | #009639 | nginx |
| Vault | #FFEC6E | vault |
| Ansible | #EE0000 | ansible |
| Grafana | #F46800 | grafana |
| Prometheus | #E6522C | prometheus |
| Loki | #F46800 | grafana |
| Alertmanager | #E6522C | prometheus |
| Jest | #C21325 | jest |
| Pytest | #0A9EDC | pytest |
| Cypress | #19A975 | cypressio |
| Vitest | #6E9F18 | vitest |
| Playwright | #2EAD33 | playwright |
| Selenium | #43B02A | selenium |
| GitHub Actions | #2088FF | githubactions |
| GitLab CI | #FC6D26 | gitlab |
| Git Hooks | #F05032 | git |

### 5. Генерация README.md
Сгенерировать README.md по шаблону с сохранением структуры:

1. Header capsule (статичный) - визуальная шапка с именем и описанием
2. Contact Information - из socials и email:
   - Portfolio link
   - Email
   - Telegram ссылки из socials
3. Technology Stack - из skills.categories:
   - Для каждой категории: заголовок и badge для каждого навыка
   - Формат badge: ![Language](https://img.shields.io/badge/Language-Level-COLOR?style=flat&logo=ICON&logoColor=white)
4. GitHub Analytics (статичный) - стандартные бейджики статистики GitHub
5. Development Focus (статичный) - core competencies и current focus
6. Quick Stats & Connect - из socials:
   - Статистика просмотров профиля и подписчиков
   - Ссылки на соцсети в виде badge с кнопками

### 6. Запись результата
Записать сгенерированный контент в /Users/antonkozevnikov/development/github_profile/README.md, заменяя существующее содержимое.

## Триггер
Скилл активируется командой /readme-md-updater.

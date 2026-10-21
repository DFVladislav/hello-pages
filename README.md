# 🚀 Hello Pages

**Деплой React SPA (Vite + TypeScript) на живой URL через GitHub Pages, Environments и Deployments.**

[![CI/CD](https://github.com/DFVladislav/hello-pages/actions/workflows/ci-cd.yml/badge.svg)](https://github.com/DFVladislav/hello-pages/actions/workflows/ci-cd.yml)
[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen?logo=github)](https://DFVladislav.github.io/hello-pages/)

---

## 📖 О проекте

Этот проект — наглядный пример **настоящего Continuous Deployment (CD)** для React-приложения. Сайт собирается с помощью **Vite**, тестируется через **Vitest** и автоматически деплоится на **GitHub Pages**.

**Что реализовано:**
- **Continuous Integration (CI):** Проверка типов (`tsc`), линтер (`eslint`), тесты (`vitest`) и сборка (`vite build`).
- **Continuous Deployment (CD):** Автоматическая выгрузка папки `dist` на GitHub Pages, но **только если CI прошел успешно** (гейтинг `needs: ci`).
- **GitHub Environments:** Деплой привязан к окружению `github-pages`.

### 🖥 Живой сайт и скриншоты

*Сайт доступен по адресу: [https://DFVladislav.github.io/hello-pages/](https://DFVladislav.github.io/hello-pages/)*

**Скриншот сайта:**
![Сайт](docs/screenshot-site.png)

**Успешный пайплайн (CI/CD):**
![Actions](docs/screenshot-actions.png)

**История деплоев (Environments):**
![Environments](docs/screenshot-environments.png)

---

## 🛠 Стек технологий

- **React 18** — библиотека для создания пользовательских интерфейсов.
- **Vite** — современный сборщик, обеспечивающий мгновенную горячую замену модулей (HMR).
- **TypeScript** — типизированный JavaScript для надежности кода.
- **Vitest** — сверхбыстрый фреймворк для юнит-тестирования.
- **ESLint** — статический анализ кода для поиска проблем.
- **GitHub Actions** — CI/CD платформа для автоматизации.

---

## 📁 Структура проекта

```text
hello-pages/
├── .github/workflows/
│   └── ci-cd.yml            # Пайплайн CI/CD
├── public/                  # Статические файлы (favicon)
├── src/                     # Исходники React
│   ├── components/          # Переиспользуемые компоненты (Header, About, Projects)
│   ├── App.tsx              # Корневой компонент
│   ├── App.test.tsx         # Тесты
│   ├── main.tsx             # Точка входа
│   └── index.css            # Глобальные стили
├── .gitignore
├── index.html               # HTML-шаблон
├── package.json
├── tsconfig.json
└── vite.config.ts           # Конфигурация Vite (включая base path)
```

---

## ⚙️ Как это работает (Этапы CI/CD)

Пайплайн описан в файле `.github/workflows/ci-cd.yml` и состоит из двух последовательных джоб:

### 1. Валидация и сборка (Job: `ci`)
Запускается при каждом пуше в `main` или создании Pull Request.
1. Устанавливаются зависимости через `npm ci` (строгая установка по `package-lock.json`).
2. Запускается линтер (`npm run lint`) и проверка типов (`npm run type-check`).
3. Прогоняются тесты (`npm test`).
4. Выполняется production-сборка (`npm run build`).
5. Готовая папка `dist` сохраняется как артефакт (`actions/upload-artifact`).

### 2. Деплой (Job: `deploy`)
Имеет параметр `needs: ci`. Это значит, что **деплой не запустится, если тесты или сборка упали**.
1. Скачивается артефакт `dist` (без повторной сборки).
2. С помощью `actions/deploy-pages` сайт выкладывается на серверы GitHub.
3. Действие привязывается к окружению `github-pages`.

> **Особенность GitHub Pages:** В `vite.config.ts` жестко задан параметр `base: '/hello-pages/'`. Это обязательно, чтобы пути к CSS и JS файлам формировались корректно с учетом подпапки репозитория.

---

## 🚀 Локальная разработка

### Требования
- Node.js (версия 20+)

### 1. Установка зависимостей
```bash
npm install
```

### 2. Проверка кода
```bash
npm run lint
npm run type-check
npm run test
```

### 3. Запуск в режиме разработки
```bash
npm run dev
```
Откройте `http://localhost:5173/hello-pages/`

### 4. Сборка и предпросмотр
```bash
npm run build
npm run preview
```

---

## 🔄 Как обновить сайт

1. Внесите изменения в файлы внутри папки `src/`.
2. Сделайте коммит и пуш:
   ```bash
   git add .
   git commit -m "feat: update content"
   git push origin main
   ```
3. Перейдите во вкладку **Actions**. После успешного прохождения CI, изменения автоматически уедут на живой сайт.


### СКРИНШОТЫ 
<img width="1522" height="456" alt="изображение" src="https://github.com/user-attachments/assets/a1ec95f2-b3a3-416d-a473-b14e188efb5c" />
<img width="1533" height="834" alt="изображение" src="https://github.com/user-attachments/assets/e93f30c2-e129-4087-a8f7-1701ed56a804" />
<img width="1536" height="537" alt="изображение" src="https://github.com/user-attachments/assets/2956fb5a-ee9b-4183-9d4c-7d2fcbc630e2" />


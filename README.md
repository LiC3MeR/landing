# Developer Portfolio

Современный landing для разработчика с Vue 3, Vite и Tailwind CSS.

## Структура проекта

```
/
├── src/
│   ├── App.vue           # Главный компонент
│   ├── main.js          # Точка входа
│   ├── style.css        # Глобальные стили
│   └── data.json        # Данные портфолио (редактируй эту файл)
├── public/              # Статические файлы
├── dist/                # Собранный проект (после build)
├── index.html           # HTML шаблон
├── vite.config.js       # Конфигурация Vite
├── tailwind.config.js   # Конфигурация Tailwind
├── nginx.conf           # Конфигурация для nginx
└── package.json         # Зависимости
```

## Быстрый старт

### 1. Установка зависимостей
```bash
npm install
```

### 2. Редактирование данных
Открой `src/data.json` и отредактируй:
- Основная информация (имя, должность, описание)
- Секция "О себе"
- Навыки и уровень владения
- Опыт работы
- Контакты

### 3. Запуск для разработки
```bash
npm run dev
```
Откроется на http://localhost:3000

### 4. Сборка для production
```bash
npm run build
```

## Публикация на nginx

### 1. Скопируй собранный проект на сервер
```bash
scp -r dist/* user@your-server:/var/www/landing/
```

### 2. Скопируй конфигурацию nginx
```bash
sudo cp nginx.conf /etc/nginx/sites-available/landing
sudo ln -s /etc/nginx/sites-available/landing /etc/nginx/sites-enabled/landing
```

### 3. Замени `your-domain.com` на твой домен в `nginx.conf`

### 4. Перезагрузи nginx
```bash
sudo nginx -t
sudo systemctl restart nginx
```

## Дополнительно

### Для HTTPS с Let's Encrypt:
```bash
sudo certbot certonly --standalone -d your-domain.com
```

Затем раскомментируй HTTPS блок в `nginx.conf`.

### Для изменения фотографии:
1. Загрузи фото в `public/` (например, `photo.jpg`)
2. Изменить путь в `src/data.json`:
   ```json
   "photoUrl": "/photo.jpg"
   ```

### Цветовая схема:
Цвета установлены в `src/data.json` для каждого опыта работы (`color: "purple"/"blue"/"green"`). Или отредактируй переменные в `src/style.css`.

#--- docker build -t my-node-app .
#--- docker run --rm -p 3000:3000 my-node-app

FROM base_image

# Установка Node.js
RUN apt-get update && apt-get install -y nodejs npm

# Создание рабочей директории
WORKDIR /app

# Копирование файлов приложения
COPY . .

# Установка зависимостей
RUN npm install

# Запуск приложения
CMD ["node", "app.js"]


Конечно, вы можете передать переменные окружения в различные скрипты из вашего `package.json` и использовать их в приложении Vite. Давайте рассмотрим, как это можно сделать для разных сценариев: сборка приложения, запуск в режиме разработки и использование в Docker.

### 1. Передача переменных окружения в скрипты сборки и запуска из `package.json`

#### Пример `package.json`

```json
{
  "scripts": {
    "build": "vite build",
    "dev": "vite"
  }
}
```

#### Передача переменных окружения в скрипты

В `package.json` вы можете использовать переменные окружения напрямую в скриптах. Например:

```json
{
  "scripts": {
    "build": "VITE_API_URL=$VITE_API_URL vite build",
    "dev": "VITE_API_URL=$VITE_API_URL vite"
  }
}
```

### 2. Передача переменных окружения в пайплайн `.gitlab-ci.yml`

#### Пример `.gitlab-ci.yml`

```yaml
variables:
  VITE_API_URL: "https://api.example.com"
  VITE_ENVIRONMENT: "production"

stages:
  - build
  - deploy

build_front_app:
  stage: build
  script:
    - npm install
    - npm run build
  artifacts:
    paths:
      - dist/

deploy_front_app:
  stage: deploy
  script:
    - echo "Deploying the application..."
  dependencies:
    - build_front_app
```

#### Объяснение:

- **Переменные окружения:** `VITE_API_URL` и `VITE_ENVIRONMENT` определены в разделе `variables`.
- **Сборка:** В скрипте сборки используется команда `npm run build`, которая автоматически передаст переменные окружения из пайплайна в скрипт сборки Vite.

### 3. Передача переменных окружения в Docker Compose и Dockerfile

#### Пример `Dockerfile`

```Dockerfile
# Dockerfile
FROM node:14

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Передача переменных окружения в скрипт dev
CMD ["npm", "run", "dev"]
```

#### Пример `docker-compose.yml`

```yaml
# docker-compose.yml
version: '3.8'

services:
  frontend:
    build: .
    environment:
      - VITE_API_URL=https://api.example.com
      - VITE_ENVIRONMENT=development
    ports:
      - "3000:3000"
```

#### Объяснение:

- **Dockerfile:** Команда `CMD` запускает скрипт `dev`, который получает переменные окружения из `docker-compose.yml`.
- **Docker Compose:** В разделе `environment` определены переменные окружения, которые будут доступны в контейнере.

### 4. Использование переменных окружения в приложении Vite

В приложении Vite вы можете использовать переменные окружения через `import.meta.env`.

#### Пример использования в коде Vite

```javascript
// В вашем приложении Vite
console.log(import.meta.env.VITE_API_URL);
console.log(import.meta.env.VITE_ENVIRONMENT);
```

### Полный пример

#### `package.json`

```json
{
  "scripts": {
    "build": "vite build",
    "dev": "vite"
  }
}
```

#### `.gitlab-ci.yml`

```yaml
variables:
  VITE_API_URL: "https://api.example.com"
  VITE_ENVIRONMENT: "production"

stages:
  - build
  - deploy

build_front_app:
  stage: build
  script:
    - npm install
    - npm run build
  artifacts:
    paths:
      - dist/

deploy_front_app:
  stage: deploy
  script:
    - echo "Deploying the application..."
  dependencies:
    - build_front_app
```

#### `Dockerfile`

```Dockerfile
# Dockerfile
FROM node:14

WORKDIR /app

COPY package*.json ./

RUN npm install

COPY . .

# Передача переменных окружения в скрипт dev
CMD ["npm", "run", "dev"]
```

#### `docker-compose.yml`

```yaml
# docker-compose.yml
version: '3.8'

services:
  frontend:
    build: .
    environment:
      - VITE_API_URL=https://api.example.com
      - VITE_ENVIRONMENT=development
    ports:
      - "3000:3000"
```

### Объяснение полного примера:

- **Переменные окружения:** Определены в `.gitlab-ci.yml` и `docker-compose.yml`.
- **Сборка:** В скрипте сборки (`npm run build`) переменные окружения передаются автоматически.
- **Запуск в режиме разработки:** В `docker-compose.yml` переменные окружения передаются контейнеру, который запускает `npm run dev`.
- **Использование в коде:** В приложении Vite переменные окружения доступны через `import.meta.env`.

Таким образом, вы можете успешно передавать переменные окружения из CI/CD пайплайна, Docker Compose и Dockerfile в скрипты сборки и запуска, а затем использовать их в приложении Vite.

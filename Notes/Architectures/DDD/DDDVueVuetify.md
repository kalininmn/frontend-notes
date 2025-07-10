## Пример реализации DDD в Vue SPA с Vuetify

### Структура проекта

```
src/
├── app/
│   ├── core/                  # Ядро приложения
│   │   ├── domain/           # Доменная логика
│   │   │   ├── entities/     # Бизнес-сущности
│   │   │   └── value-objects/
│   │   ├── application/      # Прикладной слой
│   │   └── infrastructure/   # Инфраструктурный слой
│   ├── ui/                   # Пользовательский интерфейс
│   │   ├── components/
│   │   └── pages/
│   └── services/             # Сервисы
├── shared/                   # Общие компоненты
└── store/                   # Управление состоянием
```

### Доменный слой (Domain)

**Пример сущности User:**
```typescript
// domain/entities/User.ts
export class User {
  private id: string;
  private name: string;
  private email: string;

  constructor(id: string, name: string, email: string) {
    this.id = id;
    this.name = name;
    this.email = email;
  }

  // Методы валидации и бизнес-логики
}
```

### Прикладной слой (Application)

**Пример порта:**
```typescript
// application/ports/UserRepository.ts
export interface UserRepository {
  getUserById(id: string): Promise<User>;
  saveUser(user: User): Promise<void>;
}

// application/services/UserService.ts
export class UserService {
  constructor(private userRepository: UserRepository) {}

  async createUser(name: string, email: string): Promise<User> {
    const user = new User(uuidv4(), name, email);
    await this.userRepository.saveUser(user);
    return user;
  }
}
```

### Инфраструктурный слой

**Пример адаптера:**
```typescript
// infrastructure/adapters/UserDBAdapter.ts
import { UserRepository } from '../application/ports/UserRepository';

export class UserDBAdapter implements UserRepository {
  async getUserById(id: string): Promise<User> {
    // Реализация получения данных из БД
  }

  async saveUser(user: User): Promise<void> {
    // Реализация сохранения в БД
  }
}
```

### Пользовательский интерфейс (UI)

**Пример компонента с Vuetify:**
```vue
<!-- ui/components/UserForm.vue -->
<template>
  <v-form @submit.prevent="submit">
    <v-text-field
      v-model="name"
      label="Имя"
      required
    ></v-text-field>
    <v-text-field
      v-model="email"
      label="Email"
      required
    ></v-text-field>
    <v-btn type="submit">
      Сохранить
    </v-btn>
  </v-form>
</template>

<script setup>
import { ref } from 'vue';
import { useUserService } from '@/app/core/application/services/UserService';

const name = ref('');
const email = ref('');
const userService = useUserService();

async function submit() {
  try {
    await userService.createUser(name.value, email.value);
  } catch (error) {
    // Обработка ошибок
  }
}
</script>
```

### Интеграция с гексагональной архитектурой

**Пример портов и адаптеров:**
```typescript
// ports/UserPort.ts
export interface UserPort {
  createUser(user: User): Promise<void>;
  getUser(id: string): Promise<User>;
}

// adapters/UserAdapter.ts
import { UserPort } from './ports/UserPort';
import { UserService } from '@/app/core/application/services/UserService';

export class UserAdapter implements UserPort {
  constructor(private userService: UserService) {}

  async createUser(user: User): Promise<void> {
    return this.userService.createUser(user);
  }

  async getUser(id: string): Promise<User> {
    return this.userService.getUser(id);
  }
}
```

### Преимущества такого подхода:

* **Изоляция бизнес-логики** от UI и инфраструктуры
* **Тестируемость
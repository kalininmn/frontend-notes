# Class <sup>ES6, 2015</sup>

Всегда `use strict`.

`constructor` класса является [функцией-конструктором](./FunctionConstructor.md):
```javascript
class User {
    constructor(name) {
        this.name = name;
    }; // function F(name) { this.name = name; }
}
```

#

Методы класса сохраняются в его `prototype`:
```javascript
class User {
    // counstructor() {} (неявно)
    sayHi() {
        alert('Hi!');
    }
}

// User.prototype == { consctuctor: User, sayHi }
```

#

`Геттеры` и `Сеттеры` класса сохраняются в его `prototype`:
```javascript
class User {
    constructor(name) {
        this.name = name;
    }
    
    get name() {
        return this._name;
    }
    
    set name(value) {
        if (value.length < 4) {
            alert('Имя слишком короткое');
            return;
        }
        this._name = value;
    }
}
```

#

При объявлении класса `геттеры` и&nbsp;`сеттеры` создаются на `User.prototype`:

```javascript
Object.defineProperties(User.prototype, {
    name: {
        get() {
            return this._name;
        },
        set(name) {
            ...
        }
    },
});
```

#

`геттеры` и&nbsp;`сеттеры` можно писать через методы.

Плюсы: 
- могут принимать несколько аргументов;
- являются безопаснее при рефакторинге.

Минусы: 
- методы длиннее, чем геттеры/сеттеры.

```js
// Это не геттер и сеттер — это метод!
class User {
    getName() {
        return this.name;
    }
    
    setName(value) {
        this.name = value;
    }
}

const user = new User();
user.setName('Maks');
```

#

Поля или свойства классов.

```javascript
class User {
    human = true; // object property
    
}
```

Свойство `human` не устанавливается в `User.prototype`.<br>
Оно создаётся оператором `new` перед запуском конструктора.

## Links

⬅️ [Back](./main.md)
[⇐ readme](../readme.md)

## Class
Классы, ecmascript 6 (2015).
<br>Всегда `use strict`.

---

`constructor` класса является функцией-конструктором:
```javascript
class User {
    constructor(name) {
        this.name = name;
    }; // function F(name) { this.name = name; }
}
```

<br>Методы класса сохраняются в его `prototype`:
```javascript
class User {
    // counstructor() {} (неявно)
    sayHi() {
        alert('Hi!');
    }
}

// User.prototype == { consctuctor: User, sayHi(), }
```

<br>`Геттеры`/`Сеттеры` класса сохраняются в его `prototype`:
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
При объявлении класса `геттеры`/`сеттеры` создаются на `User.prototype`:
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

<br>`геттеры`/`сеттеры` можно писать через методы.
<br>Плюсы: могут принимать несколько аргументов и являются безопаснее при рефакторинге.
<br>Минусы: методы длиннее, чем геттеры/сеттеры.
<br><span style="color: red;">Это не геттер/сеттер — это метод!</span>
```js
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

<br>Поля / свойства классов
```javascript
class User {
    human = true; // object property
    
}
```
Свойство `human` не устанавливается в `User.prototype`.<br>
Оно создаётся оператором `new` перед запуском конструктора.

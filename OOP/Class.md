[⇐ Function prototype](./FunctionPrototype.md)<br>
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

<br>Свойства классов
```javascript
class User {
    human = true; // object property
    
}
```
Свойство `human` не устанавливается в `User.prototype`.<br>
Оно создаётся оператором `new` перед запуском конструктора.

[next ⇒](./ClassExtends.md)
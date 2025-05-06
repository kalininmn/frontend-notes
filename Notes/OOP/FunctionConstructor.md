# Function constructor <sup>ES5, 2009</sup>

Функция конструктор.

```javascript
function F() {}
```

Именуется с большой буквы.<br>
Вызывается с оператором `new`.

#

`new` — вызов функции в режиме конструктора.

```javascript
function User(name) {
    this.name = name;
    this.isAdmin = false;
}

let user = new User('John');
```

#

Функция конструктор делает следующее:
1. Создаёт пустой объект `{}`;
2. Записывает его неявно в `this`;
3. Возвращает `this`.

```javascript
function User(name) {
    // this = {}; (неявно)
    this.name = name;
    this.isAdmin = false;
    // return this; (неявно)
}
```

## Links

⬅️ [Back](./main.md)
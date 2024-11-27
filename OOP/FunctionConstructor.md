[⇐ readme](../readme.md)

## Function constructor
Функция конструктор, ecmascript 5 (2009).

---
```javascript
function F() {}
```
1. Именуется с большой буквы
2. Вызывается с оператором `new`

<br>`new` — вызов функции в режиме конструктора.

```javascript
function User(name) {
    this.name = name;
    this.isAdmin = false;
}

let user = new User('John');
```

<br>Функция конструктор делает следующее:
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
[Next ⇒](./FunctionPrototype.md)

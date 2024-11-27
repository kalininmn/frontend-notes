[⇐ Function constructor](./FunctionConstructor.md)<br>
[⇐ readme](../readme.md)

## Function prototype
Свойство функции `prototype`, ecmascript 5 (2009).

---

Если `F.prototype` содержит объект, оператор `new` устанавливает его
в `[[prototype]]` для нового объекта:

```javascript
let animal = {};

function Rabbit() {}

Rabbit.prototype = animal;

let rabbit = new Rabbit(); // rabbit.__proto__ == animal
```

<br>По умолчанию каждая не стрелочная функция содержит свойство `prototype` — объект
с единственным свойством `constructor`, которое ссылается на функцию-конструктор:
```javascript
function Rabbit() {} // Rabbit.prototype = { constructor: Rabbit }

let rabbit = new Rabbit(); // rabbit.__proto__ == Rabbit.prototype
```

[next ⇒](./Class.md)
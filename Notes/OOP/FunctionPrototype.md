# Function prototype <sup>ES5, 2009</sup>

Свойство функции `prototype`.

Если `F.prototype` содержит объект, оператор `new` устанавливает его в&nbsp;`[[Prototype]]` для нового объекта:

```javascript
let animal = {};

function Rabbit() {}

Rabbit.prototype = animal;

let rabbit = new Rabbit(); // rabbit.__proto__ == animal
```

#

По умолчанию каждая не&nbsp;стрелочная функция содержит свойство `prototype` — объект с&nbsp;единственным свойством `constructor`, которое ссылается на функцию-конструктор:
```javascript
function Rabbit() {} // Rabbit.prototype = { constructor: Rabbit }

let rabbit = new Rabbit(); // rabbit.__proto__ == Rabbit.prototype
```

## Links

⬅️ [Back](./main.md)
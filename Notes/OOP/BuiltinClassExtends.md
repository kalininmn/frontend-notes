# Built-in Class Extends <sup>ES6, 2015</sup>

Наследование классов.<br>
ООП: наследование — расширение встроенных классов.

```js
class PowerArray extends Array {
  isEmpty() {
    return this.length === 0;
  }
}

const arr = new PowerArray(1, 2, 5, 10, 50);

const filteredArr = arr.filter((item) => item >= 10);

console.log(filteredArr); // 10, 50
console.log(filteredArr.isEmpty()); // false
```

#

Статический геттер `Symbol.species` возвращает конструктор,<br>
который JS будет использовать в `.filter`, `.map` и других методах<br>
для создания новых объектов.

```js
class PowerArray extends Array {
  isEmpty() {
    return this.length === 0;
  }

  // встроенные методы массива будут использовать этот метод как конструктор
  static get [Symbol.species]() {
    return Array;
  }
}

const arr = new PowerArray(1, 2, 5, 10, 50);
console.log(arr.isEmpty()); // false

// filter создаст новый массив, используя arr.constructor[Symbol.species] как конструктор
const filteredArr = arr.filter((item) => item >= 10);

// filteredArr не является PowerArray, это Array
console.log(filteredArr.isEmpty()); // Error: filteredArr.isEmpty is not a function
```

Аналогично работают другие коллекции: `Map`, `Set`, ...

#

**Важно**<br>
Встроенные классы не наследуют методы друг-друга.

```js
// Object
// Date

Object.__proto__ -> [native code]
Object.prototype -> { constructor: Object, ... }

Array.__proto__ -> [native code]
Array.prototype -> { constructor: Array, ... }
```

## Links

🏠 [Home](/readme.md)
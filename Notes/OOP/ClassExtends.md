# Class Extends <sup>ES6, 2015</sup>

Наследование классов.<br>
ООП: наследование — расширение родительских классов.


```js
class Animal {
    constructor(name) {
        this.name = name;
        this.speed = 0;
    }
    
    run(speed) {
        this.speed = speed;
        alert(`${this.name} бежит со скоростью ${this.speed}.`);
    }
    
    stop() {
        this.speed = 0;
        aler(`${this.name} стоит неподвижно.`)
    }
}
```

```javascript
Animal.prototype = {
    constructor: Animal,
    run: function,
    stop: function,
};
```

```javascript
const animal = new Animal('Мой питомец');

animal.prototype === undefined; // true
animal.__proto__ === Animal.prototype; // true
```

#

Наследование через `extends`.<br>
`Rabbit` может использовать методы и свойства `Animal`,<br>
так-как используется неявный конструктор родителя.

```js
class Rabbit extends Animal {
    // Используется неявный конструктор родителя 
    hide() {
        alert(`${this.name} прячется.`);
    }
}
```

```javascript
Rabbit.prototype = {
    constructor: Rabbit,
    hide: function,
};
Rabbit.prototype.__proto__ = { // === Animal.prototype
    run: function,
    stop: function,
};
```

```javascript
const rabbit = new Rabbit('Белый кролик');
rabbit.hide();

rabbit.prototype === undefined; // true
rabbit.__proto__ === Rabbit.prototype; // true
```

#

Переопределение конструктора.<br>
Конструктор потомка помечается свойством `[[ConstructorKind]]: 'derived'`,<br>
который требует вызова конструктора родительского класса через `super`.

```js
class Rabbit extends Animal {
    constructor(name, earLength) { // [[ConstructorKind]]: 'derived'
        super(name);
        this.earLength = earLength;
    }
}
```

#

Переопределение полей.

```js
class Animal {
    name = 'animal';
    
    constructor() {
        alert(this.name);
    }
}

class Rabbit extends Animal {
    name = 'rabbit'; // (*)
}

new Animal() // animal
new Rabbit // animal

```

<u>Родительский конструктор</u> всегда использует своё собственное значение поля, а&nbsp;не&nbsp;переопределённое.
<br>Причина заключается в порядке инициализации полей.<br>

Поля класса инициализируется:
1. Перед конструктором для базового класса (который ничего не расширяет),
2. Сразу после super() для производного класса.

#

Наследование под капотом.<br>
Используется внутрненнее свойство методов класса или объекта `[[HomeObject]]`, без использования `this`.

```js
let animal = {
    eat() {} // animal.eat.[[HomeObject]] == animal
};

let rabbit = {
    __proto__: animal,
    eat() { // rabbit.eat.[[HomeObject]] == rabbit
        super.eat();
    }
}
```

Методы запоминают свои объекты. Эта связь навсегда.<br>
Единственное место в языке, где используется `[[HomeObject]]` – это `super`. 

```js
let animal = {
  sayHi() {
    alert("Я животное");
  }
};

let rabbit = {
  __proto__: animal,
  sayHi() {
    super.sayHi();
  }
};

let plant = {
  sayHi() {
    alert("Я растение");
  }
};

let tree = {
  __proto__: plant,
  sayHi: rabbit.sayHi // (*)
};

tree.sayHi();  // Я животное
```

Поэтому, если метод не использует `super`,<br>
то мы все ещё можем считать его свободным и&nbsp;копировать между объектами.

Для объектов `[[HomeObject]]` определяется только внутри методов `method()`, а&nbsp;не&nbsp;`method: function()`.<br>
Несоблюдение этой специфики влечёт нерабочее наследование.

## Links

⬅️ [Back](./main.md)
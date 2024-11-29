[⇐ Class](./Class.md)<br>
[⇐ readme](../readme.md)

## Class extends
Наследование классов, ecmascript 6 (2015).

---

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

const animal = new Animal('Мой питомец');

// Animal.prototype = {
//     constructor: Animal,
//     run: function,
//     stop: function,
// };

// animal.prototype === undefined;
// animal.__proto__ === Animal.prototype;
```

<br>**Наследование через** `extends`.
<br>`Rabbit` может использовать методы и свойства `Animal`,
<br>так-как используется неявный конструктор родителя.
```js
// class Animal

class Rabbit extends Animal {
    // Используется неявный конструктор родителя 
    hide() {
        alert(`${this.name} прячется.`);
    }
}

const rabbit = new Rabbit('Белый кролик');
rabbit.hide();

// Rabbit.prototype = {
//     constructor: Rabbit,
//     hide: function,
// };
// Rabbit.prototype.__proto__ = { // === Animal.prototype
//     run: function,
//     stop: function,
// };

// rabbit.prototype === undefined;
// rabbit.__proto__ === Rabbit.prototype;
```
<br>**Переопределение конструктора**
<br>Конструктор потомка помечается свойством `[[ConstructorKind]]: 'derived'`,
<br>который требует вызова конструктора родительского класса через `super`.
```js
// ... Animal

class Rabbit extends Animal {
    constructor(name, earLength) { // [[ConstructorKind]]: 'derived'
        super(name);
        this.earLength = earLength;
    }
    
    // ...
}
```

<br>**Переопределение полей**
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
<u>Родительский конструктор</u> всегда использует своё собственное значение поля, 
а не переопределённое.
<br>Причина заключается в порядке инициализации полей. Поля класса инициализируется:
1. Перед конструктором для базового класса (который ничего не расширяет),
2. Сразу после super() для производного класса.

<br>**Наследование под капотом** 
<br>Используется внутрненнее свойство методов класса или объекта `[[HomeObject]]`, 
без использования `this`.
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

Методы запоминают свои объекты. Эта связь навсегда.
<br>Единственное место в языке, где используется `[[HomeObject]]` – это `super`. 
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

<br>Поэтому если метод не использует `super`, то мы все ещё можем считать его свободным 
<br>и копировать между объектами.

Для объектов `[[HomeObject]]` определяется только внутри методов `method()`, 
а не `method: function()`.
<br>Несоблюдение этой специфики влечёт нерабочее наследование.

[next ⇒](./StaticProperties.md)

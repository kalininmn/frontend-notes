[⇐ readme](../readme.md)

## Static properties
Статические свойства и методы

---

Это свойства и методы, которые присвоены самому классу и могут быть вызваны только через класс.

```js
class User {
    static staticMethod() {
        alert(this === User);
    }
}

// Тоже самое что и:
User.staticMethod = function() {
    alert(this === User);
}

User.staticMethod(); // true
```
Значением `this` при вызове `User.staticMethod()` является сам `User`.

<br>Статические методы используются для реализации функций, 
<br>которые будут принадлежать классу в целом, но не какому-либо его конкретному объекту.
```js
class Article {
  constructor(title, date) {
    this.title = title;
    this.date = date;
  }

  static compare(articleA, articleB) {
    return articleA.date - articleB.date;
  }
}

// использование
let articles = [
  new Article("HTML", new Date(2019, 1, 1)),
  new Article("CSS", new Date(2019, 0, 1)),
  new Article("JavaScript", new Date(2019, 11, 1))
];

articles.sort(Article.compare);
```
или
```js
class UserService {
    static async getUsers() {
        const response = await fetch('/users');
        return response.json();
    }
}

async function loadUsers() {
    const users = await UserService.getUsers();
    console.log(users);
}
```

<br><span style="color: green;">**Классный пример**</span>
```js
class Article {
  constructor(title, date) {
    this.title = title;
    this.date = date;
  }

  static createTodays() {
    // помним, что this = Article
    return new this("Сегодняшний дайджест", new Date());
  }
}

let article = Article.createTodays();

alert(article.title); // Сегодняшний дайджест
```

<br>**Статические свойства**
```js
class Article {
  static publisher = "KalininMN";
}

// Тоже самое что и:
Article.publisher = "KalininMN";
```

## Статические свойства и методы -- наследуются
```js
class Animal {
    static compare(animalA, animalB) {
        return animalA.speed - animalB.speed;
    }
}

class Rabbit extends Animal {}

const rabbits = [
    new Rabbit("Белый кролик", 10),
    new Rabbit("Чёрный кролик", 5),
];

rabbits.sort(Rabbit.compare);
```
`extends` даёт `Rabbit` ссылку `[[Prototype]]`на `Animal`.
```js
Rabbit.__proto__ == Animal; // true
```
`extends` даёт `Rabbit.prototype` ссылку `[[Prototype]]` на `Animal.prototype`.
```js
Rabbit.prototype.__proto__ == Animal.prototype; // true
```

<br>В результате:
```js
class Animal {}
class Rabbit extends Animal {}

// для статики
alert(Rabbit.__proto__ === Animal); // true

// для обычных методов
alert(Rabbit.prototype.__proto__ === Animal.prototype); // true
```

[⇐ readme](../readme.md)

## Public properties

Публичные поля, свойства и методы

---

**Свойства и методы класса**

```js
class Animal {
    cunstructor(name) {
        this.name = name;
        this.age = 0;
    }
    
    plusOneAge() {
        this.age += 1;
    }
    
    happyBirthday() {
        console.log('Yey!');
        this.plusOneAge();
    }
}

// Обращение как к статике
console.log(Animal.name); // Animal
console.log(Animal.plusOneAge()) // is not a function

// Обращение к экземпляру
const animal = new Animal('Teddy');

console.log(animal.name); // Teddy

animal.plusOneAge();
console.log(animal.age); // 1

animal.happyBirthday(); // Yey!
console.log(animal.age); // 2
```

**Поля класса**

```js
class Animal {
    name = 'Teddy';
}

const animal = new Animal();

console.log(Animal.name); // Animal
console.log(animal.name); // Teddy
```

```js
class Animal {
    name = 'Teddy';
}

class SupAnimal extends Animal {}

const supAnimal = new SupAnimal();

console.log(supAnimal.name); // Teddy
```

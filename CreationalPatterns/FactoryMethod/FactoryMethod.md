[⇐ readme](../readme.md)

## Factory method
Фабричный метод или виртуальный конструктор.
<br>[Порождающий шаблон проектирования](../Summary/CreationalPatterns.md), 
предоставляющий [подклассам](../OOP/ClassExtends.md) (дочерним классам) интерфейс для создания экземпляров некоторого класса. 
<br><br>В момент создания наследники могут определить, какой класс создавать. 
<br>Иными словами, данный шаблон делегирует создание объектов наследникам родительского класса. 
<br><br>Это позволяет использовать в коде программы не конкретные классы, 
<br>а манипулировать абстрактными объектами на более высоком уровне.

---

![](../imgs/i.webp)

**Product — продукт** 
<br>Определяет интерфейс объектов, создаваемых абстрактным методом.

**ConcreteProduct — конкретный продукт** 
<br>Реализует интерфейс `Product`.

**Creator — создатель**
<br>Объявляет фабричный метод, который возвращает объект типа `Product`. 
<br>Может также содержать реализацию этого метода «по умолчанию».
<br>Может вызывать фабричный метод для создания объекта типа `Product`.

**ConcreteCreator — конкретный создатель**
<br>Переопределяет фабричный метод таким образом, 
<br>чтобы он создавал и возвращал объект класса `ConcreteProduct`.

## Purpose

---

Определяет интерфейс для создания объекта, но оставляет подклассам решение о том, 
<br>на основании какого класса создавать объект. Фабричный метод позволяет классу 
<br>делегировать создание подклассов. 
<br><br>Используется, когда:
1. Классу заранее неизвестно, объекты каких подклассов ему нужно создавать;
2. Класс спроектирован так, чтобы объекты, которые он создаёт, специфицировались подклассами;
3. Класс делегирует свои обязанности одному из нескольких вспомогательных подклассов, 
и планируется локализовать знание о том, какой класс принимает эти обязанности на себя.

## Advantage

---

1. Позволяет сделать код создания объектов более универсальным, 
не привязываясь к конкретным классам (`ConcreteProduct`), 
а оперируя лишь общим интерфейсом (`Product`);
2. Позволяет установить связь между параллельными иерархиями классов.

---

<details>
<summary>Пример TS</summary>

```typescript
interface Product {
    GetName(): string
}

class ConcreteProductA implements Product {
    public GetName() {
        return 'ProductA'
    }
}

class ConcreteProductB implements Product {
    public GetName() {
        return 'ProductB'
    }
}

interface Creator {
    FactoryMethod(): Product
}

class ConcreteCreatorA implements Creator {
    public FactoryMethod() {
        return new ConcreteProductA()
    }
}

class ConcreteCreatorB implements Creator {
    public FactoryMethod() {
        return new ConcreteProductB()
    }
}

// An array of creators
const creators: Creator[] = [new ConcreteCreatorA(), new ConcreteCreatorB()];
const products: string[] = [];

// Iterate over creators and create products
creators.forEach((creator) => products.push(creator.FactoryMethod().GetName()));
```
</details>

<details>
<summary>Пример ES6</summary>

```javascript
class Product {
    GetName() {}
}

class ConcreteProductA extends Product {
    GetName() {
        return 'ProductA';
    }
}

class ConcreteProductB extends Product {
    GetName() {
        return 'ProductB';
    }
}

class Creator {
    FactoryMethod() {}
}

class ConcreteCreatorA extends Creator {
    FactoryMethod() {
        return new ConcreteProductA()
    }
}

class ConcreteCreatorB extends Creator {
    FactoryMethod() {
        return new ConcreteProductB()
    }
}

// An array of creators
const creators: Creator[] = [new ConcreteCreatorA(), new ConcreteCreatorB()];
const products: string[] = [];

// Iterate over creators and create products
creators.forEach((creator) => products.push(creator.FactoryMethod().GetName()));
```
</details>

<details>
<summary>Пример ES5 (без наследования)</summary>

```javascript
function NewConcreteCreatorA() {
  return {
      factoryMethod() {
          return {
              getName() {
                  return "ConcreteProductA";
              },
          };
      },
  };
};
function NewConcreteCreatorB() {
    return {
        factoryMethod() {
            return {
                getName() {
                    return "ConcreteProductB";
                },
            };
        },
    };
};

// An array of creators
var creators = [NewConcreteCreatorA(), NewConcreteCreatorB()];
var products = [];

// Iterate over creators and create products
creators.forEach((creator) => products.push(creator.FactoryMethod().GetName()));
```
</details>
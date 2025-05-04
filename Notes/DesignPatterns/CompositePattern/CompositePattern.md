[⇐ readme](../readme.md)

## Composite pattern
Компоновщик.

Паттерн определяет иерархию классов, 
которые одновременно могут состоять из примитивных и сложных объектов.<br>
Позволяет обращаться к отдельным объектам и группам объектов одинаково.<br>

---

↓ Делает процесс добавления новых видов объекта более простым ↓

<details>
<summary>Пример ES6</summary>

```javascript
class Component {
    constructor(name, value) {
        this.name = name;
        this.value = value;
    }
    execute() {}
}

class Leaf extends Component {
    execute() {
        return this.value;
    }
}

class Composite extends Component {
    constructor(name, value) {
        super(name, value);
        this.children = [];
    }

    add(component) {
        this.children.push(component);
    }
    remove(componentName) {
        this.children = this.children.filter((x) => x.name !== componentName);
    }
    execute() {
        this.children.forEach((x) => {
            this.value = (this.value || 0) + x.execute();
        });
        return this.value;
    }
}

const kitchen = new Composite('Кухня');

kitchen.add(new Leaf('Верхняя секция', 5200));
kitchen.add(new Leaf('Верхняя двойная секция', 10000));
kitchen.add(new Leaf('Нижняя секция', 4500) );
kitchen.add(new Leaf('Нижняя угловая секция', 7800) );

const equipment = new Composite('Техника');

equipment.add(new Leaf('Газовая плита', 26400));
equipment.add(new Leaf('Холодильник', 32300));
equipment.add(new Leaf('Посудомойка', 21600));

kitchen.add(equipment);
```
</details>

<details>
<summary>Пример ES5</summary>

```javascript
function Component() {
    this.name = '';
    this.value = 0;
    this.execute = function () { };
}

function Leaf(name, value) {
    this.name = name;
    this.value = value;

    this.execute = function () {
        return this.value;
    };
}

Leaf.prototype = Object.create(Component.prototype);
Leaf.prototype.constructor = Leaf;

function Composite(name) {
    var self = this;
    var children = [];

    this.name = name;

    this.add = function (component) {
        children.push(component);
    };

    this.remove = function (componentName) {
        var newChildren = [];
        children.forEach(function (component) {
            if (component.name !== componentName) {
                newChildren.push(component);
            }
        });
        children = newChildren;
    };

    this.execute = function () {
        children.forEach(function (component) {
            self.value = (self.value || 0) + component.execute();
        });

        return self.value;
    };
}

Composite.prototype = Object.create(Component.prototype);
Composite.prototype.constructor = Composite;

var kitchen = new Composite('Кухня');

kitchen.add(new Leaf('Верхняя секция', 5200));
kitchen.add(new Leaf('Верхняя двойная секция', 10000));
kitchen.add(new Leaf('Нижняя секция', 4500));
kitchen.add(new Leaf('Нижняя угловая секция', 7800));

var equipment = new Composite('Техника');

equipment.add(new Leaf('Газовая плита', 26400));
equipment.add(new Leaf('Холодильник', 32300));
equipment.add(new Leaf('Посудомойка', 21600));

kitchen.add(equipment);
```
</details>
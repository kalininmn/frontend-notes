## Принципы объектно-ориентированного проектирования SOLID

<details>
<summary>
Single responsibility principle (принцип единственной ответственности)
</summary>

<br>
Принцип заключается в описании `класс`а, который `ответственнен только за что-то одно`.

Принцип лучше реализуется через `описание моделей` и `TDD`.

Есть возможность отрефакторить код (через паттерны), чтобы прийти к SRP.
<br><br>
</details>

<details>
<summary>
Open-closed principle (принцип открытости-закрытости)
</summary>

<br>
Пишем интерфейс и реализацию, хотябы частично покрывающую интерфейс,<br> 
где класс открыт к расширению, но закрыт к модификациям.
Реализации интерфейсов могут быть заменены полиморфным путём.
<br><br>
</details>

<details>
<summary>
Liskov substitutions principle (принцип подстановки Лисков)
</summary>

<br>
Функции, которые используют базовый тип, должны иметь возможность использовать подтипы базового типа не зная об этом.
<br><br>

**Формула**<br>
Свойство `q(x)`, где свойство удовлетворяет нескольким `x` типа `T`.<br>
Свойство `q(y)`, где свойство удовлетворяет нескольким `y` типа `S`.<br>
Свойство `q(y)` соответствует свойству `q(x)`, так-как тип `S` является наследником типа `T`.
<br><br>
</details>
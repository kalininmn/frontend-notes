[⇐ Private properties](./PrivateProperties.md)<br>
[⇐ readme](../readme.md)

## Protected properties

Защищённые свойства
<br>ООП: инкапсуляция — отделение внутреннего интерфейса от внешнего.

---
Такие свойства и методы не должны быть доступны извне.

В JS нет защищённых свойств, например как в Java.
<br>Но есть согласованность между разработчиками 
<br>именовать такие свойства с нижним подчеркиванием `_`.

```js
class CoffeMachine {
    _waterAmount = 0;
}
```

Делаем `_waterAmount` защищённым.
```js
class CoffeeMachine {
  _waterAmount = 0;

  set waterAmount(value) {
    if (value < 0) throw new Error("Отрицательное количество воды");
    this._waterAmount = value;
  }

  get waterAmount() {
    return this._waterAmount;
  }

  constructor(power) {
    this._power = power;
  }

}
```

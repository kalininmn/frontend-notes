[⇐ readme](../readme.md)

## Interface
Интерфейс

**You should prefer** `interface`

---

Describe object's shape using an `interface` declaration
```ts
interface User {
    name: string;
    id: number;
}
```

Declare a JavaScript object conforms to the shape of your new `interface`
```ts
const user: User = {
    name: 'Hayes',
    id: 0,
}
```

If you provide an object that doesn’t match the interface you have provided, TS will warn you
```ts
const user: User = {
    username: 'Hayes', // Object literal may only specify known properties, and 'username' does not exist in type 'User'.
    id: 0,
}
```

Support classes and object-oriented programming
```ts
class UserAccount {
  name: string; // object property...
  id: number;
 
  constructor(name: string, id: number) {
    this.name = name;
    this.id = id;
  }
}


const user: User = new UserAccount("Murphy", 1);
```

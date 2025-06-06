[⇐ readme](../readme.md)

## Never type
Тип никогда

---

```ts
// Because TypeScript supports code flow analysis, the language
// needs to be able to represent when code logically cannot
// happen. For example, this function cannot return:

const neverReturns = () => {
  // If it throws on the first line
  throw new Error("Always throws, never returns");
};

// If you hover on the type, you see it is a () => never
// which means it should never happen. These can still be
// passed around like other values:

const myValue = neverReturns();

// Having a function never return can be useful when dealing
// with the unpredictability of the JavaScript runtime and
// API consumers that might not be using types:

const validateUser = (user: User) => {
  if (user) {
    return user.name !== "NaN";
  }

  // According to the type system, this code path can never
  // happen, which matches the return type of neverReturns.

  return neverReturns();
};

// The type definitions state that a user has to be passed in
// but there are enough escape valves in JavaScript whereby
// you can't guarantee that.

// Using a function which returns never allows you to add
// additional code in places which should not be possible.
// This is useful for presenting better error messages,
// or closing resources like files or loops.

// A very popular use for never, is to ensure that a
// switch is exhaustive. E.g., that every path is covered.

// Here's an enum and an exhaustive switch, try adding
// a new option to the enum (maybe Tulip?)

enum Flower {
  Rose,
  Rhododendron,
  Violet,
  Daisy,
}

const flowerLatinName = (flower: Flower) => {
  switch (flower) {
    case Flower.Rose:
      return "Rosa rubiginosa";
    case Flower.Rhododendron:
      return "Rhododendron ferrugineum";
    case Flower.Violet:
      return "Viola reichenbachiana";
    case Flower.Daisy:
      return "Bellis perennis";

    default:
      const _exhaustiveCheck: never = flower;
      return _exhaustiveCheck;
  }
};

// You will get a compiler error saying that your new
// flower type cannot be converted into never.

// Never in Unions

// A never is something which is automatically removed from
// a type union.

type NeverIsRemoved = string | never | number;

// If you look at the type for NeverIsRemoved, you see that
// it is string | number. This is because it should never
// happen at runtime because you cannot assign to it.

// This feature is used a lot in example:conditional-types

```

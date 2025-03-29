Всього існує два додаткових модифікатори для mapping types:
- `readonly` - чи можна мутувати поле
- `?` - обов'язковість поля

Щоб додати або видалити ці модифікатори треба використовувати префікси `+` та `-`. Якщо префікс не вказано `+` використовується за замовчуванням

Наприклад, тип `CreateMutable` який видаляє readonly зі всіх полів:

```ts
type CreateMutable<T> = {
  -readonly [P in keyof T]: T[P];
};
 
type LockedAccount = {
  readonly id: string;
  readonly name: string;
};
 
type UnlockedAccount = CreateMutable<LockedAccount>;
// ^ type UnlockedAccount = {
//     id: string;
//     name: string;
//   }
```

Або ж тип `Concrete` який видаляє optional зі всіх полів:


```ts
type Concrete<Type> = {
  [Property in keyof Type]-?: Type[Property];
};
 
type MaybeUser = {
  id: string;
  name?: string;
  age?: number;
};
 
type User = Concrete<MaybeUser>;
// ^ type User = {
//     id: string;
//     name: string;
//     age: number;
//   }
```

Іноді буває ситуація, коли ми хочемо, наприклад, відфільтрувати деякі ключі з об'єкта, або ж дописати до кожного ключа якийсь префікс, або ж якось по іншому змінити деякі ключі

Для цього в Mapping types ми можемо використовувати `as`

```ts
type MappedTypeWithNewProperties<T> = {
    [P in keyof T as NewKeyType]: T[P]
}
```

Наприклад, використовуючи [[Template Literal Types]] ми можемо до кожного ключа дописати якийсь префікс:

```ts
type Getters<T> = {
    [P in keyof T as `get\${Capitalize<string $ P>}`]: () => T[P]
};
 
interface Person {
    name: string;
    age: number;
    location: string;
}
 
type LazyPerson = Getters<Person>;
// ^ type LazyPerson = {
//     getName: () => string;
//     getAge: () => number;
//     getLocation: () => string;
//   }
```

Або ж, наприклад, ми хочемо прибрати якийсь ключ з об'єкта взагалі (аналог [[Omit<T, K>]]):

```ts
// Remove the 'kind' property
type RemoveKindField<T> = {
    [P in keyof Type as Exclude<P, "kind">]: T[P]
};
 
interface Circle {
    kind: "circle";
    radius: number;
}
 
type KindlessCircle = RemoveKindField<Circle>;
// ^ type KindlessCircle = {
//    radius: number;
// }
```

Оригінальний код Omit:

```ts
type Omit<T, K extends keyof any> = { 
	[P in Exclude<keyof T, K>]: T[P];
}
```

Також ми можемо проходитись не по примітивним типам, таким як number, string тощо, а по [[Union]]:

```ts
type EventConfig<Events extends { kind: string }> = {
    [E in Events as E["kind"]]: (event: E) => void;
}
 
type SquareEvent = { kind: "square", x: number, y: number };
type CircleEvent = { kind: "circle", radius: number };
 
type Config = EventConfig<SquareEvent | CircleEvent>
// ^ type Config = {
//       square: (event: SquareEvent) => void;
//       circle: (event: CircleEvent) => void;
//   }
```

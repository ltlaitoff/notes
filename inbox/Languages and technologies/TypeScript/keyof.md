`keyof` в [[TypeScript]] приймає [[TypeScript Object|Object]] та повертає [[Union]] всіх його ключів

Наприклад:

```ts
type Point = { x: number, y: number }
type PointKeys = keyof Point
// ^ type PointKeys = 'x' | 'y'
```

І тепер ми можемо, наприклад, створити змінну з типом `PointKeys` та ми можемо бути впевненими, що значення цієї змінної точно відповідає одному з ключів `Point`

```ts
const key: PointKey = 'x' // ok
const key2: PointKey = 'a' // error
```

Якщо ж тип об'єкта не має чітких ключів, а має тільки їх тип, то `keyof` поверне цей тип:

```ts
type Arrayish = { [n: number]: unknown }
type ArrayishKey = keyof Arrayish
// ^ type ArrayishKey = number

type Mapish = { [n: string]: boolean }
type MapishKey = keyof Mapish
// ^ type MapishKey = string | number
```

Важливо зазначити, що `keyof` при `Mapish` повернув `string | number`, оскільки [[Ключі в JavaScript автоматично приводяться до рядків]]

Тобто `arr[0]` та `arr["0"]` це одне і те саме

keyof часто використовують в [[Mapped types]]

// TODO: Add `T[number]` для взяття всіх значень

Документація про keyof - https://www.typescriptlang.org/docs/handbook/2/keyof-types.html
**Mapped types** - це типи в [[TypeScript]], які створюються шляхом ітерації по властивостях іншого типу(зазвичай об'єкта) для створення нового типу, де кожна властивість може бути перетворена або модифікована

Mapped types використовують [[Index Signatures]], який виглядає ось так:

```ts
type OnlyBoolsAndHorses = {
  [key: string]: boolean | Horse
}
```

Mapped type це [[Generic]] тип, який використовує [[Union]] `PropertyKey`'s (який часто створюється через [[keyof]]), для ітерації через ключі з метою створення нового типу:

```ts
type OptionsFlags<T> = {
  [P in keyof T]: boolean
}
```

Наприклад, це код ітерується по ключах деякого об'єкта та для кожного ключа ставиться значення в `boolean`

```ts
type Features = {
  darkMode: () => void
  newUserProfile: () => void
}

type FeatureOptions = OptionsFlags<Features>
// type FeatureOptions = {
//    darkMode: boolean;
//    newUserProfile: boolean;
// }
```

За допомогою mapped types можна створити свій [[Record<Keys, Type>]]:

```ts
type Record<K extends string | number, T> = {
	[_ in K]: T
}
```

Головна сила Mapping types полягає в їх використанні разом з іншими структурами TypeScript, наприклад разом з [[Умовні типи|умовними типами]] ми можемо створювати багато чого цікавого

За допомогою [[Mapping types модифікатори]] та [[Зміна ключів через "as" в mapping types]], а ще й використання інших структур ми можемо зробити майже що завгодно!

Як приклад, ми можемо створити тип, який буде ставити readonly тільки для деяких ключів:

```ts
type MyReadonly2<T, K extends keyof T = keyof T> = {
  readonly [key in keyof T as key extends K ? key : never]: T[key];
} & {
    [key in keyof T as key extends K ? never : key]: T[key];
  }
```

Або ж створити свій `Pick`:

```ts
type MyPick<T, K extends keyof T> = { [P in K]: T[P] }
```
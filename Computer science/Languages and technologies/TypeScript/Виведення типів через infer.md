**infer** - це ключове слово в TypeScript яке дозволяє нам виводити типи окремих елементів всередині Умовних типів

Представимо ситуацію, що ми хочемо написати тип, який буде повертати тип значення, яке повертає деяка функція

```ts
type ReturnType<T extends (...args: any) => any> = ...
```

Щоб це зробити ми можемо... Ну... Якось магічно взяти тип значення яке повертає фукнція

Проблему видно відразу - не зрозуміло ЯК це дістати!

Або ось ще приклад! Припустимо, що ми хочемо взяти останній елемент масиву:

```ts
type Last<T extends readonly unknown[]> = ...
```

Щоб нам це зробити ми можемо спробувати знаходити довжину масиву(що не так просто ) і потім віднімати від неї 1 та брати тип... Спойлер: У мене це не працювало, див [15](https://github.com/ltlaitoff/study/blob/main/typescript/tasks/15-last-of-array.ts))

Проблему видно і проблема досить глибока. Якщо нам складно зробити такі базові операції, що ж буде на складних?

Тому, на такі випадки в TypeScript існує `infer`

Фактично, через `infer` ми можемо всередині умовного типу отримати якийсь окремий елемент!

Наприклад, `ReturnType`:

```ts
type ReturnType<T> = T extends (...args: any) => infer R ? R : never
```

Тобто, порівнюючи типи через `extends` ми в другому типі пишемо `infer` і через нього можемо отримати доступ до якогось окремого типу!

Або ж ось `Last`:

```ts
type Last<T extends readonly unknown[]> = T extends [...any, infer Item]
	? Item
	: never
```

Також це працює з [[Template Literal Types]]:

```ts
type A = TrimLeft<'  str'>
// ^ type A = 'str'
type B = TrimLeft<' \n str'>
// ^ type B = 'str'
type C = TrimLeft<'     str     '>
// ^ type C = 'str     '

type Divider = ' ' | '\n' | '\t'

type TrimLeft<S extends string> = S extends `${Divider}${infer Item}`
	? TrimLeft<Item>
	: S
```
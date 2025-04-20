`typeof` це оператор [[TypeScript]] який повертає тип деякого [[JavaScript]] виразу

В самому [[JavaScript]] вже є [[typeof]], але він повертає тип, який потім можна використовувати в самому JavaScript, в його виразах та коді

```javascript
const a = 'Hello world!'
console.log(typeof a) // "string"
```

В TypeScript `typeof` це оператор, який можна використовувати, щоб отримати тип, з яким потім можна робити маніпуляції

```typescript
const a = 'Hello world!'
type A = typeof a
// ^ type A = string
```

Тобто, і те, і те бере тип, але вони роблять це по різному та для різних цілей

Використовувати `typeof` для примітивних типів це не дуже цікаво. Набагато цікавіше коли ми починаємо його використовувати для складніших структур

Наприклад, використовуючи `typeof` ми можемо отримати тип функції JavaScript:

```typescript
const mul2 = (a: number) => {
	return a * 2
}

type Mul2 = typeof mul2
// type Mul2 = (a: number) => number
```

Звичайно ми можемо спочатку зробити тип для функції, а потім оголосити JavaScript функцію по цьому типу

```typescript
type Mul2 = (a: number) => number

const mul2: Mul2 = (a: number) => {
	return a * 2
}
```

Але такий підхід не дуже зручний, бо нам приходиться писати забагато не дуже потрібного коду

Після того як ми взяти тип через `typeof` ми можемо проводити над ним різні маніпуляції

Наприклад, ми можемо з типу функції вивести тип значення, яке вона повертає!

```typescript
const mul2 = (a: number) => {
	return a * 2
}

type Mul2Return = ReturnType<typeof mul2>
```

Або ж взяти типи аргументів. Або ж якось змінити типи аргументів/значення яке повертається

Або ж ми можемо через [[keyof]] взяти всі ключі створеного об'єкта!

```typescript
const foo = {
	a: 1,
	b: true,
	c: "test"
}

type FooKeys = keyof typeof foo
// type FooKeys = 'a' | 'b' | 'c'
```

Наша фантазія безмежна!

### typeof з масивами

Коли у нас є якийсь масив

```typescript
const foo = ['a', 'b', 1]
```

`typeof` поверне нам `(string | number)[]`, що насправді логічно

Масиви в JavaScript не є статичними, ми можемо в них додавати значення

Якщо ж ми хочемо створити точну копію цього масиву з такими самими значеннями ми можемо використати `as const`

```typescript
const foo = ['a', 'b', 1]

type Foo = typeof foo
// ^ type Foo = (string | number)[]

const bar = ['a', 'b', 1] as const;

type Bar = typeof bar
// ^ type Bar = ['a', 'b', 1]
```

---

Документація - https://www.typescriptlang.org/docs/handbook/2/typeof-types.html
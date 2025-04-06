**Union** - це тип в [[TypeScript]] який є комбінацією з двох або більше інших типів

Кожен окремий тип в Union називається **Union member** 

**Union** представляє значення, яке може бути будь-яким із цих типів

> [!hint]
> Ми можемо думати про Union як про `OR`, або ж `АБО`
> 
> Тобто, або перший тип, або другий тип, або ...

Синтаксис Union являє собою перелічення типів через `|`:

```typescript
type U = string | number | boolean

const a: U = 's'
const b: U = 1
const c: U = false
```

Зазвичай Union використовуються для вказання аргументів функцій:

```typescript
function foo(a: number | boolean) {
	return a
}

foo(1) // ok
foo(false) // ok
foo('str') // error
```

Тобто, оскільки ми вказали, що аргумент `a` може бути `number | boolean` тепер ми не можемо передати туди щось інше

> [!info]
> 
> Також ми можемо записувати перед першим Union member `|` щоб красиво відформатувати типи
> 
> ```typescript
> function printTextOrNumberOrBool(
>  textOrNumberOrBool:
>     | string
>     | number
>     | boolean
> ) {
>   console.log(textOrNumberOrBool);
> }
> ```

За замовчуванням TypeScript надає нам можливість виконувати операції, які дозволені для всіх елементів Union

Наприклад, якщо у нас є Union `string | number`, то ми не можемо на нього викликати метод `.toUpperCase`, оскільки він є тільки у рядків

```ts
function someFunction(arg: string | number) {
	return arg.toUpperCase()
	// ^ Error
}
```

Щоб викликати метод нам треба точно знати, що аргумент це рядок

Для цього ми можемо написати перевірку, таку саму, як і в звичайному JavaScript, яка буде перевіряти тип, і якщо він рядок, то виконувати потрібну операцію. В TypeScript це називається [[Narrowing]]

```ts
function someFunction(arg: string | number) {
	if (typeof arg === 'string') {
		// arg: string
		return arg.toUpperCase()
	}
	
	// arg: number
	return arg
}
```

Також для цього ми можемо використовувати інші перевірки, такі як `Array.isArray`, або ж навіть написати свої власні через [[User-defined type guard]]

> [!faq]
> It might be confusing that a _union_ of types appears to have the _intersection_ of those types’ properties
> 
> This is not an accident - the name _union_ comes from [[Type theory]]
> 
> The _union_ `number | string` is composed by taking the union _of the values_ from each type
> 
> Notice that given two sets with corresponding facts about each set, only the _intersection_ of those facts applies to the _union_ of the sets themselves
> 
> For example, if we had a room of tall people wearing hats, and another room of Spanish speakers wearing hats, after combining those rooms, the only thing we know about _every_ person is that they must be wearing a hat


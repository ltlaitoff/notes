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


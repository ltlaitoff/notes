**Literal типи** - це коли ми в типах точно використовуємо конкретний рядок або число

Це відбувається через те, як [[JavaScript]] працює зі змінними. У нас є [[let]] та [[var]], при оголошенні змінної в них ми можемо потім змінювати її значення. А також є [[const]], в якому ми не можемо змінювати значення

```ts
var a = 'a'
let b = 'b'
const c = 'cat'

a = 'a1' // correct
b = 'b1' // correct
c = 'cat1' // error
```

Тому у випадку з `c` ми можемо точно сказати, що там завжди буде рядок `"cat"` і він ніколи не зміниться. Саме це і робить TypeScript! І це називається **Literal types**

```ts
var a = 'a' // type a = string
let b = 'b' // type b = string
const c = 'cat' // type c = 'cat'
```

Самі по собі вони не дуже цінні, ми не можемо багато зробити зі змінною, яка має тільки одне значення

Але комбінуючи літерали в [[Union]] ми можемо зробити вже багато потрібних речей. Наприклад, ми можемо сказати, що фукнція буде приймати тільки деякий набір рядків:

```ts
function printText(s: string, alignment: "left" | "right" | "center") {
  // ...
}

printText("Hello, world", "left"); // ok
printText("G'day, mate", "centre"); // error
```

Те саме можна зробити і з числами:

```ts
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}
```

І звичайно ми можемо об'єднувати літерали та інші типи в Union

```ts
function configure(x: Options | "auto") {
  // ...
}
```

> [!info] Boolean
> 
> Існують ще також Boolean літерали, які мають два значення: `true` або `false`
> 
> Детальніше - [[Boolean це аліас для Union true or false]]




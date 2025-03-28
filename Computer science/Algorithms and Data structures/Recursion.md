**Recursion**, або ж **Рекурсія** - виклик [[Підпрограма|підпрограми]], тобто [[Функція|фукнції]] або [[Процедура|процедури]], з неї самої, або ж іншої підпрограми

У нас є якась функція і ця функція викликає саму себе при деяких обставинах і, звичайно, з іншими аргументами

**Навіщо це потрібно?** Таким чином ми можемо зробити багато алгоритмів простішими для розуміння іншими розробниками

Рекурсія складається з двох **Базового кейсу** та **Рекурсивного кейсу**

**Базовий кейс** - це умова, при якій завершується рекурсія

Якщо його не додати - рекурсія буде нескінченою

**Рекурсивний кейс** - це умова виклику рекурсії

Без рекурсивного кейсу не буде рекурсії

### Приклад рекурсії на факторіалах

Наприклад, візьмемо [[Факторіал]]

Факторіал $10! = 10 * 9 * 8 * ... * 1$. Тобто $10! = 10 * 9!$

Припустимо, ми хочемо створити функцію, яка буде його вираховувати

Для цього ми можемо написати функцію, яка буде приймати число, і віддавати результат

Також, оскільки $10! = 10 * 9!$, ми можемо всередині цієї функції викликати цю саму функцію, але з числом на одиницю менше!

```typescript
function fact(number: number) {
	return number * fact(number - 1)
}
```

І тепер, що буде коли ми передаємо 10:

```
fact(10) = 10 * fact(9)
fact(9) = 9 * fact(8)
...
fact(1) = 1 * fact(0)
fact(0) = 0 * fact(-1)
...
fact(-10) = -10 * fact(-11)
```

Як можна побачити, все, що йде до одиниці відповідає формулі факторіала!

**Але така фукнція уходить в мінус, а також є нескінченою**

Щоб такого не було нам треба додати **Базовий кейс**

У випадку факторіалів це 1 та 0, або тільки 0

```typescript
function fact(number: number) {
	if (number === 0 || number === 1) {
		return 1
	}
	
	return number * fact(number - 1)
}
```

Цей приклад є дуже простим. Тут можна додати кешування, купу перевірок та тестів і тоді це буде більш схоже на щось реальне, але це гарно пояснює ідею


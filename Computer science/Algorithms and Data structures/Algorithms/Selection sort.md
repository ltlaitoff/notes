**Selection sort**, а сортування вибіркою - це алгоритм сортування, при якому ми створюємо новий масив та переносимо елементи по одному в правильному порядку

Наприклад, у нас є масив `a`

```c
[5, 8, 1, 2, 32, 6, 9]
```

І ми хочемо його відсортувати

Для цього ми створюємо новий пустий масив `b`. Проходимось по `a`, знаходимо найбільший елемент та додаємо його до `b`

```c
[32]
[5, 8, 1, 2, 6, 9]

[32, 9]
[5, 8, 1, 2, 6]

...

[32, 9, 9, 6, 5, 2, 1]
[]
```

І таким чином ми отримуємо новий відсортований масив!

Цей алгоритм займає [[O(n^2)]]

Один прохід по масиву `a` це n операцій. А ми проходимось по масиву `a` також n / 2 разів

Тобто складність буде `n * n / 2`, але оскільки [[В Big O відкидують числа]], то  складність виходить [[O(n^2)]]

### Реалізація selection sort

Для того, щоб реалізувати selection sort нам потрібна функція, яка знаходить максимальне(або мінімальне, якщо треба) число:

```ts
function findSmallest(nums: number[]) {
	let smallestIndex = Math.infinity

	for (let i = 0; i <= nums.length; i++) {
		if (nums[smallestIndex] > nums[i]) {
			smallestIndex = i
		}
	}

	return smallestIndex
}
```

І тепер ми можемо написати сам selection sort

```ts
function selectionSort(nums: number[]) {
	const result = []
	
	for (let num in nums) {
		const smallestIndex = findSmallest(nums)
		result.push(nums[smallestIndex])
		delete smallestIndex[smallestIndex]
	}
}
```
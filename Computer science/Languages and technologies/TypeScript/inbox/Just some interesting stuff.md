// It means typescript can transform number and big number to string

```ts
type Absolute<T extends number | string | bigint> =
	`${T}` extends `-${infer Item}` ? Item : `${T}`
```
---
aliases:
  - JWT
---
**Json Web Token**, або **JWT** - це відкритий стандарт([RFC 7591](https://datatracker.ietf.org/doc/html/rfc7519)) який визначає компактний та самодостатній шлях для безпечної передачі інформації між сторонами в JSON форматі

**JWT** читаються як `джот` ;0 

Ми можемо довіряти інформації, яка зберігається у **JWT**, а також ми можемо її перевіряти, оскільки кожен токен має [[Digital signature|Цифровий підпис]]

**JWT** токени можуть бути підписані або за допомогою секретного ключа, з [[HMAC]] алгоритмом, або, як зазвичай роблять, використовуючи [[Public and private key pair]] з [[RSA]] або [[ECDSA]]

**JWT** фокусуються саме на підписаних токенах. Звичайно ми можемо їх закодувати та передавати кудись, але для цього краще використовувати щось інше

Якщо **JWT** токен був підписаний використовуючи [[Public and private key pair]], то ми можемо бути точно впевнені, що тільки той, хто зберігає **private** ключ підписав цей токен. А перевірити ми це можемо тільки використовуючи **public**

**Private** - це ключ який потрібно дуже гарно зберігати, оскільки інакше від вашого імені можна буде випускати токени
**Public** - можна буквально(наприклад, [public ключі github](https://github.com/xanf.keys)) зберігати в public. Хоч на заборі його написати. Він потрібен тільки для перевірки підпису. 

>[!danger] JWT не підходять для конфіденційної інформації
> Щоб прочитати інформацію у **JWT** нам навіть не потрібно мати ключі
> 
> Тому JWT зовсім не підходить для секретної інформації!

Зазвичай JWT використовують для авторизації - [[Auth через JWT]]

## Структура JWT

JWT токен являє собою строку, яка складається з трьох елементів розділених точками

- `Header`
- `Payload`
- `Signature`

Звичайний JWT токен виглядає ось так:

```
xxxxx.yyyyy.zzzzz
```

Header та payload закодовані в Base64URL, а сигнатура не потребує кодування

> [!warning]
> 
> При збільшенні кількості контенту наш токен буде збільшуватись відповідно
> 
> Це потрібно враховувати, щоб не вийти за ліміти при їх використанні

### Header

Header токена зазвичай складається з типу токена, тобто "JWT", та алгоритму, яким він був підписаний

Наприклад:

```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### Payload

Це основна частина токена в яку ми можемо записувати контент, який ми хочемо передати

Ця частина має три види записів

**Зареєстровані**

Вони не є обов'язковими, але рекомендуються до використання 

Найбільш поширені:
- `exp` - Expiration time
- `sub` - Subject
- `iss` - Issuer
- `aud` - Audience

Список всіх зареєстрованих - [Registered Claim Names](https://datatracker.ietf.org/doc/html/rfc7519#section-4.1)

**Публічні**

Це список загально використовуваних означень - [JSON Web Token Claims](https://www.iana.org/assignments/jwt/jwt.xhtml)

Вони використовуються, щоб різні компанії та різні сервіси мали деяку стандартизацію, а не робили все так, як захочуть

Ці назви не є обов'язковими, але їх бажано використовувати

**Приватні**

Це наші унікальні назви які ми передаємо тільки між серверами, з якими це узгоджено

Тут може бути будь-що

### Signature

Це [[Digital signature|Цифровий підпис]] токена

Різні алгоритми працюють по різному, але підпис завжди прив'язаний до даних

Тобто, якщо ми в фінальному токені спробуємо щось змінити у нас буде не валідна сигнатура

---
## Reference

"Introduction to JSON Web Tokens" з jwt.io: https://jwt.io/introduction

"Сесії проти JWT #1: Що обрати?" від [[JavaScript Січ]]: https://youtu.be/Zk9drnLo590?t=1074

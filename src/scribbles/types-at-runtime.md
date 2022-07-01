# Distinguish types at runtime

Often, using the typescript, you have to handle situations when you don't know the type 
beforehand, during the compilation time. It hardly could be taken as a big problem and there are usually two or three types to choose from. But anyway, due the frequency of the situation, it is totally ok to looking for robust and concise solution.

Let's look on a case with an REST endpoint that may return an error instead of a data.

The simplest solution is to make all the properties of the data optional.

```typescript
interface Response {
    price?: number;
    errorText?: string;
}

// no properties are fine for compiler, but not for us
let empty: Response = {};

// object with price and errorText at the same time is invalid, but not for compiler if all the proerties marked optional
let allTogether: Response = {
  price: 100,
  errorText: 'Price is not available'
}; 
```

We have to do better than that. For that we could try the discriminated unions. They allow to enumerate the set of possible types.

```typescript
interface TileInfo {
    price: string;
}

interface TileError {
    errorText: string;
}

type TileData = TileInfo | TileError;
```

Such a construct later may be used together with the `in` operator as a type guard.

```typescript
if ('price' in data) {
    showPrice(data);
} else {
    showError(data);
}
```

This will work exactly as expected. The only "flaw" of the approach is that you have to use a string literal as name of a property. It doesn't work with the variables or enums.

Because of this, a typecasting is another method to prompt a type.

```typescript
(renderingData as ResponseSuccess).accessData.forEach(doSomething);
```

With no other attempts to use the value of uncertain type typecasting will do the job. Otherwise, typescript will ask you to cast a type every each attempt to access a value.

```typescript
//this won't work
if (data as TileInfo) {
    showPrice(data.price);
}

// you have to cast type each time to make it valid
if (data as TileInfo) {
    showPrice(data as TileInfo).price;
}
```

Both variants are ok when used appropriately to a situation.

## Links

-   Discriminated unions [http://www.typescriptlang.org/docs/handbook/advanced-types.html#discriminated-unions](http://www.typescriptlang.org/docs/handbook/advanced-types.html#discriminated-unions)
-   Type guarding with the `in` operator [http://www.typescriptlang.org/docs/handbook/advanced-types.html#using-the-in-operator](http://www.typescriptlang.org/docs/handbook/advanced-types.html#using-the-in-operator)
-   Type guards and type assertions [http://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-type-assertions](http://www.typescriptlang.org/docs/handbook/advanced-types.html#type-guards-and-type-assertions)

The combination of these two approaches may help to work safely with the inputs that may provide different types.

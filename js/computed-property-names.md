Computed property names are an es6 feature that lets you use the result of an expression as a key in an object by wrapping the expression in `[]`

```
const foo = { bar: 'baz' }

// Error!
const x = { foo.bar: 'myCoolValue' }

// Works!
const x = { [ foo.bar ]: 'myCoolValue' }

// {baz: "myCoolValue"}
```

Or using a function:

```
function getKey(){
    return 'baz';
}

// Error!
const x = { getKey(): 'myCoolValue' }

// Works!
const x = { [ getKey() ]: 'myCoolValue' }

// {baz: "myCoolValue"}

```

[source](https://tylermcginnis.com/computed-property-names/)

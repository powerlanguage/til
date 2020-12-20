Placing the `async` keyword before a function means **one thing**: the function always returns a promise. Other return values will be wrapped in a promise.

```
async function f() {
    return 1;
}

f().then(console.log);
```

is the same as:

```
function f() {
    return new Promise(function(resolve, reject){
        resolve(1);
    })
}

f().then(console.log);
```

The `await` keyword only works **inside** `async` functions. It is used before a promise to make javascript wait until that promise settles and returns its result.

```
async function f() {

    let promise = new Promise(function(resolve, reject){
        setTimeout(() => {
            resolve('Done!');
        }, 1000)
    })

    let result = await promise;

    console.log(result); // Done!
}

f()
```

Remember `await` **cannot** be used at the top level. It can only be used inside an `async` function. You either need to use a `.then` _or_ wrap the containing code in an async IIFE `(async () => {})()`;

```
async function wait() {
  await new Promise(resolve => setTimeout(resolve, 1000));

  return 10;
}

// Using then
wait().then(console.log) // logs 10 after 1 second

// Using IIFE

(async () => {
    let res = await wait(); // execution pauses as we're using await in async fn
    console.log(res); // logs 10 after 1 second
})()

```

## Examples

```
async function wait() {
  await new Promise(resolve => setTimeout(resolve, 1000));

  return 10;
}

x = wait(); // x is a promise because async functions always return promises
// x = Promise {<pending>}
// After 1 second
// x = Promise {<fulfilled>: 10}
```

Even though `10` is not a promise, the fact `wait` is an `async` function means it will always be returned as a promise.

Because `await` is used inside the `wait` function, the code execution pauses until the `setTimeout` is done. Then the promise returned from `wait` is resolved as `10`.

Question: Does the promise wrapping the `setTimeout` interact at all with the `10` returned? I don't think so, but am not 100%.

[Reference](https://javascript.info/async-await)

If you want to make a series of async calls in parallel `Promise.all` has got you covered. To make them in sequence (one being initiated after the other) you have two options:

- Loop
- Reduce

Shared code:

```
const timeStamp = () => {
  const d = new Date();
  return d.toLocaleTimeString();
};

const sleep = (ms, fruit) => {
  return new Promise((resolve) => {
    console.log("Running promise executor", fruit);
    setTimeout(() => {
      console.log("Resolving", fruit, timeStamp());
      resolve();
    }, ms);
  });
};

const fruitBasket = {
  apple: 27,
  pear: 69,
  banana: 420,
};

function getNumFruit(fruit) {
  return sleep(1000, fruit).then(() => {
    return fruitBasket[fruit];
  });
}

const fruits = Object.keys(fruitBasket);
```

## For Loop

Loop pauses at the `await` until the promise has resolved.

```
async function fetchFruitForLoop() {
  for (let i = 0; i < fruits.length; i++) {
    const fruit = fruits[i];
    console.log("Starting", fruit, timeStamp());
    let fruitNum = await getNumFruit(fruit);
    console.log(fruit, fruitNum);
  }
}
```

## For of Loop

As above, but shorter/simpler.

```
async function fetchFruitForOf() {
  for (const fruit of fruits) {
    let fruitNum = await getNumFruit(fruit);
    console.log(fruit, fruitNum);
  }
}
```

## Reduce

Not 100% on this. We can use the fact that the accumulator in the reduce can change over time. When the previous promise resolves, we attach to it via a `then` and call the next promise.

```
function fetchFruitReduce() {
  const fruitNums = fruits.reduce((prevPromise, nextFruit) => {
    console.log("Enqueing", nextFruit, timeStamp());
    return prevPromise.then(() => getNumFruit(nextFruit));
  }, Promise.resolve());
  fruitNums.then((val) => console.log(val));
}
```

Output:

```
Enqueing apple 2:12:25 PM
Enqueing pear 2:12:25 PM
Enqueing banana 2:12:25 PM
Running promise executor apple
Resolving apple 2:12:26 PM
Running promise executor pear
Resolving pear 2:12:27 PM
Running promise executor banana
Resolving banana 2:12:28 PM
```

I am still unclear on when you'd want to use one ve

- https://css-tricks.com/why-using-reduce-to-sequentially-resolve-promises-works/
- https://zellwk.com/blog/async-await-in-loops/
- https://stackoverflow.com/questions/40328932/javascript-es6-promise-for-loop - bunch of options here I am not entirely clear on

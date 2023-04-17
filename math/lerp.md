**Lerp** stands for _Linear Interpolation_. Given two numbers, find a number at some point between them. Used for easing or smoothing a value.

A Lerp function takes 3 parameters:

- `start` value
- `end` value
- `percentage` value (progress)

```
function lerp(start, end, percentage){
    return start + (end - start) * percentage
}
```

`percentage`

- closer to `0.1` returns a value closer to `start`
- closer to `0.9` returns a value closer to `end`

In order for the returned value to change, we need one of the inputs to change.

```
// We want x to move towards targetX
x = 0;
targetX = 100;

// This 'teleports' instantly
x = targetX

// What if we went 10% of the distance. And then 10% of the remaining distance. And then 10% of that remaining distance, etc.

// Note, we are reassigning x AND using it in the lerp function
x = lerp(x, targetX, 0.1)

// If this happens within a loop running at say 60fps we'll see x move towards targetX by 10% each update

```

[source](https://www.febucci.com/2018/08/easing-functions/)

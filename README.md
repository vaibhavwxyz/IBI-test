## 💡 Q1. What are the differences between cookie, local storage and session storage?

### 🚀 Answer

- **Cookies:** cookie are small data (upto 4kb), both persistent and sesstion-based, accessible on the client-side and server-side.
- **Local storage:** Local storage are larger data (5mb to 10 mb), remains indefinitely, accessible only on the client-side
- **Session storage:** Session storage are similar to local storage, but data clears when the browser session ends.

## 💡 Q2. Explain the output of the above-given code and explain why?

```javascript
for (var i = 0; i < 5; i++) {
  setTimeout(() => console.log(i), 100);
}
```

### 🚀 Answer

```javascript
Output: 5;
5;
5;
5;
5;
```

Explanation: The `for` loop uses `var` to declare `i`, which has function scope. The loop finishes, and when the `setTimeout` callback run, they all access the same `i` with the value 5. To get the desired output, use `let i` instead of `var i`.

## 💡 Q3. What is Sharding in MongoDB, and how does it work?

### 🚀 Answer

Sharding is a data partitioning technique used in MongoDB to horizontally distribute data across multiple servers or shards. Each shard is a separate database that holds a subset of the data, allowing MongoDB to scale horizontally and handle large datasets and high read/write loads efficiently.

## 💡 Q4. What is promise chaining? Explain with an example.

### 🚀 Answer

Promise chaining is a technique used in JavaScript to handel asynchronous operations sequentially by chaining multiple promises together using their `then()` method. Each `then()` block receives the resolved value of the previous promise, enabling a clean and readable way to handel asynchronous operations.

Example:

```javascript
fetch("https://api.example.com/data") // Returns a Promise
  .then((response) => response.json()) // Parse response as JSON
  .then((data) => {
    // Process the data from the first Promise
    return fetch(data.nextUrl); // Return a new Promise for the next request
  })
  .then((nextResponse) => nextResponse.json())
  .then((nextData) => {
    // Process data from the second request
    console.log(nextData);
  })
  .catch((error) => {
    // Handle errors from any of the Promises in the chain
    console.error("Error:", error);
  });
```

## 💡 Q5. What are Higher-Order Components (HOC) in React and how do they work?

### 🚀 Answer

HOCs are functions that take a component as an argument and return a new component with enhanced functionality. They allow you to reuse component logic and share code among multiple components. HOCs don't modify the original component; instead, they create a new one with added props or behavior.

**Example:**

```javascript
// Higher-Order Component to add a 'loading' prop to a component
const withLoading = (WrappedComponent) => {
  return class WithLoading extends React.Component {
    render() {
      const { isLoading, ...props } = this.props;
      if (isLoading) {
        return <div>Loading...</div>;
      }
      return <WrappedComponent {...props} />;
    }
  };
};

// Usage of the HOC with a component
const MyComponent = ({ data }) => {
  return <div>{data}</div>;
};

const MyComponentWithLoading = withLoading(MyComponent);

// Rendering the enhanced component
ReactDOM.render(
  <MyComponentWithLoading isLoading={true} />,
  document.getElementById("root")
);
```

## 💡 Q6. What is callback hell? Explain different ways to solve callback hell with examples each.

### 🚀 Answer

Callback hell refers to the situation where multiple nested callbacks are used in asynchronous JavaScript code, leading to deeply nested and hard-to-read code. It becomes challenging to manage control flow and handle errors. This commonly occurs when handling multiple asynchronous operations, such as API calls within callbacks.

**Ways to Solve Callback Hell:**

1. Use named functions:

```javascript
function step1(callback) {
  // Asynchronous operation...
  callback();
}

function step2(callback) {
  // Asynchronous operation...
  callback();
}

function step3(callback) {
  // Asynchronous operation...
  callback();
}

step1(() => {
  step2(() => {
    step3(() => {
      // Code after all steps are completed
    });
  });
});
```

2. Use Promises:

```javascript
function step1() {
  return new Promise((resolve, reject) => {
    // Asynchronous operation...
    resolve();
  });
}

function step2() {
  return new Promise((resolve, reject) => {
    // Asynchronous operation...
    resolve();
  });
}

function step3() {
  return new Promise((resolve, reject) => {
    // Asynchronous operation...
    resolve();
  });
}

step1()
  .then(() => step2())
  .then(() => step3())
  .then(() => {
    // Code after all steps are completed
  })
  .catch((error) => {
    // Handle errors
  });
```

## 💡 Q7. Use Array.reduce() method to reverse the following given array

```javasctipt
const arr = [1, 2, 3, 4, 5]
```

### 🚀 Answer

```javascript
const arr = [1, 2, 3, 4, 5];

const reversedArr = arr.reduce((acc, num) => {
  acc.unshift(num);
  return acc;
}, []);

console.log(reversedArr); // Output: [5, 4, 3, 2, 1]
```

## 💡 Q8. In what order will the numbers 1-4 be logged to the console when the code below is executed? Why?

```javascript
(function () {
  console.log(1);

  setTimeout(function () {
    console.log(2);
  }, 1000);

  setTimeout(function () {
    console.log(3);
  }, 0);

  console.log(4);
})();
```

### 🚀 Answer

```javascript
1;
4;
3;
2;
```

**Explanation:**

- The code starts executing synchronously, so console.log(1) is printed first.
- The setTimeout with a delay of 0 milliseconds is placed in the event queue. However, since it's non-zero, it will be executed after other synchronous tasks.
- console.log(4) is printed next.
- The setTimeout with a delay of 1000 milliseconds is placed in the event queue.
- Since the event loop is clear, the setTimeout with a delay of 0 milliseconds (from step 2) is moved from the event queue to the call stack and executed, resulting in console.log(3) being printed.
- Finally, after a delay of 1000 milliseconds, console.log(2) is printed.

## Q9. What will the code below output to the console and why?

```javascript
var arr1 = "john".split("");
var arr2 = arr1.reverse();
var arr3 = "jones".split("");

arr2.push(arr3);

console.log("array 1: length=" + arr1.length + " last=" + arr1.slice(-1));
console.log("array 2: length=" + arr2.length + " last=" + arr2.slice(-1));
```

### 🚀 Answer

**The output of the code will be:**

```javascript
array 1: length=5 last=5
array 2: length=5 last=j,o,n,e,s
```

**Explanation:**

- `arr1` is set to `["j", "o", "h", "n"]`.
- `arr2` is assigned the reference to `arr1` and then reversed, so both `arr1` and `arr2` now point to the same array `["n", "h", "o", "j"].`
- `arr3` is set to `["j", "o", "n", "e", "s"].`
- `arr2.push(arr3)` pushes the reference of arr3 to the end of arr2, so arr2 becomes `["n", "h", "o", "j", ["j", "o", "n", "e", "s"]]`.
- `arr1` is still pointing to the same array, so it has the same length as `arr2` (5) and the last element is `"n"`.
- `arr2` has a length of 5 and the last element is the array `["j", "o", "n", "e", "s"]`.

## 💡 Q10. What will the following code's output be in sequence and explain why?

```javascript
function printNumber(num) {
  console.log(num);
}

console.log(1);

setTimeout(printNumber, 0, 2);
setTimeout(printNumber, 100, 3);

console.log(4);
```

### 🚀 Answer

```javascript
1;
4;
2;
3;
```

**Explanation:**

- `console.log(1)` and `console.log(4)` are synchronous operations, so they are executed first and log `1` and `4` to the console, respectively.
- `setTimeout(printNumber, 0, 2)` is placed in the event queue with a delay of 0 milliseconds. Although the delay is 0, it will be executed after the synchronous tasks in the call stack are completed.
- The second `setTimeout(printNumber, 100, 3)` is placed in the event queue with a delay of 100 milliseconds.
- The event loop checks the event queue and finds the function `printNumber(2)` with the delay of 0 milliseconds. Since the call stack is empty, it moves this function from the event queue to the call stack and executes it, logging `2` to the console.
- The event loop then checks the event queue again and finds the function `printNumber(3)` with the delay of 100 milliseconds. After approximately 100 milliseconds, it moves this function from the event queue to the call stack and executes it, logging `3` to the console.
-

## 💡 Q11. Check the below given code, if there are any issues, fix them and explain the output

```javascript
const numbers = [1, 2, 3, 4, 5];
const result = numbers.reduce((acc, num) => {
  if (num % 2 === 0) {
    acc.evens.push(num);
  } else {
    acc.odds.push(num);
  }
  return acc;
});

console.log(result);
```

### 🚀 Answer

The given code has an issue because the initial value for the accumulator is not provided. The `reduce` function will not work as expected. To fix it, we need to provide an initial accumulator object with properties `evens` and `odds` as empty arrays.

**Fixed code:**

```javascript
const numbers = [1, 2, 3, 4, 5];

const result = numbers.reduce(
  (acc, num) => {
    if (num % 2 === 0) {
      acc.evens.push(num);
    } else {
      acc.odds.push(num);
    }
    return acc;
  },
  { evens: [], odds: [] }
);

console.log(result);
```

**output**

```javascript
{ evens: [2, 4], odds: [1, 3, 5] }
```

Now, the `reduce` function correctly accumulates the even and odd numbers into the `result` object, and the output displays separate arrays for even and odd numbers.

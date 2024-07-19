## Let's understand how JavaScript executes code

JavaScript executes code using js engine which is already present in browser.
Lets understand different parts which are involve in executing js code.

- **call stack** -> where code actually gets executed
- **callback queue** or **task queue** -> where async callbacks are stored before getting executed in call stack.
- **microtask queue** -> where high priority callbacks(such as promises and mutation observers) placed before getting executed in call stack.
- **web api** -> where async functions a kept before pushing them into microtask queue or callback queue.
- **event loop** -> which keeps on looking whether call stack is empty or not so that it can take and push the callback from task or microtask queue to call stack if there is any.

let's take an example

```
var num = 10;
console.log('start');

setTimeout(()=>{
    console.log('from setTimeout');
},1000);

let promise = new Promise((resolve,reject)=>{
    resolve('from promise');
})

promise.then((response)=>console.log(response));

console.log('end');
```

Above we have a small snippet.

- First when we run a js code it will create global execution context and pushes it into call stack. Which has two phases and execution context has two compinent namly memory and code

  1. **creation phase** : where all the var variables get memory allocated with undefined and all functions with function declaration get memory
     |memory|code|
     |:----:|:---:|
     |window : {...}| |
     |num:undefined| |
     |promise : | |

     - Here window object contains all the apis which are provided by browser.
     - As let belongs to TDZ promise variable is still not initialized with any value.

  2. **execution phase** : where all the js code gets executed line by line.

  - First var num is being initialized by 10.so now num value is changed to 10;
    memory|code|
    |:----:|:---:|
    |window : {...}| |
    |num:10| |
    |promise :{promise}| |

  - now console.log('start') pushed to call stack and this log function creates its own execution context with memory and code will print the 'start' to console and popped off from call stack.
  - Now setTimeout() is pushed into call stack as it is async function with some timer it gets popped off and sent to web api. when timer goes off this function is now pushed into callback queue.
  - Next promise object is created and initialized into promise variable.
  - Next we are calling promise with .then function as it is async in nature and it belongs to microtask first it is popped off from call stack to web api and web api pushed this promise to microtask queue.
  - now console.log('end') pushed to call stack and this log function creates its own execution context with memory and code will print the 'end' to console and popped off from call stack.
  - now global execution context also gets popped off from call stack.
  - Here comes the event loop which is looking whether call stack is empty or not. Now as it is empty it looks for are their any callback present in microtask queue(because it has higher priority than task queue). and pushes this attached callback to call stack. and it executes code by creating its own exeution context and logs 'from promise' and poped off from call stack.
  - event loop first pushes all the callbacks from microtask queue and then moves to task queue.
  - as microtask queue is empty now event loop goes for pushing callbacks from task queue to call stack and it logs 'from setTimeout' and pops the exection context of callback.

  ```
  //output
  start
  end
  from promise
  from setTimeout
  ```

## What is a Promise?

A **Promise** is a **object** which is representing eventual completion or failure of async operation.

```
// creating a promise
function createPromise() {
  return new Promise(function (resolve, reject) {
    //do some operation here
    //after getting required data call resolve()
    //else call reject()
    //resolve,reject are functions provided by js
    let gotData = false;
    if (gotData) {
      setTimeout(() => {
        resolve("resolved");
      }, 5000);
    } else {
      const err = new Error("Data is not found");
      reject(err);
    }
  });
}
```

> [!NOTE]
> UnhandledPromiseRejection: This error originated either by throwing inside of an async function without a catch block,
> or by rejecting a promise which was not handled with .catch().

## promisify an async callback functions

```
//promisify setTimeout

function pSetTimeout(callback, timeInSeconds) {
  return new Promise((resolve) => {
    setTimeout(() => {
      let res = callback();
      resolve(res);
    }, timeInSeconds * 1000);
  });
}

// pSetTimeout(() => "done", 5).then((data) => console.log(data));

//promisify fs.readFile
const fs = require("fs");
function pReadFile(path) {
  return new Promise((resolve, reject) => {
    fs.readFile(path, "utf8", (err, data) => {
      if (err) {
        reject(err);
      } else {
        resolve(data);
      }
    });
  });
}

pReadFile("./promise.js")
  .then((data) => console.log(data))
  .catch((err) => console.log(err));
```

## Chaining a promise

```
//with the help of promise chaining we can avoid callback hell
//creating a promise chain
//while creating a promise chain we have to return either a value or promise in attached functions by using .then
//eg :
let cart = ["shirt", "pants"];

// let promise = createOrder(cart);

// promise
//   .then((orderId) => {
//     console.log("OrderId :", orderId);
//     return orderId;
//   })
//   .then((orderId) => {
//     return proceedToPayment(orderId);
//   })
//   .then((paymentInfo) => {
//     console.log(paymentInfo);
//     return paymentInfo;
//   })
//   .then((paymentInfo) => {
//     return showOrderSummary(paymentInfo);
//   })
//   .then((orderSummary) => {
//     console.log(orderSummary);
//     return orderSummary;
//   })
//   .then((orderSummary) => {
//     return updateWallet(orderSummary);
//   })
//   .then((walletBalance) => {
//     console.log(walletBalance);
//   })
//   .catch((err) => {
//     console.log(err.message);
//   });

function createOrder(cart) {
  return new Promise(function (resolve, reject) {
    setTimeout(() => {
      if (cart.length > 0) {
        let orderId = "asad5efwe";
        resolve(orderId);
      } else {
        const err = new Error('"Cart order id is not found"');
        reject(err);
      }
    }, 5000);
  });
}

function proceedToPayment(orderId) {
  return new Promise(function (resolve, reject) {
    setTimeout(() => {
      if (orderId.length > 0) {
        resolve("Payment done Successfully");
      } else {
        const err = new Error("Payment is not Successfull");
        reject(err);
      }
    }, 4000);
  });
}

function showOrderSummary(paymentInfo) {
  return new Promise(function (resolve, reject) {
    setTimeout(() => {
      if (paymentInfo.length > 0) {
        resolve("Showing order summary");
      } else {
        const err = new Error("Failed showing orderSummary");
        reject(err);
      }
    }, 2000);
  });
}

function updateWallet(orderSummary) {
  return new Promise(function (resolve, reject) {
    setTimeout(() => {
      if (orderSummary.length > 0) {
        resolve("updated wallet balance");
      } else {
        const err = new Error("failed updating wallet balance");
        reject(err);
      }
    }, 1000);
  });
}
```

## Throwing error inside .then

```
//throwing err inside .then

// promise.then((data) => {
//   console.log(data);
//   throw new Error('from then block')
// });

//throwing err inside .then and using .catch()
//.catch() will handle the error if we throw error INSIDE .then() and also handle rejected promise

// promise
//   .then((data) => {
//     console.log(data);
//     throw new Error("from then block");
//   })
//   .then((data) => console.log(data)) // i wont get executed
//   .catch((err) => console.log(err.message));


```

## Using .catch() between .then() chain and finally block

```
//we can also have .catch between .then() to handle a particular err
//but all the .then() will execute after .catch if no err is present
//eg:

// let ex = createPromise();
// ex.then()
//   .catch()
//   .then(() => {
//     console.log("i will execute no matter what");
//   })
//   .finally(() => {
//     console.log("I also execute no matter what");
//   });

//.catch() at last of chaining can catch all the error above it.
//.finally() always execute whether catch() or then()  execute or not

``
```

## Promise functions

- **Promise.all(iterable)**
  - makes all api calls parallel and wait for all of them to finish (incase all pronies are resolved)
  - As soon as anyone of the promise is rejected it throws an error immediately it will not wait for other promises.
- **Promise.allSettled(iterable)**
  - Irrespective of success or failure it will wait for all the promises to be settled and gives array of object
  - for resolved value object -> { status: 'fulfilled' , value : 'resolved value' }
  - for reject value object -> { status : 'rejected' , reason : 'reason' }
- **Promise.race(iterable)**
    - returns result of first settled(either resolved or rejected) promise.
- **Promise.any(iterable)** 
  - wait for 1st success of promise to return the value.
  - if all the promises are rejected then returns aggregate error which is array of all errors.
  - To access array of errors use (err.errors)
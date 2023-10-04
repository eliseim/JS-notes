# Object destructuring

- https://blog.greenroots.info/javascript-object-destructuring-usages-you-must-know
- https://www.freecodecamp.org/news/javascript-object-destructuring-spread-operator-rest-parameter/

Store data in `key` - `value` pairs (aka `object properties`):

```js
const employee = {
  id: 007,
  name: "James",
};
```

## ⭐ Basic destructuring

```js
const employee = {
  id: 007,
  name: "James",
};

// Traditionally retrieving the values:
const id = employee.id;
const name = employee.name;

// --- Destructuring assignment syntax ---
const { id, name } = employee;

// ⚠️ The keywords let and const are significant in object destructuring
{ name  } = employee // Uncaught SyntaxError: Unexpected token '='

// Parenthesis `(...)` are required when you want to omit the let or const keyword:
({ name  } = employee);
```

## ⭐ Nested object destructuring

```js
const employee = {
  id: 007,
  name: "James",
  dept: {
    id: "D001",
    name: "Spy",
    address: {
      street: "30 Wellington Square",
      city: "Chelsea",
    },
  },
};

// Traditional:
const street = employee.dept.address.street;
console.log(street); // 30 Wellington Square

// --- Destructure: ---
const {
  dept: {
    address: { street },
  },
} = employee;
console.log(street); // 30 Wellington Square
```

## ⭐ Define a new variable (& default value) with object destructuring

```js
const employee = {
  id: 007,
  name: "James",
  dept: "Spy",
};

// Traditional:
const age = employee.age ? employee.age : 25;

// --- Destructure: ---
const { name, age = 25 } = employee;

// More magic!
// Add a new variable `message` and assign a value computed
// using the object property values:
const { name, dept, message = `${name} is ${dept}` } = employee;
console.log(message); // James is Spy
```

## ⭐ Add Aliases

Let's assume your source code has an existing variable named `dept`. So if we use the same variable name in destructuring, there will be a name conflict.
Instead, you can use an alias name to create the variable with this new name.

```js
const employee = {
  id: 007,
  name: "James",
  dept: "Spy",
};

const { dept: department } = employee;
console.log(department); //Spy
console.log(dept); // Uncaught ReferenceError: dept is not defined
```

## ⭐ Handle Dynamic Name Property

We often handle API response data as JavaScript objects. These objects may contain dynamic data such that, as a client, we may not even know the property key names in advance.

The method `getPropertyValue(key)` takes a property key name and should return the value of it

```js
const employee = {
  id: 007,
  name: "James",
};

const name = getPropertyValue("name");
console.log(name); // James
```

Create a function that returns the value of the employee object properties when we pass a key as an argument:

```js
function getPropertyValue(key) {
  const { [key]: returnValue } = employee;
  return returnValue;
}
```

The square brackets([..]) around the key in the destructuring assignment. The key we pass to the function gets evaluated, and the value is retrieved from the object.

## ⭐ Destructure objects in the function argument and return value

Use object destructuring to pass the property values as arguments to the function

```js
const employee = {
  return {
    id: 007,
    name: "James",
    dept: "Spy";
  };
};

function logEmployee({name, dept}) {
  console.log(`${name} is ${dept}`);
}

logEmployee(employee); // James is Spy
```

### Another usage with a function

If a function returns an object, you can destructure the values directly into variables.

```js
function getUser() {
  return {
    name: "Alex",
    age: 45,
  };
}
const { age } = getUser();
console.log(age); // 45
```

## ⭐ Destructuring in loops

```js
const employees = [
  {
    name: "Alex",
    age: 43,
  },
  {
    name: "John",
    age: 33,
  },
];

for (let { name, age } of employees) {
  console.log(`${name} is ${age} years old!`);
}
// Alex is 43 years old!
// John is 33 years old!
```

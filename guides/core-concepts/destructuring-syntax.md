# Destructuring Syntax in TypeScript

## Overview

Destructuring is a JavaScript/TypeScript syntax that allows you to extract values from arrays or properties from objects into distinct variables. It's fundamental to modern React Native development and makes code more readable and concise.

## Prerequisites

- Basic understanding of JavaScript objects and arrays
- Familiarity with TypeScript types
- Understanding of variable declarations (`const`, `let`)

## Why Destructuring Matters

**Without destructuring:**
```typescript
const user = { name: 'John', age: 30, email: 'john@example.com' };
const name = user.name;
const age = user.age;
const email = user.email;
```

**With destructuring:**
```typescript
const user = { name: 'John', age: 30, email: 'john@example.com' };
const { name, age, email } = user;
```

Destructuring reduces boilerplate code and makes your intent clearer - you're explicitly stating which properties you need.

## Object Destructuring

### Basic Syntax

```typescript
const person = {
  name: 'Alice',
  age: 28,
  city: 'San Francisco'
};

// Extract properties into variables
const { name, age, city } = person;

console.log(name);  // 'Alice'
console.log(age);   // 28
console.log(city);  // 'San Francisco'
```

**How it works:** Variable names must match the object's property names.

### Partial Extraction

You don't need to extract all properties:

```typescript
const person = {
  name: 'Alice',
  age: 28,
  city: 'San Francisco',
  job: 'Engineer'
};

// Extract only what you need
const { name, city } = person;
// age and job are ignored
```

### Renaming Variables

Use the colon (`:`) to rename while destructuring:

```typescript
const user = { name: 'Bob', age: 35 };

const { name: userName, age: userAge } = user;
//      ^^^^  ^^^^^^^^
//      key   new variable name

console.log(userName);  // 'Bob'
console.log(userAge);   // 35
console.log(name);      // ❌ ReferenceError: name is not defined
```

### Default Values

Provide fallback values for undefined properties:

```typescript
const settings = { theme: 'dark' };

const { theme, language = 'en', fontSize = 14 } = settings;

console.log(theme);     // 'dark'
console.log(language);  // 'en' (default)
console.log(fontSize);  // 14 (default)
```

### Nested Destructuring

Extract properties from nested objects:

```typescript
const user = {
  name: 'Charlie',
  address: {
    street: '123 Main St',
    city: 'Boston',
    coordinates: {
      lat: 42.3601,
      lng: -71.0589
    }
  }
};

// Destructure nested properties
const {
  name,
  address: {
    city,
    coordinates: { lat, lng }
  }
} = user;

console.log(name);  // 'Charlie'
console.log(city);  // 'Boston'
console.log(lat);   // 42.3601
console.log(lng);   // -71.0589

// Note: 'address' and 'coordinates' variables are NOT created
console.log(address);  // ❌ ReferenceError
```

**Common pitfall:** When destructuring nested objects, only the innermost properties become variables.

### Rest Operator with Objects

Collect remaining properties using the rest operator (`...`):

```typescript
const user = {
  id: 1,
  name: 'Diana',
  age: 29,
  email: 'diana@example.com',
  city: 'Seattle'
};

const { id, name, ...otherInfo } = user;

console.log(id);        // 1
console.log(name);      // 'Diana'
console.log(otherInfo); // { age: 29, email: 'diana@example.com', city: 'Seattle' }
```

**Important:** Rest operator must be the last element in destructuring.

```typescript
// ✅ Valid
const { a, b, ...rest } = obj;

// ❌ Invalid
const { a, ...rest, b } = obj;  // SyntaxError
```

## Array Destructuring

### Basic Syntax

```typescript
const colors = ['red', 'green', 'blue'];

// Extract by position
const [first, second, third] = colors;

console.log(first);   // 'red'
console.log(second);  // 'green'
console.log(third);   // 'blue'
```

**How it works:** Variables are assigned based on array position, not name.

### Skipping Elements

Use commas to skip array elements:

```typescript
const numbers = [1, 2, 3, 4, 5];

const [first, , third, , fifth] = numbers;
//           ^        ^
//           skip     skip

console.log(first);  // 1
console.log(third);  // 3
console.log(fifth);  // 5
```

### Default Values

Provide defaults for undefined array elements:

```typescript
const coordinates = [10];

const [x = 0, y = 0, z = 0] = coordinates;

console.log(x);  // 10
console.log(y);  // 0 (default)
console.log(z);  // 0 (default)
```

### Rest Operator with Arrays

Collect remaining elements:

```typescript
const [first, second, ...rest] = [1, 2, 3, 4, 5];

console.log(first);   // 1
console.log(second);  // 2
console.log(rest);    // [3, 4, 5]
```

### Swapping Variables

Elegant variable swapping without a temporary variable:

```typescript
let a = 1;
let b = 2;

// Swap values
[a, b] = [b, a];

console.log(a);  // 2
console.log(b);  // 1
```

## Function Parameter Destructuring

### Object Parameters

```typescript
// ❌ Without destructuring
function createUser(config) {
  const name = config.name;
  const age = config.age;
  const email = config.email;
  // ...
}

// ✅ With destructuring
function createUser({ name, age, email }) {
  console.log(name, age, email);
}

createUser({ name: 'Eve', age: 25, email: 'eve@example.com' });
```

### Default Parameters

```typescript
function createButton({
  label = 'Submit',
  color = 'blue',
  disabled = false
}) {
  console.log(label, color, disabled);
}

createButton({ label: 'Click me' });
// Outputs: 'Click me' 'blue' false
```

### Combining with Rest Operator

```typescript
function logUser({ name, age, ...otherDetails }) {
  console.log(`Name: ${name}, Age: ${age}`);
  console.log('Other details:', otherDetails);
}

logUser({
  name: 'Frank',
  age: 32,
  city: 'Austin',
  job: 'Designer'
});
// Name: Frank, Age: 32
// Other details: { city: 'Austin', job: 'Designer' }
```

## React Native Examples

### Component Props

```typescript
import { View, Text, TouchableOpacity } from 'react-native';

// ❌ Without destructuring
function Button(props) {
  return (
    <TouchableOpacity onPress={props.onPress}>
      <Text>{props.label}</Text>
    </TouchableOpacity>
  );
}

// ✅ With destructuring
function Button({ label, onPress }) {
  return (
    <TouchableOpacity onPress={onPress}>
      <Text>{label}</Text>
    </TouchableOpacity>
  );
}
```

### Hooks

```typescript
import { useState } from 'react';

// Array destructuring with useState
const [count, setCount] = useState(0);
//     ^^^^^  ^^^^^^^^
//     value  setter function

const [user, setUser] = useState({ name: 'Alice', age: 28 });
```

### Testing Library

```typescript
import { render, fireEvent } from '@testing-library/react-native';

test('button responds to press', () => {
  // Object destructuring from render result
  const { getByText, getByTestId } = render(<Button label="Click me" />);

  const button = getByTestId('button');
  fireEvent.press(button);
});
```

### API Responses

```typescript
async function fetchUser(id: number) {
  const response = await fetch(`/api/users/${id}`);
  const data = await response.json();

  // Extract only needed fields
  const { name, email, avatar } = data;

  return { name, email, avatar };
}
```

### Props Forwarding

```typescript
interface CustomButtonProps {
  label: string;
  variant?: 'primary' | 'secondary';
  onPress: () => void;
}

function CustomButton({ label, variant = 'primary', ...restProps }: CustomButtonProps) {
  return (
    <TouchableOpacity {...restProps}>
      {/* Spread remaining props to TouchableOpacity */}
      <Text>{label}</Text>
    </TouchableOpacity>
  );
}

// Usage
<CustomButton
  label="Submit"
  onPress={handlePress}
  testID="submit-button"
  accessibilityLabel="Submit form"
/>
```

## TypeScript Types with Destructuring

### Typing Destructured Parameters

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;
}

function greetUser({ name, age }: User) {
  if (age) {
    console.log(`Hello ${name}, you are ${age} years old`);
  } else {
    console.log(`Hello ${name}`);
  }
}
```

### Typing Destructured Variables

```typescript
interface Config {
  theme: 'light' | 'dark';
  language: string;
  notifications: boolean;
}

const config: Config = {
  theme: 'dark',
  language: 'en',
  notifications: true
};

const { theme, language }: Config = config;
// theme is typed as 'light' | 'dark'
// language is typed as string
```

### Partial Destructuring with Types

```typescript
interface ApiResponse {
  data: any;
  status: number;
  headers: Record<string, string>;
  config: object;
}

function handleResponse(response: ApiResponse) {
  // TypeScript knows these properties exist
  const { data, status } = response;
}
```

## Common Patterns

### Extracting from Function Returns

```typescript
function getUserInfo() {
  return {
    name: 'George',
    age: 40,
    email: 'george@example.com'
  };
}

// Destructure immediately
const { name, email } = getUserInfo();
```

### Conditional Destructuring

```typescript
const user = getUser(); // might be null

if (user) {
  const { name, email } = user;
  console.log(name, email);
}

// Or with optional chaining (TypeScript 3.7+)
const { name, email } = getUser() ?? { name: 'Guest', email: '' };
```

### Import Statements

```typescript
// Named imports use destructuring syntax
import { View, Text, StyleSheet } from 'react-native';
import { useState, useEffect } from 'react';

// This is similar to:
const ReactNative = require('react-native');
const { View, Text, StyleSheet } = ReactNative;
```

## Spread Operator vs Destructuring

### Spread Operator (Creating)

Used on the **right side** of assignment to expand/copy:

```typescript
const original = { a: 1, b: 2 };

// Copy object
const copy = { ...original };

// Merge objects
const merged = { ...obj1, ...obj2 };

// Add properties
const extended = { ...original, c: 3 };
```

### Destructuring (Extracting)

Used on the **left side** of assignment to extract:

```typescript
const object = { a: 1, b: 2, c: 3 };

// Extract properties
const { a, b } = object;
```

### Using Both Together

```typescript
const user = { id: 1, name: 'Hannah', age: 27, city: 'Portland' };

// Destructure then spread
const { id, ...userWithoutId } = user;

const updated = { ...userWithoutId, age: 28 };
// { name: 'Hannah', age: 28, city: 'Portland' }
```

## Common Pitfalls

### 1. Variable Name Mismatch

```typescript
const obj = { name: 'John' };

// ❌ Wrong - 'username' doesn't exist on obj
const { username } = obj;
console.log(username);  // undefined

// ✅ Correct - use rename syntax
const { name: username } = obj;
console.log(username);  // 'John'
```

### 2. Destructuring Null or Undefined

```typescript
const data = null;

// ❌ Error - Cannot destructure null
const { value } = data;  // TypeError

// ✅ Safe - provide default object
const { value } = data ?? { value: 'default' };
```

### 3. Nested Destructuring Confusion

```typescript
const user = {
  info: { name: 'Ian', age: 33 }
};

// ❌ Common mistake - 'info' is not a variable
const { info: { name } } = user;
console.log(info);  // ReferenceError

// ✅ Create both variables if needed
const { info, info: { name } } = user;
console.log(info);  // { name: 'Ian', age: 33 }
console.log(name);  // 'Ian'
```

### 4. Array Index Assumptions

```typescript
const coords = [10];

// ❌ Dangerous - assumes array has 2 elements
const [x, y] = coords;
console.log(y);  // undefined

// ✅ Safe - use defaults
const [x, y = 0] = coords;
console.log(y);  // 0
```

## Performance Considerations

Destructuring has **no performance penalty** - it's syntactic sugar that compiles to simple property access. Modern JavaScript engines optimize it effectively.

```typescript
// These are equivalent in performance:
const name = user.name;
const { name } = user;
```

## Best Practices

### ✅ Do

- Use destructuring to make code intent clear
- Destructure in function parameters for cleaner signatures
- Use default values to avoid undefined checks
- Combine with TypeScript types for safety

### ❌ Don't

- Over-nest destructuring (max 2-3 levels for readability)
- Destructure everything (only extract what you use)
- Use destructuring with potentially null/undefined values without safety checks

## Summary

| Syntax | Purpose | Example |
|--------|---------|---------|
| `const { a, b } = obj` | Extract object properties | `const { name } = user` |
| `const [a, b] = arr` | Extract array elements | `const [x, y] = coords` |
| `const { a: newName } = obj` | Rename while extracting | `const { name: userName } = user` |
| `const { a = 1 } = obj` | Provide default value | `const { count = 0 } = data` |
| `const { a, ...rest } = obj` | Collect remaining properties | `const { id, ...user } = data` |
| `const { a: { b } } = obj` | Nested destructuring | `const { user: { name } } = response` |

## Further Reading

- [MDN: Destructuring Assignment](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
- [TypeScript Handbook: Object Destructuring](https://www.typescriptlang.org/docs/handbook/variable-declarations.html#destructuring)
- [React Documentation: Components and Props](https://react.dev/learn/passing-props-to-a-component)

---

**Next Steps:** Learn about [spread operators](./spread-operator.md) and [rest parameters](./rest-parameters.md) to complement your destructuring knowledge.

# Angular Signal Definition

**Angular Signal** is a simple way to store a value that can change over time and automatically update anything that uses it.

## Key Points
- Signals are functions that hold a value and notify dependents when the value changes.
- They help in building reactive UIs without the need for manual change detection or complex state management.
- Signals can be read, written, and subscribed to, making them flexible for various use cases.

## Example Usage
```typescript
import { signal } from '@angular/core';

const counter = signal(0);

// Read the value
console.log(counter()); // 0

// Update the value
counter.set(1);
console.log(counter()); // 1
```

---
*Update this README as you add more information or examples about Angular Signals.*

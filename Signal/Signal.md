# Angular Signals: Essential Usage Examples

Below are practical code examples for using Angular signals in a component, covering creation, updating, set, effect, and template usage.

```typescript
import { Component, signal, computed, effect } from '@angular/core';

@Component({
	selector: 'app-signal-demo',
	template: `
		<div>
			<p>Count: {{ count() }}</p>
			<p>Double: {{ double() }}</p>
			<button (click)="increment()">Increment</button>
			<button (click)="reset()">Reset</button>
		</div>
	`
})
export class SignalDemoComponent {
	// Creating a signal
	count = signal(0);

	// Updating a signal using set
	increment() {
		this.count.set(this.count() + 1);
	}

	// Resetting a signal
	reset() {
		this.count.set(0);
	}

	// Computed signal
	double = computed(() => this.count() * 2);

	// Using effect to react to changes
	logEffect = effect(() => {
		console.log('Count changed:', this.count());
	});
}
```

**Key Points:**
- Use `signal(initialValue)` to create a signal.
- Read a signal’s value by calling it as a function: `count()`.
- Update a signal with `.set(newValue)` or `.update(fn)`.
- Use `computed(() => ...)` for derived values.
- Use `effect(() => ...)` to react to changes in signals.
- Use signals directly in Angular templates: `{{ count() }}`.

# Angular Signals Interview Questions (Grouped by Topic)

## 1. Basics of Angular Signals
1. What are Angular signals?
	- Angular signals are reactive primitives introduced in Angular to manage and track state changes efficiently, enabling fine-grained reactivity in applications.
2. What is the primary use case for signals in Angular?
	- Signals are used to manage local and shared state reactively, allowing components to automatically update when the state changes.
3. How do signals differ from traditional observables in Angular?
	- Signals are synchronous, have no concept of subscriptions, and update automatically, while observables are asynchronous and require manual subscription management.
4. How do you create a signal in Angular?
	- Use the `signal` function: `const count = signal(0);`.
5. How do you read the value of a signal?
	- Call the signal as a function: `count()` returns the current value.
6. How do you update the value of a signal?
	- Use the `set` method: `count.set(newValue);` or use `update` for functional updates.
7. What is the syntax for declaring a signal in Angular?
	- `const mySignal = signal(initialValue);`
8. How do you reset a signal to its initial value?
	- Store the initial value and use `set(initialValue)` to reset.
9. How do you use signals in Angular templates?
	- Reference the signal as a function in the template: `{{ count() }}`.
10. How do you subscribe to changes in a signal?
	- Use the `effect` function to react to signal changes: `effect(() => { ... });`

## 2. Computed Signals and Effects
11. What is a computed signal?
	- A computed signal derives its value from other signals and updates automatically when dependencies change.
12. How do you create a computed signal in Angular?
	- Use the `computed` function: `const double = computed(() => count() * 2);`
13. What is the difference between a signal and a computed signal?
	- A signal holds state, while a computed signal derives its value from other signals.
14. What is the `effect` function in the context of signals?
	- `effect` runs a side-effectful function whenever its dependent signals change.
15. How do you use the `effect` function with signals?
	- `effect(() => { console.log(count()); });` runs whenever `count` changes.
16. How do you handle side effects with signals?
	- Use the `effect` function to perform side effects in response to signal changes.
17. How do you memoize computations with signals?
	- Use computed signals to memoize derived values based on dependencies.
18. How do you throttle or debounce updates to a signal?
	- Implement throttling/debouncing logic inside an `effect` or use a custom utility with signals.
19. How do you combine multiple signals?
	- Use a computed signal that depends on multiple signals: `computed(() => a() + b())`.
20. How do you handle errors in signals?
	- Use try-catch blocks inside computed or effect functions to handle errors gracefully.

## 3. Signals vs Observables and RxJS
21. How do signals compare to RxJS subjects?
	- Signals are synchronous and push-based, while RxJS subjects are asynchronous and require subscriptions.
22. What are the benefits of using signals over observables?
	- Signals offer simpler syntax, automatic updates, and better performance for local state.
23. How do you convert an observable to a signal?
	- Use a helper function like `toSignal(observable)` from Angular utilities.
24. How do you convert a signal to an observable?
	- Use a utility like `toObservable(signal)` to bridge signals and observables.
25. What are the limitations of signals in Angular?
	- Signals are not suitable for asynchronous streams or event-based data; observables are better for those cases.
26. How do signals improve performance in Angular applications?
	- Signals enable fine-grained reactivity, reducing unnecessary change detection cycles.
27. How do signals affect Angular’s rendering process?
	- Signals trigger updates only for components that depend on them, optimizing rendering.
28. What is the difference between signals and Angular zones?
	- Signals provide reactivity without relying on zones, allowing for more predictable updates.
29. How do signals work with Angular’s OnPush change detection strategy?
	- Signals work seamlessly with OnPush, as they trigger updates only when their value changes.
30. How do you unsubscribe from a signal?
	- Signals do not require manual unsubscription; they are automatically managed by Angular.

## 4. State Management and Sharing
31. Can signals be used for state management in Angular?
	- Yes, signals can manage both local and shared state reactively.
32. How do you use signals for global application state?
	- Define signals in a service and inject the service where needed.
33. How do you use signals for local component state?
	- Declare signals directly in the component class for local state.
34. How do you share a signal between components?
	- Provide the signal via a service and inject the service into multiple components.
35. How do you pass a signal as an input to a child component?
	- Pass the signal reference as an input property to the child component.
36. How do you emit events from a signal?
	- Update the signal’s value to represent an event or use an effect for side effects.
37. How do you persist signal state across page reloads?
	- Sync the signal’s value with localStorage or another persistent storage in an effect.
38. How do you use signals in Angular services?
	- Declare signals as properties in the service and expose them to consumers.
39. How do you use signals in Angular standalone components?
	- Use signals as you would in any component; standalone components support signals natively.
40. How do you use signals in Angular modules?
	- Signals can be used in any component or service within a module.

## 5. Signals in Angular Features
41. How do you use signals with Angular forms?
	- Bind form controls to signals and update signals on form value changes.
42. How do you use signals for form validation?
	- Use computed signals to derive validation state from form signals.
43. How do you use signals with Angular’s forms API?
	- Integrate signals with reactive or template-driven forms by syncing values.
44. How do you use signals with Angular’s reactive forms?
	- Use effects to update signals when form values change and vice versa.
45. How do you use signals with Angular’s template-driven forms?
	- Bind signals to ngModel and update them in response to user input.
46. How do you use signals with Angular’s form controls?
	- Use signals to represent the value and validity of form controls.
47. How do you use signals with Angular’s form groups?
	- Represent form group state as a signal and update it based on child controls.
48. How do you use signals with Angular’s form arrays?
	- Use signals to manage the array of form controls and their values.
49. How do you use signals with Angular’s validators?
	- Use computed signals to represent validation results and errors.
50. How do you use signals with Angular’s async validators?
	- Use effects to trigger async validation and update signals with results.

## 6. Signals in Angular Templates and Components
51. How do you use signals in Angular templates?
	- Reference signals as functions in the template: `{{ mySignal() }}`.
52. How do you use signals with Angular’s template reference variables?
	- Pass signals to template reference variables for dynamic template updates.
53. How do you use signals with Angular’s structural directives?
	- Use signals to control structural directives like *ngIf or *ngFor.
54. How do you use signals with Angular’s attribute directives?
	- Bind signals to directive inputs for reactive behavior.
55. How do you use signals with Angular’s custom pipes?
	- Pass signal values to custom pipes for transformation.
56. How do you use signals with Angular’s built-in pipes?
	- Use signal values as input to built-in pipes in templates.
57. How do you use signals with Angular’s content projection?
	- Pass signal values to projected content via input bindings.
58. How do you use signals with Angular’s view encapsulation?
	- Signals work independently of view encapsulation; use as normal.
59. How do you use signals with Angular’s change detection strategies?
	- Signals trigger updates only for dependent components, supporting all strategies.
60. How do you use signals with Angular’s lifecycle hooks?
	- Use signals in lifecycle hooks to react to or update state as needed.

## 7. Signals and Angular Services/DI
61. How do signals interact with Angular’s dependency injection?
	- Signals can be provided via services and injected using Angular’s DI system.
62. Can signals be used in Angular services?
	- Yes, signals are often used in services for shared state.
63. How do you use signals with Angular’s dependency injection tokens?
	- Provide signals using custom injection tokens for advanced scenarios.
64. How do you use signals with Angular’s environment variables?
	- Initialize signals with values from environment variables at startup.
65. How do you use signals with Angular’s HTTP interceptors?
	- Use signals in interceptors to manage or react to HTTP state changes.
66. How do you use signals with Angular’s guards?
	- Use signals to represent authentication or authorization state in guards.
67. How do you use signals with Angular’s resolvers?
	- Use signals to store and provide resolved data to components.
68. How do you use signals with Angular’s event emitters?
	- Use signals as an alternative to event emitters for state changes.
69. How do you use signals with Angular’s router?
	- Use signals to track and react to route changes.
70. How do you use signals with Angular’s HTTP requests?
	- Store HTTP response data in signals and update UI reactively.

## 8. Signals and Application Architecture
71. How do you use signals with Angular’s dependency graph?
	- Use signals to represent dependencies and propagate changes through the graph.
72. How do you use signals with Angular’s schematic tools?
	- Integrate signals into schematics for code generation or scaffolding.
73. How do you use signals with Angular’s workspace configuration?
	- Use signals to manage and react to configuration changes.
74. How do you use signals with Angular’s build process?
	- Use signals in build scripts or tools for reactive configuration.
75. How do you use signals with Angular’s deployment process?
	- Use signals to manage deployment state or environment-specific settings.
76. How do you use signals with Angular’s server-side rendering (SSR)?
	- Use signals for state management in SSR-compatible ways.
77. How do you use signals with Angular’s progressive web app (PWA) features?
	- Use signals to manage PWA state, such as offline status or updates.
78. How do you use signals with Angular’s service workers?
	- Use signals to track service worker status and events.
79. How do you use signals with Angular’s web workers?
	- Use signals to communicate state between main thread and web workers.
80. How do you use signals with Angular’s logging?
	- Use signals to track and react to log events or state changes.

## 9. Signals and Testing/Debugging
81. How do you test components that use signals?
	- Test by updating signals and asserting the component’s response.
82. How do you use signals in Angular unit tests?
	- Manipulate signals in tests and check for expected UI or logic changes.
83. How do you mock signals in tests?
	- Provide mock signal implementations or use test doubles.
84. How do you debug signals in Angular?
	- Use logging in effects or computed signals to trace changes.
85. How do you use signals with Angular’s debugging tools?
	- Inspect signal values and effects using Angular DevTools or console logs.
86. How do you use signals with Angular’s performance profiling?
	- Profile signal updates and their impact on rendering using profiling tools.
87. How do you use signals with Angular’s error handling?
	- Handle errors in effects or computed signals and update error signals.
88. How do you clean up resources used by signals?
	- Clean up in component destroy hooks or use teardown logic in effects.
89. What is the lifecycle of a signal in Angular?
	- Signals are created, updated, and destroyed with their owning component or service.
90. How do you use signals with Angular’s CLI commands?
	- Use signals in CLI-generated code or scripts for state management.

## 10. Signals and Advanced Angular Features
91. How do you use signals with Angular’s accessibility features?
	- Use signals to manage and update accessibility-related state reactively.
92. How do you use signals with Angular’s internationalization (i18n)?
	- Store and update locale or translation state in signals.
93. How do you use signals with Angular’s localization (l10n)?
	- Use signals to manage localized content and react to locale changes.
94. How do you use signals with Angular’s testing utilities?
	- Integrate signals into test setups and assertions.
95. How do you use signals with Angular’s animations?
	- Use signals to trigger and control animations based on state changes.
96. How do you use signals with Angular’s event system?
	- Use signals to represent and react to custom events.
97. How do you use signals with Angular’s router events?
	- Track router events in signals and update UI accordingly.
98. How do you use signals with Angular’s guards and resolvers?
	- Use signals to store and provide guard or resolver results.
99. How do you use signals with Angular’s workspace configuration?
	- Use signals to manage and react to workspace configuration changes.
100. How do you use signals with Angular’s project structure?
	- Organize signals by feature or domain for maintainable project structure.

## Difference Between set and update Methods

- **set(newValue):** Directly assigns a new value to the signal, replacing the current value.
	- Example: `count.set(5);` sets the signal value to 5.
- **update(fn):** Updates the signal’s value based on its current value by applying a function.
	- Example: `count.update(v => v + 1);` increments the current value by 1.

Use `set` when you know the exact value to assign, and `update` when you want to modify the value based on its previous state.

## Difference Between Writable and Readonly Signals

- **Writable Signal:**
	- Allows both reading and updating its value.
	- You can use `.set()` and `.update()` methods to change its value.
	- Example: `const count = signal(0); count.set(5);`

- **Readonly Signal:**
	- Can only be read, not updated directly.
	- Created using the `asReadonly()` method or by returning a signal as readonly from a service/component.
	- Prevents accidental modification from outside the owner.
	- Example:
		```typescript
		const count = signal(0);
		const readonlyCount = count.asReadonly();
		// readonlyCount.set(5); // Error: set is not available
		```

Use writable signals for internal state management and expose readonly signals to consumers to enforce immutability.

## How to Convert Observable into Signal

Angular provides a utility function called `toSignal` to convert an RxJS Observable into a Signal.

**Example:**

```typescript
import { Component, computed, effect, signal, toSignal } from '@angular/core';
import { Observable, interval } from 'rxjs';

@Component({
	selector: 'app-observable-to-signal',
	template: `<p>Value: {{ value() }}</p>`
})
export class ObservableToSignalComponent {
	// Example Observable
	source$: Observable<number> = interval(1000);

	// Convert Observable to Signal
	value = toSignal(this.source$, { initialValue: 0 });
}
```

**Key Points:**

## How to Convert Subject into Signal

A Subject in RxJS is both an Observable and an Observer. To convert a Subject into a Signal, you can use the same `toSignal` utility, since a Subject is an Observable.

**Example:**

```typescript
import { Component, toSignal } from '@angular/core';
import { Subject } from 'rxjs';

@Component({
	selector: 'app-subject-to-signal',
	template: `
		<button (click)="emitValue()">Emit Value</button>
		<p>Latest Value: {{ value() }}</p>
	`
})
export class SubjectToSignalComponent {
	subject$ = new Subject<number>();
	value = toSignal(this.subject$, { initialValue: 0 });

	emitValue() {
		this.subject$.next(Math.floor(Math.random() * 100));
	}
}
```

**Key Points:**
- A Subject can be converted to a Signal using `toSignal(subject$, { initialValue })`.
- The Signal will always reflect the latest value emitted by the Subject.

## Difference Between Angular Signals and RxJS Observables

| Feature                | Angular Signals                        | RxJS Observables                |
|------------------------|----------------------------------------|---------------------------------|
| Reactivity Model       | Fine-grained, synchronous              | Push-based, asynchronous        |
| Subscriptions         | No subscriptions needed                | Requires manual subscriptions   |
| Memory Management      | Automatic, no unsubscribe needed       | Must unsubscribe to avoid leaks |
| Change Detection       | Triggers only affected consumers       | May trigger broader updates     |
| Use Case               | Local/component state, UI reactivity   | Streams, async data, events     |
| API Simplicity         | Simple, function-based                 | Rich, operator-heavy            |
| Error Handling         | Try/catch in computed/effect           | catchError, error callbacks     |
| Async Support          | Not for async streams                  | Designed for async streams      |
| Integration            | Native in Angular (v16+)               | External RxJS library           |

**Key Points:**
- Signals are best for local, synchronous, and UI-driven state.
- RxJS Observables are best for asynchronous data streams, events, and complex reactive flows.
- Signals simplify state management and reduce boilerplate for UI reactivity.
- Observables provide powerful operators for complex async and event-based logic.


# What are Angular Signals and why were they introduced?

**Answer:**

Angular Signals are a reactive primitive introduced in Angular to manage and track state changes in a more predictable and efficient way. Signals allow you to create reactive values that automatically update any consumers when their value changes, similar to observables but with a simpler and more direct API.

**Why were they introduced?**

Signals were introduced to address the limitations of Angular's traditional change detection mechanism, which relies on zone.js and can be inefficient for large or complex applications. With signals, Angular can perform fine-grained reactivity, updating only the parts of the UI that depend on changed values. This leads to better performance, easier state management, and a more modern reactive programming model.

## What is the difference between signal(), computed(), and effect()?

**Answer:**

- **signal()**: Creates a reactive value (signal) that holds state. You can read its value by calling it as a function (e.g., `count()`) and update it using `.set()` or `.update()`. Signals are the basic building blocks for reactive state in Angular.

- **computed()**: Creates a derived (computed) signal whose value is automatically recalculated whenever its dependent signals change. It is used for values that are based on other signals, ensuring the derived value is always up to date.

- **effect()**: Registers a side-effectful function that runs automatically whenever any of its dependent signals change. Use `effect()` to perform actions (like logging, API calls, or DOM updates) in response to signal changes, but not to produce new values.

**Summary Table:**

| Function      | Purpose                                 | Usage Example                  |
|--------------|-----------------------------------------|-------------------------------|
| signal()     | Holds and updates reactive state         | `const count = signal(0);`     |
| computed()   | Derives value from other signals         | `const double = computed(() => count() * 2);` |
| effect()     | Runs side effects on signal changes      | `effect(() => { console.log(count()); });` |


## How do you read and write signal values?

**Answer:**

To **read** a signal's value, call the signal as a function:

```typescript
const value = count(); // Reads the current value of the signal
```

To **write** (update) a signal's value, use the `.set()` or `.update()` methods:

- **set(newValue):** Directly assigns a new value to the signal.

	```typescript
	count.set(5); // Sets the signal value to 5
	```

- **update(fn):** Updates the signal’s value based on its current value by applying a function.

	```typescript
	count.update(v => v + 1); // Increments the current value by 1
	```

**Summary:**
- Read: `signal()`
- Write: `signal.set(newValue)` or `signal.update(fn)`


## What is the role of computed() and when is it recalculated?

**Answer:**

The `computed()` function in Angular creates a derived signal whose value is automatically calculated based on one or more other signals. Its main role is to keep a value in sync with its dependencies, so you never have to manually update it when the underlying signals change.

**When is it recalculated?**

A computed signal is recalculated automatically whenever any of the signals it depends on change. Angular tracks these dependencies, and only recomputes the value when necessary, ensuring efficient and up-to-date derived state.

**Example:**

```typescript
const count = signal(2);
const double = computed(() => count() * 2);
// double() will always return twice the current value of count
```

**Summary:**
- Use `computed()` to derive values from other signals.
- Recalculation happens automatically and only when dependencies change.


## What is the default equality check in signals and how can you customize it?

**Answer:**

By default, Angular signals use strict equality (`===`) to determine if a signal's value has changed. This means the signal will only notify dependents and trigger updates if the new value is not strictly equal to the previous value.

**Customizing the equality check:**
You can customize the equality check by passing an `equal` function as an option when creating a signal. This function receives the old and new values and should return `true` if they are considered equal (no update), or `false` if they are different (trigger update).

**Example:**

```typescript
const deepEqual = (a, b) => JSON.stringify(a) === JSON.stringify(b);
const mySignal = signal({ foo: 1 }, { equal: deepEqual });
```

In this example, the signal uses deep equality for objects, so updates only occur if the object structure actually changes.

**Summary:**
- Default: strict equality (`===`)
- Custom: provide an `equal` function when creating the signal

## How does change detection differ when using signals versus zone.js?

**Answer:**

When using **zone.js** (the traditional Angular approach), change detection is triggered globally for the entire component tree whenever any asynchronous event occurs (like user input, HTTP requests, timers, etc.). This can lead to unnecessary checks and updates across many components, even if only a small part of the state has changed.

With **signals**, Angular enables fine-grained reactivity. Change detection is only triggered for components and templates that directly depend on the changed signal. This means updates are more targeted and efficient, reducing unnecessary work and improving performance, especially in large applications.

**Summary:**
- **zone.js:** Triggers global change detection for most async events, updating many components.
- **signals:** Triggers change detection only for affected consumers, enabling more efficient and predictable updates.



# What is toSignal() and toObservable(), and when would you use them?

**Q: What is `toSignal()`?**

**A:**
`toSignal()` is a utility function in Angular that converts an RxJS Observable into a Signal. This allows you to bridge the world of Observables (asynchronous streams) and Signals (synchronous, fine-grained reactivity). When you use `toSignal(observable, { initialValue })`, the resulting Signal will always reflect the latest value emitted by the Observable.

**When to use `toSignal()`:**
- When you have an Observable (e.g., from HTTP, RxJS, or Angular services) and want to use its latest value reactively in your component or template as a Signal.
- To integrate async data streams into the Signals-based reactivity model.

**Example:**
```typescript
import { toSignal } from '@angular/core';
import { Observable } from 'rxjs';

const obs$: Observable<number> = ...;
const value = toSignal(obs$, { initialValue: 0 });
```

---

**Q: What is `toObservable()`?**

**A:**
`toObservable()` is a utility function that converts a Signal into an RxJS Observable. This is useful when you want to expose a Signal's value to APIs or libraries that expect Observables, or when you need to use RxJS operators on a Signal's value.

**When to use `toObservable()`:**
- When you have a Signal and need to interoperate with code that expects an Observable (e.g., Angular async pipes, RxJS operators, or third-party libraries).
- To bridge Signals-based state into the Observable ecosystem.

**Example:**
```typescript
import { toObservable } from '@angular/core';

const count = signal(0);
const count$ = toObservable(count);
```

---

**Summary Table:**

| Function        | Converts           | Use Case                                                      |
|-----------------|--------------------|---------------------------------------------------------------|
| `toSignal()`    | Observable → Signal| Use Observable data as a Signal in components/templates       |
| `toObservable()`| Signal → Observable| Use Signal data in Observable-based APIs or with RxJS         |

**When to use each:**
- Use `toSignal()` when you want to consume Observable data reactively as a Signal.
- Use `toObservable()` when you need to expose Signal data to Observable consumers or use RxJS features.

# How do signals interact with OnPush change detection strategy?

**Q: How do signals interact with the OnPush change detection strategy in Angular?**

**A:**
Signals work seamlessly with Angular's OnPush change detection strategy. When you use OnPush, Angular only checks a component for updates when its inputs change, an event is triggered, or when you manually mark it for check. However, signals provide fine-grained reactivity: when a signal's value changes and that signal is used in a component's template or logic, Angular automatically marks the component for check—even with OnPush enabled.

**Key Points:**
- Signals trigger updates only for components that depend on them, not the entire component tree.
- You do not need to manually call `ChangeDetectorRef.markForCheck()` when using signals in templates; Angular handles this automatically.
- This leads to more efficient rendering and better performance, especially in large applications.

**Example:**
```typescript
@Component({
	selector: 'app-demo',
	template: `Count: {{ count() }}`,
	changeDetection: ChangeDetectionStrategy.OnPush
})
export class DemoComponent {
	count = signal(0);
	// When count.set() is called, the component updates automatically
}
```

**Summary:**
- Signals and OnPush work together to provide highly efficient, targeted updates in Angular apps.


# What are the cleanup mechanics of effect() and how do you avoid memory leaks?

**Q: What are the cleanup mechanics of `effect()` and how do you avoid memory leaks?**

**A:**
The `effect()` function in Angular allows you to register a cleanup callback to release resources or unsubscribe from side effects when the effect is re-executed or destroyed. This is similar to the cleanup function in RxJS's `useEffect` or Angular's `ngOnDestroy`.

**How cleanup works:**
- Inside the `effect()` callback, you can return a function. This returned function is called automatically before the effect re-runs (due to dependency changes) or when the effect is destroyed (e.g., when the component is destroyed).
- Use this cleanup function to unsubscribe from observables, remove event listeners, or clean up any resources allocated in the effect.

**Example:**
```typescript
effect(() => {
	const subscription = someObservable.subscribe(...);
	return () => {
		subscription.unsubscribe(); // Cleanup
	};
});
```

**How to avoid memory leaks:**
- Always return a cleanup function from `effect()` when you create subscriptions, event listeners, or allocate resources.
- For effects inside Angular components, cleanup is automatic when the component is destroyed.
- Avoid creating long-lived effects outside of component or service lifecycles unless you manage their cleanup manually.

**Summary:**
- Use the return value of the `effect()` callback for cleanup logic.
- This ensures resources are released and prevents memory leaks in Angular applications.

# What is untracked() and when would you use it?

**Q: What is `untracked()` in Angular signals and when would you use it?**

**A:**
`untracked()` is a utility function provided by Angular's signals API that allows you to read the value of a signal without establishing a reactive dependency. Normally, when you access a signal inside a `computed()` or `effect()`, Angular tracks that access and will re-run the computation or effect whenever the signal changes. By wrapping the access in `untracked()`, you tell Angular not to track that signal as a dependency for the current computation or effect.

**When to use `untracked()`:**
- When you want to read a signal's value inside a `computed()` or `effect()` but do NOT want changes to that signal to trigger recomputation or re-execution.
- Useful for reading values for logging, debugging, or for one-off logic where reactivity is not desired.

**Example:**
```typescript
import { computed, signal, untracked } from '@angular/core';

const count = signal(0);
const double = computed(() => {
	const current = untracked(count); // Not tracked as a dependency
	return current * 2;
});
```
In this example, `double` will not update when `count` changes, because the access is untracked.

**Summary:**
- Use `untracked()` to read a signal's value without making it a dependency of the current reactive context.
- This gives you fine-grained control over reactivity and can help avoid unnecessary updates.

# Advanced Angular Signals Q&A

## How would you implement a signal-based service for shared state?
Create a service with private writable signals for state, expose readonly signals (via asReadonly or computed), and provide methods to update state. Inject the service wherever shared state is needed.

**Example:**
```typescript
@Injectable({ providedIn: 'root' })
export class CounterService {
	private _count = signal(0);
	count = this._count.asReadonly();

	increment() { this._count.update(v => v + 1); }
	reset() { this._count.set(0); }
}
```

---

## What is the difference between asReadonly() and computed() for exposing signals?
- `asReadonly()` returns a readonly view of the original signal (no updates allowed, but value is always in sync).
- `computed()` creates a new signal derived from the original, which can transform or filter the value.

Use `asReadonly()` to prevent external mutation; use `computed()` to expose a transformed or derived value.

---

## How do you handle async data (like HTTP) with signals?
Use `toSignal()` to convert an Observable (e.g., from HttpClient) into a signal. This allows you to use async data reactively in your component or template.

**Example:**
```typescript
value = toSignal(this.http.get('/api/data'), { initialValue: null });
```

---

## Can signals replace NgRx or other state management libraries?
Signals can replace simple state management needs, especially for local or shared state. For large-scale, complex, or cross-cutting state (with effects, middleware, devtools, etc.), libraries like NgRx may still be preferable.

---

## Explain the glitch-free (consistent) update semantics of Angular signals.
Angular signals guarantee that all computed signals and effects see a consistent state during updates. When multiple signals change, all computations are re-evaluated in topological order, so no intermediate or inconsistent values are observed—this is called “glitch-free” reactivity.

---

## How does Angular's signal graph handle diamond dependency problems?
Angular’s signal graph ensures that each computed/effect is only re-evaluated once per update, even if it’s reached via multiple paths (the “diamond problem”). This prevents redundant computations and ensures consistency.

---

## What is the allowSignalWrites option in effect() and when is it needed?
`allowSignalWrites: true` allows you to update signals inside an effect. By default, effects cannot write to signals they depend on (to prevent infinite loops). Use this option only when you intentionally want to update signals in response to other signals.

---

## How do signals work with Angular's new defer blocks (@defer)?
Signals can be used inside `@defer` blocks to provide reactive data. When the block is activated, it will render with the current signal values and update as those signals change.

---

## How would you implement an undo/redo feature using signals?
Keep a history stack of previous signal values. On each change, push the old value to the stack. Undo pops from the stack and sets the signal to the previous value. Redo can be implemented with a forward stack.

---

## What are the implications of using signals in a zoneless Angular application?
Signals enable fine-grained, explicit reactivity without relying on zone.js. In zoneless apps, signals ensure UI updates happen only when needed, improving performance and predictability. You must trigger updates manually for non-signal state.



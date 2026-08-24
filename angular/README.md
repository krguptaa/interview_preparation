# Angular Interview Questions & Answers for 10+ Years Experience

> Senior-level Angular interview preparation covering fundamentals, architecture, modern Angular, performance, RxJS, dependency injection, routing, forms, testing, security, and real-world scenarios.

**Source reviewed:** The original interview material covered Angular fundamentals, Angular vs AngularJS/React/Vue, npm, Angular CLI, package files, components, modules, application bootstrap, data binding, and directives. The source was also partially incomplete at the end, so this README preserves those topics and expands them with senior-level questions and practical examples. fileciteturn0file0L5-L13

---

# 1. Angular Framework Fundamentals and Architecture

## 1.1 What is Angular?

### Answer

**Angular** is a TypeScript-based, component-oriented web application framework maintained by Google. It provides an integrated platform for building scalable applications, including routing, dependency injection, forms, HTTP communication, testing, build tooling, and server-side rendering.

Angular is particularly suitable for large enterprise applications because it provides strong conventions and a complete application architecture rather than only a UI layer.

### Example

For an enterprise CRM application:

```text
Angular Application
│
├── Authentication
├── Dashboard
├── Customer Management
├── Reports
├── Task Management
├── Shared Components
├── API Services
└── Routing
```

Angular can provide the structure for all of these areas using components, services, routes, dependency injection, forms, and HTTP APIs.

### Senior-Level Answer

> "I use Angular when I need a structured and maintainable frontend architecture for a medium-to-large application. Its component model, dependency injection, routing, forms, RxJS integration, CLI, and strong TypeScript support make it suitable for enterprise applications. For a senior-level implementation, I also focus on standalone components, signals, lazy loading, OnPush-compatible design, testing, security, and performance."

---

## 1.2 What are the advantages of Angular?

### Answer

Key advantages include:

- Component-based architecture
- TypeScript support
- Dependency Injection
- Strong CLI and build tooling
- Routing
- Reactive and template-driven forms
- RxJS integration
- Signals and modern reactive state management
- Standalone components
- Lazy loading
- Server-side rendering and hydration
- Built-in testing support
- Strong ecosystem and long-term maintainability

### Practical Example

Instead of putting all logic into one component:

```text
CustomerComponent
    |
    +-- CustomerService
    |
    +-- CustomerFormComponent
    |
    +-- CustomerListComponent
    |
    +-- CustomerDetailsComponent
```

Each component has a focused responsibility.

### Senior-Level Perspective

The biggest advantage in an enterprise application is not simply that Angular is "easy." The important advantage is **consistency and maintainability across a large team**.

---

## 1.3 What are the main features of Angular?

### Answer

Important Angular features include:

1. Component-based architecture
2. Dependency Injection
3. Data binding
4. Routing
5. Signals
6. Services
7. Angular CLI
8. Testing
9. Standalone components
10. Lazy loading
11. RxJS
12. HttpClient
13. Angular Forms
14. Server-side rendering
15. Hydration
16. Built-in control flow
17. Modern change detection

Angular's current documentation highlights components, Signals, SSR/SSG, dependency injection, routing, forms, CLI, and DevTools as core parts of the framework. citeturn0search5

---

## 1.4 What is the difference between Angular and AngularJS?

| Angular | AngularJS |
|---|---|
| Modern TypeScript-first framework | Original JavaScript framework |
| Component-based architecture | Controller/directive-based architecture |
| Angular CLI | No equivalent modern Angular CLI |
| Modern Dependency Injection | Dependency Injection also existed in AngularJS |
| Supports modern routing and build tooling | Older architecture |
| Supports standalone components | Does not |
| Supports Signals | Does not |
| Angular is a complete rewrite | Original framework |

### Important Correction

It is incorrect to say that AngularJS did not have Dependency Injection. **AngularJS had Dependency Injection**, and it was one of its important features.

### Migration Example

Legacy application:

```text
AngularJS
  |
  +-- Controllers
  +-- $scope
  +-- Directives
```

Modern Angular:

```text
Angular
  |
  +-- Components
  +-- Services
  +-- Signals
  +-- RxJS
  +-- Dependency Injection
```

### Senior-Level Question

**How would you migrate an AngularJS application to Angular?**

A good answer should mention:

- Inventory existing modules and dependencies
- Identify high-risk legacy components
- Establish automated tests
- Upgrade incrementally where possible
- Separate business logic from UI
- Replace `$scope` patterns with component state
- Replace AngularJS services with Angular services
- Migrate routing
- Introduce TypeScript types
- Migrate toward standalone components
- Run regression and performance testing

---

# 2. Angular vs React vs Vue

## 2.1 Angular vs React

### Answer

Angular and React both build modern web applications, but they have different philosophies.

**Angular** is a full-featured framework with integrated solutions for:

- Routing
- Dependency Injection
- Forms
- HTTP
- Application architecture
- Testing
- Build tooling

**React** is primarily a UI library, so applications commonly select additional libraries for routing, state management, forms, and other concerns.

### Enterprise Example

For a large organization with several teams:

```text
Angular
   |
   +-- Standard architecture
   +-- Standard DI
   +-- Standard Router
   +-- Standard Forms
   +-- Standard CLI
```

This can reduce architectural differences between teams.

### Senior-Level Answer

> "I would not choose Angular simply because it is faster or better than React. I would evaluate team expertise, application size, architecture requirements, ecosystem, performance requirements, hiring, long-term maintenance, and existing technology. Angular is often attractive for enterprise applications where a consistent, opinionated framework is valuable."

---

## 2.2 Angular vs Vue

Angular and Vue are both component-based technologies, but Angular is generally more opinionated and provides a broader integrated platform.

Vue provides flexibility and a progressive adoption model.

### Decision Example

| Requirement | Possible Choice |
|---|---|
| Large enterprise application | Angular |
| Highly opinionated architecture | Angular |
| Small application | Angular or Vue |
| Existing Vue team | Vue |
| Existing Angular enterprise ecosystem | Angular |

The final decision should be based on project and team requirements rather than framework popularity.

---

# 3. NPM, Node.js and Angular CLI

## 3.1 What is NPM?

### Answer

**NPM (Node Package Manager)** is the package manager commonly used with Node.js projects and Angular applications.

It provides:

- Package installation
- Dependency management
- Script execution
- Version management
- Package publishing

### Example

```bash
npm install
```

Installs dependencies defined in `package.json`.

```bash
npm install rxjs
```

Installs a package.

```bash
npm run build
```

Runs a script defined in `package.json`.

---

## 3.2 What is the `node_modules` folder?

`node_modules` contains installed project dependencies.

Example:

```text
project/
├── src/
├── package.json
├── package-lock.json
└── node_modules/
    ├── @angular/
    ├── rxjs/
    └── typescript/
```

### Interview Tip

Do not commit `node_modules` to Git.

It should normally be listed in `.gitignore`.

---

## 3.3 What is Angular CLI?

Angular CLI is the official command-line tool used to create, develop, build, test, and maintain Angular applications.

### Common Commands

```bash
ng new my-app
ng serve
ng build
ng test
ng generate component customer
ng generate service customer
ng update
```

### Example

```bash
ng generate component customer/customer-list
```

This can generate the component structure and associated files.

---

# 4. package.json vs package-lock.json

## 4.1 What is `package.json`?

`package.json` describes project metadata, scripts, dependencies, and allowed dependency version ranges.

Example:

```json
{
  "scripts": {
    "start": "ng serve",
    "build": "ng build",
    "test": "ng test"
  },
  "dependencies": {
    "@angular/core": "^21.0.0",
    "rxjs": "~7.8.0"
  }
}
```

---

## 4.2 What is `package-lock.json`?

`package-lock.json` records the resolved dependency tree, including exact versions of transitive dependencies.

### Why is it important?

Suppose:

```text
Developer A
    |
    +-- npm install
    |
    +-- Dependency version X

CI Server
    |
    +-- npm ci
    |
    +-- Same locked dependency tree
```

This improves reproducibility.

### Senior-Level Interview Answer

> "`package.json` describes what dependencies the project needs and the version ranges that are acceptable. `package-lock.json` records the exact dependency resolution. In CI/CD I prefer `npm ci` because it installs from the lock file and gives a more reproducible build."

---

## 4.3 What is the difference between `^`, `~`, and an exact version?

Example:

```json
"package-a": "^1.2.3",
"package-b": "~1.2.3",
"package-c": "1.2.3"
```

General behavior:

| Version | Meaning |
|---|---|
| `^1.2.3` | Allows compatible updates within major version 1 |
| `~1.2.3` | Allows patch updates within the 1.2 release line |
| `1.2.3` | Requests exactly 1.2.3 |

Always verify package-manager semantics and peer dependency constraints before upgrading a production application.

---

# 5. Components and Standalone Components

## 5.1 What is an Angular Component?

A component is the fundamental UI building block in Angular.

A component normally contains:

```text
Component
├── TypeScript
├── Template
├── Styles
└── Tests
```

A component is defined using `@Component`.

### Example

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-customer-list',
  templateUrl: './customer-list.html'
})
export class CustomerListComponent {
  customers = [];
}
```

---

## 5.2 What is a Selector and Template?

### Selector

A selector identifies how a component can be used in a template.

```typescript
@Component({
  selector: 'app-customer-list'
})
```

Usage:

```html
<app-customer-list></app-customer-list>
```

### Template

A template defines the UI rendered by the component.

```html
<h2>Customers</h2>

@for (customer of customers; track customer.id) {
  <p>{{ customer.name }}</p>
}
```

---

## 5.3 What are Standalone Components?

Standalone components allow components, directives, and pipes to declare their dependencies directly instead of requiring an NgModule declaration.

Example:

```typescript
@Component({
  selector: 'app-customer',
  standalone: true,
  imports: [CustomerListComponent],
  template: `
    <app-customer-list />
  `
})
export class CustomerComponent {}
```

Modern Angular applications can use standalone APIs as the primary architecture. Angular also provides migration tooling for converting existing NgModule-based applications incrementally. citeturn0search6turn0search7

### Senior-Level Question

**Would you immediately migrate a large enterprise application from NgModules to standalone?**

A strong answer:

> "Not blindly. I would evaluate the current application, test coverage, dependencies, shared modules, lazy-loaded features, and release risk. I would migrate incrementally feature by feature, validate bundle size and runtime behavior, and keep the migration independently deployable."

---

# 6. NgModule and app.module.ts

## 6.1 What is an NgModule?

An `NgModule` is the traditional Angular mechanism for grouping declarations, imports, providers, and related application configuration.

Example:

```typescript
@NgModule({
  declarations: [
    CustomerComponent
  ],
  imports: [
    CommonModule
  ]
})
export class CustomerModule {}
```

### Important Modern Angular Note

Do not describe `app.module.ts` as mandatory in modern Angular.

Modern Angular supports **standalone application bootstrapping**, so an application can be created without `AppModule`.

---

# 7. How does an Angular Application Start?

## 7.1 Traditional NgModule Bootstrap

A simplified traditional flow is:

```text
index.html
    |
    v
main.ts
    |
    v
AppModule
    |
    v
AppComponent
    |
    v
Application UI
```

---

## 7.2 Modern Standalone Bootstrap

Modern Angular commonly uses:

```text
index.html
    |
    v
main.ts
    |
    v
bootstrapApplication()
    |
    v
Root Component
    |
    v
Application UI
```

Example:

```typescript
bootstrapApplication(AppComponent, appConfig)
  .catch(err => console.error(err));
```

### Senior-Level Interview Point

If the interviewer asks about `AppModule`, explain both architectures:

> "Older Angular applications commonly bootstrap through `AppModule`, while modern Angular applications can bootstrap a standalone root component directly using `bootstrapApplication`. I would be comfortable maintaining both architectures during a migration."

---

# 8. Data Binding

## 8.1 What is Data Binding?

Data binding connects component state with the template.

Angular commonly provides:

1. Interpolation
2. Property binding
3. Event binding
4. Two-way binding
5. Component input/output communication

---

## 8.2 String Interpolation

Interpolation displays a value in a template.

```typescript
customerName = 'John';
```

```html
<h2>{{ customerName }}</h2>
```

### Important Correction

It is not accurate to say interpolation works only with strings. Angular evaluates the expression and renders the resulting value as text.

---

## 8.3 Property Binding

Property binding binds a template expression to a DOM or component property.

```typescript
isDisabled = true;
```

```html
<button [disabled]="isDisabled">
  Save
</button>
```

Property binding is useful for booleans, numbers, objects, arrays, and other values.

---

## 8.4 Event Binding

Event binding handles events from the template.

```html
<button (click)="saveCustomer()">
  Save
</button>
```

```typescript
saveCustomer() {
  console.log('Customer saved');
}
```

---

## 8.5 Two-Way Binding

Two-way binding combines property and event binding.

```html
<input [(ngModel)]="customerName">
```

Conceptually:

```text
[(ngModel)]
      =
[property] + (event)
```

For enterprise applications, reactive forms are often preferred for complex validation and dynamic forms.

---

# 9. Input and Output Communication

## 9.1 How do parent and child components communicate?

### Parent -> Child

Use an input.

Modern Angular supports signal-based inputs as well as the traditional `@Input()` API.

Example:

```typescript
@Component({
  selector: 'app-customer',
  template: `{{ name }}`
})
export class CustomerComponent {
  name = input.required<string>();
}
```

Parent:

```html
<app-customer [name]="customerName" />
```

---

## 9.2 Child -> Parent

Use an output.

Example:

```typescript
@Component({
  selector: 'app-customer',
  template: `
    <button (click)="selectCustomer()">
      Select
    </button>
  `
})
export class CustomerComponent {
  selected = output<number>();

  selectCustomer() {
    this.selected.emit(1001);
  }
}
```

Parent:

```html
<app-customer (selected)="onCustomerSelected($event)" />
```

### Practical Example

```text
CustomerList
      |
      | customerId
      v
CustomerCard
      |
      | selected event
      v
CustomerList
```

### Senior-Level Rule

Use:

- Inputs/outputs for local component communication
- Services/signals for shared application state
- Route parameters for URL-driven state
- RxJS for asynchronous streams and event pipelines

Avoid putting every piece of state into a global store.

---

# 10. Directives

## 10.1 What are Directives?

Directives are classes that add behavior to elements or components.

The main categories are:

1. Components
2. Attribute directives
3. Structural/control-flow mechanisms

A component is technically a specialized directive with a template. Angular's component documentation describes components as the most basic UI building blocks and a subset of directives. citeturn0search12

---

## 10.2 Attribute Directive

An attribute directive changes the behavior or appearance of an existing element.

Example:

```typescript
@Directive({
  selector: '[appHighlight]'
})
export class HighlightDirective {
  constructor(private el: ElementRef) {
    this.el.nativeElement.style.fontWeight = 'bold';
  }
}
```

Usage:

```html
<p appHighlight>Important Customer</p>
```

---

## 10.3 Structural Directives and Modern Control Flow

Traditional Angular applications commonly use:

```html
<div *ngIf="isLoggedIn">
  Welcome
</div>
```

```html
<div *ngFor="let customer of customers">
  {{ customer.name }}
</div>
```

Modern Angular provides built-in control flow:

```html
@if (isLoggedIn) {
  <div>Welcome</div>
}

@for (customer of customers; track customer.id) {
  <div>{{ customer.name }}</div>
}
```

Built-in control flow reduces the need for imports such as `CommonModule` for these template features. citeturn0search6

---

# 11. Dependency Injection

## 11.1 What is Dependency Injection?

Dependency Injection (DI) is a design pattern where Angular provides required dependencies instead of a class creating them directly.

### Without DI

```typescript
class CustomerComponent {
  customerService = new CustomerService();
}
```

This creates tight coupling.

### With DI

```typescript
@Injectable({
  providedIn: 'root'
})
export class CustomerService {}
```

```typescript
@Component({...})
export class CustomerComponent {
  private customerService = inject(CustomerService);
}
```

### Benefits

- Loose coupling
- Better testing
- Reusability
- Centralized configuration
- Replaceable implementations

---

# 12. What are Angular Service Provider Scopes?

Angular has hierarchical dependency injection.

A service can be provided at different levels, such as:

```text
Application
   |
   +-- Root Injector
   |
   +-- Route Injector
   |
   +-- Component Injector
```

### Root Provider

```typescript
@Injectable({
  providedIn: 'root'
})
export class AuthService {}
```

Usually one application-level instance is created.

### Component Provider

```typescript
@Component({
  providers: [CustomerStateService]
})
```

This creates a service instance associated with that component's injector hierarchy.

### Senior-Level Example

If a feature requires isolated state:

```text
Customer Page
   |
   +-- CustomerStateService
```

Providing the state service at the feature/component level can prevent unrelated screens from sharing the same state instance.

---

# 13. What is the `inject()` function?

Modern Angular allows dependencies to be obtained using `inject()`.

```typescript
export class CustomerComponent {
  private router = inject(Router);
  private customerService = inject(CustomerService);
}
```

It can reduce constructor boilerplate and can be used in supported injection contexts.

### Senior-Level Point

`inject()` does not replace Dependency Injection. It is another API for accessing the Angular DI system.

---

# 14. What are Angular Signals?

## 14.1 What is a Signal?

A Signal is a reactive wrapper around a value.

Example:

```typescript
import { signal, computed } from '@angular/core';

count = signal(0);

doubleCount = computed(() => this.count() * 2);

increment() {
  this.count.update(value => value + 1);
}
```

Template:

```html
<p>Count: {{ count() }}</p>
<p>Double: {{ doubleCount() }}</p>
```

Angular tracks where signals are read and reacts when their values change. citeturn0search2turn0search16

---

## 14.2 Signal vs Observable

| Signal | Observable |
|---|---|
| Represents reactive state | Represents asynchronous/event streams |
| Synchronous reads | Usually consumed asynchronously |
| Fine-grained UI reactivity | Powerful stream operators |
| `signal()` | `Observable` |
| `computed()` | `map()`, `combineLatest()`, etc. |
| `effect()` | `subscribe()` |

### Practical Example

Use Signals for:

```text
UI State
- selected customer
- loading state
- filter value
- current tab
```

Use RxJS for:

```text
Async/Event Streams
- HTTP streams
- WebSocket events
- search debounce
- retry logic
- stream combination
```

### Senior-Level Answer

> "I don't treat Signals and RxJS as competitors. Signals are excellent for application and UI state, while RxJS is excellent for asynchronous streams and event composition. In a real application I may use both and bridge between them when appropriate."

---

# 15. What is Change Detection?

### Answer

Change detection is Angular's mechanism for determining when template bindings need to be updated.

A simplified model is:

```text
Application State
       |
       v
Change Detection
       |
       v
Template Evaluation
       |
       v
DOM Update
```

For large applications, change detection strategy has a major impact on performance.

---

# 16. What is OnPush Change Detection?

`OnPush` limits unnecessary checking of component subtrees and is a key performance technique.

Example:

```typescript
@Component({
  changeDetection: ChangeDetectionStrategy.OnPush
})
export class CustomerComponent {}
```

A senior developer should understand that OnPush works best when application state is updated immutably or through Angular's supported reactive notification mechanisms.

### Example

Prefer:

```typescript
this.customer = {
  ...this.customer,
  name: 'New Name'
};
```

over mutating a shared object:

```typescript
this.customer.name = 'New Name';
```

Angular's modern documentation emphasizes OnPush-compatible components as an important step toward zoneless applications. citeturn0search1

---

# 17. What is Zoneless Angular?

Modern Angular supports change detection without relying on ZoneJS.

Zoneless change detection is stable and is the default in Angular v21+ according to the Angular documentation. citeturn0search0turn0search1

### Why is Zoneless Useful?

- Less runtime overhead
- Better performance potential
- Smaller dependency surface
- More predictable change-detection triggers
- Better debugging in some scenarios

### Example

A signal update can notify Angular that a template needs synchronization:

```typescript
loading = signal(false);

loadData() {
  this.loading.set(true);
}
```

Template:

```html
@if (loading()) {
  <app-spinner />
}
```

### Senior-Level Question

**Does Zoneless mean Angular no longer has change detection?**

No.

Zoneless means Angular does not depend on ZoneJS to determine when to schedule synchronization. Angular still performs the necessary rendering/change-detection work based on supported notifications.

---

# 18. What is RxJS and why is it used in Angular?

RxJS is a reactive programming library based on Observables.

Angular uses RxJS extensively for asynchronous and event-based programming.

### Example

```typescript
customers$ = this.http.get<Customer[]>('/api/customers');
```

Template:

```html
@for (customer of customers$ | async; track customer.id) {
  <div>{{ customer.name }}</div>
}
```

### Common Operators

```text
map
filter
switchMap
mergeMap
concatMap
exhaustMap
debounceTime
distinctUntilChanged
catchError
retry
shareReplay
combineLatest
forkJoin
```

---

# 19. switchMap vs mergeMap vs concatMap vs exhaustMap

This is a common senior-level interview question.

| Operator | Behavior | Typical Use |
|---|---|---|
| `switchMap` | Cancels previous inner stream | Search/autocomplete |
| `mergeMap` | Runs inner streams concurrently | Independent requests |
| `concatMap` | Processes sequentially | Ordered operations |
| `exhaustMap` | Ignores new values while current is active | Prevent duplicate submits |

### Example: Search

```typescript
searchTerm$
  .pipe(
    debounceTime(300),
    distinctUntilChanged(),
    switchMap(term => this.searchService.search(term))
  );
```

Why `switchMap`?

If the user enters:

```text
A
An
Ang
Angu
Angular
```

Older requests are no longer relevant. `switchMap` switches to the latest request.

---

# 20. What is the AsyncPipe?

The `async` pipe subscribes to an Observable or Promise and exposes its latest value to the template.

Example:

```html
@if (customers$ | async; as customers) {
  @for (customer of customers; track customer.id) {
    <p>{{ customer.name }}</p>
  }
}
```

### Benefits

- Reduces manual subscription code
- Helps manage subscription lifecycle
- Integrates with Angular change detection

---

# 21. How do you prevent RxJS memory leaks?

### Problem

Manual subscriptions can remain active after a component is destroyed.

```typescript
this.service.getCustomers()
  .subscribe(data => {
    this.customers = data;
  });
```

### Better Approaches

Use:

```html
| async
```

or Angular's modern subscription cleanup mechanisms such as:

```typescript
this.service.getCustomers()
  .pipe(takeUntilDestroyed())
  .subscribe();
```

### Senior-Level Answer

> "I first avoid manual subscriptions when the template can consume an Observable using AsyncPipe. For imperative subscriptions, I use lifecycle-aware cleanup such as `takeUntilDestroyed()` rather than maintaining custom Subject-based cleanup everywhere."

---

# 22. What is Angular Routing?

Angular Router provides client-side navigation between application views.

Example:

```typescript
export const routes: Routes = [
  {
    path: 'customers',
    component: CustomerListComponent
  },
  {
    path: 'reports',
    component: ReportsComponent
  }
];
```

Navigation:

```typescript
this.router.navigate(['/customers']);
```

---

# 23. What is Lazy Loading?

Lazy loading loads a feature only when it is required.

Example:

```typescript
{
  path: 'reports',
  loadComponent: () =>
    import('./reports/reports.component')
      .then(m => m.ReportsComponent)
}
```

### Architecture

```text
Initial Bundle
    |
    +-- Login
    +-- Dashboard

Lazy Chunk
    |
    +-- Reports
    +-- Analytics
```

This can reduce the initial JavaScript payload.

Angular documentation specifically recommends lazy loading for appropriate non-primary routes because it can reduce the initial bundle size. citeturn0search9turn0search15

---

# 24. What are Route Guards?

Route guards control navigation based on application conditions.

Examples:

- Authentication
- Authorization
- Unsaved changes
- Feature flags

Example:

```typescript
export const authGuard: CanActivateFn = () => {
  const auth = inject(AuthService);
  return auth.isLoggedIn();
};
```

Route:

```typescript
{
  path: 'admin',
  canActivate: [authGuard],
  loadComponent: () => import('./admin.component')
}
```

### Senior-Level Point

A frontend route guard should **not** be treated as the application's security boundary. Backend APIs must independently enforce authorization.

---

# 25. What is an HTTP Interceptor?

An interceptor can observe or modify HTTP requests and responses.

Common uses:

- Authentication tokens
- Logging
- Error handling
- Retry
- Correlation IDs
- Loading indicators

Example:

```typescript
export const authInterceptor: HttpInterceptorFn = (req, next) => {
  const token = inject(AuthService).token();

  const request = req.clone({
    setHeaders: {
      Authorization: `Bearer ${token}`
    }
  });

  return next(request);
};
```

### Architecture

```text
Component
   |
   v
Service
   |
   v
HttpClient
   |
   v
Interceptor
   |
   v
Backend API
```

---

# 26. Reactive Forms vs Template-Driven Forms

## Reactive Forms

Reactive forms define form structure and validation in TypeScript.

Example:

```typescript
form = new FormGroup({
  name: new FormControl('', Validators.required),
  email: new FormControl('', [
    Validators.required,
    Validators.email
  ])
});
```

Template:

```html
<form [formGroup]="form">
  <input formControlName="name">
  <input formControlName="email">
</form>
```

### Advantages

- Better for complex forms
- Dynamic forms
- Testability
- Programmatic validation
- Stronger separation of concerns

---

## Template-Driven Forms

Example:

```html
<input
  name="email"
  [(ngModel)]="email"
  required
>
```

Better suited to simpler forms.

### Senior-Level Answer

> "For enterprise applications with complex validation, dynamic fields, conditional sections, and extensive testing, I generally prefer reactive forms. Template-driven forms are still useful for smaller and simpler forms."

---

# 27. What is Lazy Loading vs Preloading?

### Lazy Loading

Load the feature only when the user navigates to it.

### Preloading

Load the feature in the background after the application starts.

Example:

```text
Application Starts
      |
      +-- Dashboard loads immediately
      |
      +-- Reports preloads in background
```

### Decision

Use lazy loading for:

- Large features
- Rarely used modules
- Admin functionality

Consider preloading when:

- The feature is likely to be visited soon
- Network conditions permit it
- User experience benefits from faster subsequent navigation

---

# 28. What is AOT Compilation?

**Ahead-of-Time (AOT)** compilation compiles Angular templates and application code during the build process rather than waiting until runtime.

Benefits include:

- Faster application startup
- Smaller runtime compilation overhead
- Earlier template errors
- Better production optimization

### Production Flow

```text
TypeScript
   |
   v
Angular Compiler
   |
   v
Optimized JavaScript
   |
   v
Browser
```

---

# 29. How do you improve Angular application performance?

This is an important **10+ years interview question**.

### Answer

I would investigate performance systematically rather than immediately changing code.

### Areas I would check

#### 1. Bundle Size

- Lazy-load large features
- Remove unused dependencies
- Analyze production bundles
- Avoid importing unnecessarily large libraries

#### 2. Change Detection

- Use OnPush-compatible components
- Prefer immutable state updates
- Use Signals where appropriate
- Avoid expensive template expressions

#### 3. Rendering

Use tracking with lists:

```html
@for (customer of customers; track customer.id) {
  <app-customer [customer]="customer" />
}
```

#### 4. HTTP

- Cache appropriate data
- Avoid duplicate API requests
- Use pagination
- Use debounce for search
- Cancel obsolete requests

#### 5. Images

- Optimize image sizes
- Use modern image formats
- Lazy-load images where appropriate

#### 6. Architecture

```text
Shell
 |
 +-- Lazy Feature 1
 +-- Lazy Feature 2
 +-- Lazy Feature 3
```

### Senior-Level Answer

> "I measure first using browser performance tools, Angular DevTools, bundle analysis, network timing, and real-user metrics. Then I identify whether the bottleneck is JavaScript execution, change detection, rendering, network latency, API performance, or bundle size. I optimize the actual bottleneck rather than applying generic Angular optimizations."

---

# 30. How would you design a large Angular enterprise application?

### Example Architecture

```text
src/app
│
├── core/
│   ├── auth/
│   ├── interceptors/
│   ├── guards/
│   └── services/
│
├── shared/
│   ├── components/
│   ├── directives/
│   ├── pipes/
│   └── utilities/
│
├── features/
│   ├── customers/
│   ├── tasks/
│   ├── reports/
│   └── administration/
│
├── layout/
│   ├── header/
│   ├── sidebar/
│   └── footer/
│
└── app.routes.ts
```

### Principles

- Organize by business feature
- Keep shared code truly reusable
- Avoid a huge `shared` dumping ground
- Keep core infrastructure separate
- Lazy-load large features
- Keep components focused
- Put business logic in services/state layers
- Use typed APIs
- Establish consistent error handling
- Add unit and integration tests
- Enforce linting and code standards

---

# 31. How would you handle state management in Angular?

### Answer

I would not automatically introduce NgRx or another global state library.

First classify the state.

```text
State
│
├── Local UI State
│      └── Signal
│
├── Component Communication
│      └── Input / Output
│
├── Feature State
│      └── Signals / Service / RxJS
│
├── Server State
│      └── HTTP + caching strategy
│
└── Complex Global State
       └── NgRx or another dedicated solution
```

### Senior-Level Example

For a customer management feature:

```text
CustomerList
     |
     +-- CustomerState
     |      |
     |      +-- customers
     |      +-- selectedCustomer
     |      +-- loading
     |
     +-- CustomerService
            |
            +-- HTTP API
```

The important point is to choose the simplest state solution that meets the application's requirements.

---

# 32. How do you handle API errors globally?

### Approach

Use a consistent error-handling strategy.

```text
Component
   |
   v
Service
   |
   v
HttpClient
   |
   v
Interceptor
   |
   +-- Authentication Error
   +-- Validation Error
   +-- Server Error
   +-- Network Error
```

Example:

```typescript
return this.http.get<Customer[]>('/api/customers')
  .pipe(
    catchError(error => {
      // Log / transform / propagate
      return throwError(() => error);
    })
  );
```

### Senior-Level Point

Do not display raw backend error messages directly to users. Map technical errors to appropriate user-facing messages while preserving detailed diagnostics for logging/monitoring.

---

# 33. How do you secure an Angular application?

### Important Principle

Angular security is only one part of application security.

### Key Areas

- Authentication
- Authorization
- Secure token handling
- HTTPS
- XSS protection
- CSRF protection where applicable
- Content Security Policy
- Input validation
- Secure backend APIs
- Dependency vulnerability scanning
- Avoiding unsafe DOM manipulation

### Critical Interview Point

Never say:

> "Angular route guards secure the application."

Instead:

> "Route guards improve the user experience and prevent unauthorized navigation in the client, but the backend must enforce authorization because frontend code can be modified or bypassed."

---

# 34. What is the difference between Authentication and Authorization?

### Authentication

Answers:

> "Who are you?"

Example:

```text
Username + Password
       |
       v
Identity Provider
       |
       v
Authenticated User
```

### Authorization

Answers:

> "What are you allowed to do?"

Example:

```text
User
 |
 +-- View Customers
 +-- Edit Customers
 -   Delete Customers
```

Angular can hide or disable UI actions based on permissions, but the backend must enforce the actual permissions.

---

# 35. How do you test Angular applications?

### Testing Levels

```text
Unit Tests
   |
   +-- Services
   +-- Components
   +-- Pipes
   +-- Directives

Integration Tests
   |
   +-- Component + Services

End-to-End Tests
   |
   +-- Complete User Journey
```

### Example Service Test

```typescript
it('should return customers', () => {
  service.getCustomers().subscribe(customers => {
    expect(customers.length).toBe(2);
  });

  const request = httpMock.expectOne('/api/customers');

  request.flush([
    { id: 1, name: 'John' },
    { id: 2, name: 'Jane' }
  ]);
});
```

### Modern Angular Testing

Angular's current roadmap identifies Vitest as the primary test runner following its stabilization in Angular v21. citeturn0search18

---

# 36. What are Angular Lifecycle Hooks?

Common lifecycle hooks include:

```text
constructor
ngOnChanges
ngOnInit
ngDoCheck
ngAfterContentInit
ngAfterContentChecked
ngAfterViewInit
ngAfterViewChecked
ngOnDestroy
```

### Practical Usage

Use:

- `constructor` → dependency initialization
- `ngOnInit` → initialization logic
- `ngOnChanges` → react to input changes
- `ngAfterViewInit` → logic requiring initialized view
- `ngOnDestroy` → cleanup

### Senior-Level Warning

Do not put expensive logic into hooks that execute frequently, such as:

```text
ngDoCheck
ngAfterViewChecked
```

---

# 37. What is Content Projection?

Content projection allows a parent component to provide content that a child component renders using `<ng-content>`.

### Child

```html
<div class="card">
  <ng-content></ng-content>
</div>
```

### Parent

```html
<app-card>
  <h2>Customer Details</h2>
  <p>Customer information...</p>
</app-card>
```

This is useful for reusable layout components.

---

# 38. What is the difference between ViewChild and ContentChild?

### `ViewChild`

Accesses something inside the component's own template.

```typescript
@ViewChild(CustomerComponent)
customer!: CustomerComponent;
```

### `ContentChild`

Accesses projected content supplied by the parent.

```typescript
@ContentChild(CustomerComponent)
customer!: CustomerComponent;
```

### Simple Rule

```text
Own Template
    |
    +-- ViewChild

Projected Content
    |
    +-- ContentChild
```

---

# 39. What is SSR and Hydration?

## Server-Side Rendering

SSR renders Angular application content on the server and sends HTML to the browser.

Benefits can include:

- Faster initial content visibility
- Better SEO for appropriate applications
- Improved perceived performance

## Hydration

Hydration allows Angular to reuse the server-rendered DOM rather than rebuilding the entire UI from scratch.

### Flow

```text
Browser Request
      |
      v
Angular Server
      |
      v
HTML Response
      |
      v
Browser
      |
      v
Hydration
      |
      v
Interactive Angular Application
```

---

# 40. Scenario: An Angular application is becoming slow. How would you troubleshoot it?

### Senior-Level Answer

I would follow a measurable troubleshooting process.

### Step 1: Identify the symptom

Is the problem:

- Slow initial load?
- Slow navigation?
- Slow rendering?
- Slow API response?
- Browser CPU usage?
- Memory growth?

### Step 2: Measure

Use:

- Chrome DevTools
- Network tab
- Performance tab
- Angular DevTools
- Bundle analysis
- Application monitoring

### Step 3: Check Frontend

```text
Bundle Size
   |
   +-- Lazy Loading
   +-- Tree Shaking
   +-- Large Dependencies

Rendering
   |
   +-- Change Detection
   +-- Large Lists
   +-- Expensive Templates

API
   |
   +-- Duplicate Calls
   +-- Slow Responses
   +-- Large Payloads
```

### Step 4: Optimize

Examples:

```text
Large Feature
   -> Lazy Load

Large List
   -> Track items / virtual scrolling / pagination

Duplicate Requests
   -> Cache / share result

Search API
   -> debounceTime + switchMap

Unnecessary Rendering
   -> OnPush-compatible design / Signals
```

### Step 5: Verify

Measure the same metric again after the change.

---

# 41. Scenario: How would you migrate an Angular application from an older version to a modern Angular version?

### Answer

I would avoid a large "big bang" migration.

### Migration Strategy

```text
Current Angular Version
        |
        v
Run Tests
        |
        v
Upgrade Incrementally
        |
        v
Fix Breaking Changes
        |
        v
Update Dependencies
        |
        v
Migrate Deprecated APIs
        |
        v
Adopt Standalone
        |
        v
Adopt Signals Where Useful
        |
        v
Performance Testing
        |
        v
Production Release
```

### Senior-Level Considerations

Before migration:

- Check Node.js compatibility
- Check TypeScript compatibility
- Check third-party libraries
- Run the existing test suite
- Create a clean Git branch
- Review deprecated APIs
- Check custom builders and webpack configuration
- Review UI component libraries

After migration:

- Build production bundle
- Run unit tests
- Run integration/E2E tests
- Validate routing
- Validate forms
- Check browser compatibility
- Check bundle size
- Monitor production errors

---

# 42. Scenario: How would you structure a reusable Angular component library?

### Answer

I would separate reusable components from business-specific components.

Example:

```text
UI Library
│
├── Button
├── Modal
├── Table
├── Pagination
├── DatePicker
├── Form Controls
└── Notification
```

Business application:

```text
CRM
│
├── CustomerList
├── CustomerForm
└── CustomerReport
```

The UI library should not depend on CRM-specific business logic.

### Senior-Level Principles

- Clear public APIs
- Strong typing
- Accessibility
- Consistent styling
- Documentation
- Unit tests
- Versioning
- Backward compatibility
- Avoid unnecessary dependencies

---

# 43. Scenario: How would you handle a large data table with 100,000 records?

### Answer

I would **not** load all 100,000 records into the browser.

Instead:

```text
Browser
   |
   | Page 1 / Filter / Sort
   v
Backend API
   |
   v
Database
```

Use:

- Server-side pagination
- Server-side sorting
- Server-side filtering
- Virtual scrolling where appropriate
- Debounced search
- Lightweight row components
- Stable tracking keys
- Cached reference data

### Example API

```text
GET /api/customers?page=1&pageSize=50&search=john
```

The backend returns only the required records.

---

# 44. Scenario: How do you prevent duplicate API requests?

### Possible Causes

- Multiple component subscriptions
- Multiple async pipes
- Repeated navigation
- Repeated event triggers
- Multiple service calls

### Possible Solutions

Use:

- Shared state
- Caching
- `shareReplay` where appropriate
- Signals
- Request deduplication
- Correct component lifecycle management

Example:

```typescript
customers$ = this.http.get<Customer[]>('/api/customers')
  .pipe(
    shareReplay({ bufferSize: 1, refCount: true })
  );
```

Always consider cache invalidation before introducing long-lived caching.

---

# 45. Scenario: How would you handle authentication token expiration?

### Typical Flow

```text
API Request
    |
    v
401 Unauthorized
    |
    v
Interceptor
    |
    v
Refresh Token / Re-authenticate
    |
    v
Retry Request
```

### Senior-Level Considerations

You should handle:

- Multiple simultaneous 401 responses
- Refresh request duplication
- Token rotation
- Logout on refresh failure
- Secure storage strategy
- Redirect behavior
- Race conditions

Avoid blindly retrying every request.

---

# 46. Scenario: How would you handle global application state?

### Answer

First identify whether the state really needs to be global.

Example:

```text
Global
├── Current User
├── Permissions
└── Application Configuration

Feature
├── Customer List
├── Customer Filters
└── Selected Customer

Local
├── Modal Open/Close
├── Input Value
└── Current Tab
```

Use the smallest appropriate state scope.

---

# 47. Senior Angular Interview Questions

For a 10+ years candidate, expect scenario-based questions such as:

1. How would you architect a large Angular application?
2. How would you improve Angular performance?
3. How do Signals compare with RxJS?
4. When would you use NgRx?
5. How would you migrate AngularJS to modern Angular?
6. How would you migrate NgModules to standalone?
7. How would you handle authentication and token refresh?
8. How would you design reusable components?
9. How would you prevent memory leaks?
10. How would you optimize a large data table?
11. How would you handle global API errors?
12. How would you design route-level authorization?
13. How would you debug excessive change detection?
14. How would you reduce initial bundle size?
15. How would you design an Angular application for multiple teams?
16. How would you handle environment configuration?
17. How would you implement SSR and hydration?
18. How would you design unit, integration, and E2E testing?
19. How would you handle a third-party library that is incompatible with Angular's rendering/change-detection model?
20. How would you approach a major Angular version upgrade in a production application?

---

# 48. Quick Angular Interview Revision

| Topic | Key Point |
|---|---|
| Angular | TypeScript-based application framework |
| Component | Basic UI building block |
| Standalone | Components/directives/pipes can declare dependencies directly |
| NgModule | Traditional Angular module system |
| Selector | Identifies component/directive usage |
| Template | Defines component UI |
| DI | Provides dependencies without manually creating them |
| Signal | Reactive state primitive |
| Observable | Reactive asynchronous/event stream |
| Interpolation | Displays evaluated values |
| Property Binding | Component/template -> property |
| Event Binding | Template event -> component |
| Two-way Binding | Combines property and event binding |
| Input | Parent -> child |
| Output | Child -> parent |
| Directive | Adds behavior to elements/components |
| Lazy Loading | Loads feature when needed |
| Guard | Controls route navigation |
| Interceptor | Central HTTP request/response processing |
| AOT | Compile Angular during build |
| OnPush | Reduces unnecessary component checking |
| Zoneless | Change detection without relying on ZoneJS |
| SSR | Render application on server |
| Hydration | Reuse server-rendered DOM on client |
| RxJS | Reactive asynchronous programming |
| AsyncPipe | Consumes Observable/Promise in template |
| Reactive Forms | Programmatic complex form management |
| Vitest | Modern Angular testing direction |

---

# 49. How to Answer Angular Questions as a 10+ Years Experienced Developer

Do not stop at:

> "What is X?"

Use this structure:

```text
1. Definition
       ↓
2. Why it exists
       ↓
3. How it works
       ↓
4. Real-world example
       ↓
5. When to use it
       ↓
6. When NOT to use it
       ↓
7. Performance / security considerations
       ↓
8. Trade-offs
```

### Example: Signals

Weak answer:

> "Signals are used for reactive data."

Strong senior answer:

> "Signals are Angular's reactive state primitive. I would use them for local or feature-level state where fine-grained reactive updates are useful. For example, a customer screen can keep `selectedCustomer`, `loading`, and derived values in signals. I would still use RxJS for asynchronous streams such as HTTP pipelines, WebSockets, debouncing, cancellation, and complex stream composition. The choice is based on the type of state rather than replacing RxJS everywhere."

---

# 50. Final Senior-Level Interview Checklist

Before an Angular 10+ years interview, make sure you can explain these without memorizing definitions:

- [ ] Angular architecture
- [ ] Standalone components
- [ ] NgModules and migration
- [ ] Components and directives
- [ ] Dependency Injection
- [ ] Hierarchical injectors
- [ ] `inject()`
- [ ] Signals
- [ ] RxJS
- [ ] `switchMap`, `mergeMap`, `concatMap`, `exhaustMap`
- [ ] Change detection
- [ ] OnPush
- [ ] Zoneless Angular
- [ ] Lifecycle hooks
- [ ] Inputs and outputs
- [ ] Modern control flow
- [ ] Routing
- [ ] Guards
- [ ] Lazy loading
- [ ] HTTP interceptors
- [ ] Reactive forms
- [ ] SSR and hydration
- [ ] AOT
- [ ] Performance optimization
- [ ] Security
- [ ] Testing
- [ ] State management
- [ ] Enterprise architecture
- [ ] Angular version migration
- [ ] Debugging production issues

---

# References

- Angular documentation: https://angular.dev/
- Angular Signals: https://angular.dev/essentials/signals
- Angular Zoneless: https://angular.dev/guide/zoneless
- Angular Routing: https://angular.dev/guide/routing
- Angular HTTP Client: https://angular.dev/guide/http
- Angular Migrations: https://angular.dev/reference/migrations


Absolutely. For **5+ years Angular experience**, interviewers usually go beyond basic syntax. They focus on **architecture, RxJS, performance, state management, debugging, testing, TypeScript, and real-world problem solving**.

Here is a structured list you can use for preparation.

## 1. Angular Fundamentals

1. What is Angular and how is it different from AngularJS?
2. Explain Angular architecture.
3. What are components, directives, pipes, and services?
4. What is a standalone component?
5. What is an NgModule? Is it still required?
6. Explain Angular component lifecycle hooks.
7. Difference between `constructor()` and `ngOnInit()`.
8. What is `ngOnChanges()` and when is it triggered?
9. Difference between `ngOnInit()` and `ngAfterViewInit()`.
10. What is `ngOnDestroy()` used for?
11. How does Angular detect changes?
12. What is Zone.js?
13. What is Angular's dependency injection system?
14. What is the difference between `providedIn: 'root'` and component-level providers?
15. What is hierarchical dependency injection?
16. How does Angular resolve a dependency?
17. What is `inject()` and how is it different from constructor injection?
18. What are Angular decorators?
19. Difference between `@Component`, `@Directive`, `@Pipe`, and `@Injectable`.
20. What are host elements and host bindings?

---

# 2. Data Binding

21. What are the different types of data binding in Angular?

* Interpolation
* Property binding
* Event binding
* Two-way binding

22. Difference between:

```typescript
[value]="name"
```

and

```typescript
{{ name }}
```

23. How does `[(ngModel)]` work internally?
24. What is property binding vs attribute binding?
25. Difference between:

```html
[attr.disabled]
```

and

```html
[disabled]
```

26. What is event bubbling?
27. How can a child component communicate with its parent?
28. How can a parent communicate with its child?
29. Difference between `@Input()` and `@Output()`.
30. How do you share data between unrelated components?

---

# 3. Change Detection ⭐

This is **very important for 5+ years interviews**.

31. What is change detection?
32. How does Angular's change detection work?
33. What is the difference between:

```typescript
ChangeDetectionStrategy.Default
```

and

```typescript
ChangeDetectionStrategy.OnPush
```

34. When does an `OnPush` component get checked?
35. Does `OnPush` mean Angular completely stops change detection?
36. Why doesn't changing an object property sometimes update an `OnPush` component?

Example:

```typescript
user.name = 'John';
```

37. Why does this work better with `OnPush`?

```typescript
this.user = {
  ...this.user,
  name: 'John'
};
```

38. What is `ChangeDetectorRef`?
39. Difference between:

```typescript
markForCheck()
detectChanges()
```

40. When would you use `detach()`?
41. What causes unnecessary change detection?
42. How would you optimize a component with thousands of DOM elements?

---

# 4. RxJS ⭐⭐⭐

Since you're currently learning RxJS, **spend significant time here**.

43. What is RxJS?
44. What is an Observable?
45. Observable vs Promise.
46. What are cold and hot observables?
47. What is subscription?
48. What happens when you subscribe to an Observable?
49. What is an operator?
50. Difference between:

```typescript
map()
filter()
tap()
```

51. Difference between:

```typescript
switchMap()
mergeMap()
concatMap()
exhaustMap()
```

52. When would you use `switchMap()`?
53. Why is `switchMap()` useful for search/autocomplete?
54. What happens to the previous request when `switchMap()` receives a new value?
55. Difference between `Subject`, `BehaviorSubject`, and `ReplaySubject`.
56. What is `share()`?
57. What is `shareReplay()`?
58. What does this mean?

```typescript
shareReplay(1)
```

59. What does the `1` represent in `shareReplay(1)`?
60. What does "replay the latest value to future subscribers" mean?
61. What is `combineLatest()`?
62. Difference between `combineLatest()` and `forkJoin()`.
63. What is `withLatestFrom()`?
64. Difference between `debounceTime()` and `throttleTime()`.
65. What is `distinctUntilChanged()`?
66. What is `catchError()`?
67. Where should error handling be placed in an RxJS chain?
68. What is `finalize()`?
69. What is `takeUntil()`?
70. How do you prevent memory leaks from subscriptions?
71. What is the `async` pipe?
72. Why is `async` pipe preferred over manually subscribing in many cases?
73. What happens when an Observable emits after a component is destroyed?
74. How would you cancel an HTTP request?
75. How would you implement API caching using RxJS?

---

# 5. RxJS Practical Scenarios ⭐⭐⭐

These are especially common in senior interviews.

### Scenario 1 — Search API

User types:

```text
A
An
Ang
Angu
Angular
```

How would you make sure only the latest search request is processed?

Expected concepts:

```typescript
debounceTime()
distinctUntilChanged()
switchMap()
```

---

### Scenario 2 — Multiple APIs

You need:

```text
User API
Orders API
Products API
```

and need all responses before continuing.

Which operator?

```typescript
forkJoin()
```

---

### Scenario 3 — Sequential APIs

API 2 depends on API 1.

```text
Get User
   ↓
Get User Orders
   ↓
Get Order Details
```

Which operator?

```typescript
switchMap()
```

or potentially `concatMap()` depending on the semantics.

---

### Scenario 4 — Prevent duplicate API calls

How would you cache:

```typescript
getUser(id)
```

using:

```typescript
shareReplay(1)
```

---

# 6. HTTP Client

76. How does Angular `HttpClient` work?
77. Why does `HttpClient.get()` return an Observable?
78. Are HTTP Observables cold or hot?
79. How do you add HTTP headers?
80. How do you handle HTTP errors globally?
81. What is an HTTP interceptor?
82. How would you add JWT authentication using an interceptor?
83. How would you refresh an expired JWT token?
84. How do you prevent multiple refresh-token requests?
85. How do you retry failed HTTP requests?
86. Difference between HTTP `PUT` and `PATCH`.
87. How do you cancel an HTTP request?
88. How do you cache API responses?
89. How would you handle `401`, `403`, `404`, and `500` responses?
90. How do you globally show/hide a loading spinner?

---

# 7. Routing

91. How does Angular routing work?
92. What is lazy loading?
93. Why should we lazy-load modules/routes?
94. What are route guards?
95. Difference between:

```text
CanActivate
CanDeactivate
Resolve
```

96. How do you pass route parameters?
97. Route parameter vs query parameter.
98. How do you implement authentication guards?
99. How do you prevent unauthorized users from accessing a route?
100. What is a route resolver?
101. When should you use a resolver vs fetching data inside `ngOnInit()`?
102. What is preloading strategy?
103. Difference between eager loading and lazy loading.
104. How would you handle unsaved form changes when navigating away?

---

# 8. Forms ⭐⭐

105. Template-driven vs reactive forms.
106. Which one do you prefer for large applications and why?
107. What is `FormControl`?
108. What is `FormGroup`?
109. What is `FormArray`?
110. How do you create dynamic forms?
111. How do you create custom validators?
112. Synchronous vs asynchronous validators.
113. How do you validate two fields against each other?

Example:

```text
password
confirmPassword
```

114. How do you dynamically add/remove form controls?
115. How do you disable/enable controls?
116. Difference between:

```typescript
setValue()
patchValue()
```

117. How do you detect form changes?
118. How do you reset a form?
119. How do you display validation errors efficiently?

---

# 9. Component Communication

120. Parent → Child communication.
121. Child → Parent communication.
122. Communication between sibling components.
123. Communication between unrelated components.
124. Using a shared service for communication.
125. Using `Subject`/`BehaviorSubject`.
126. Using state management.
127. When should you avoid using a shared service?

---

# 10. Directives & Pipes

128. What is a directive?
129. Structural vs attribute directives.
130. How does `*ngIf` work?
131. How does `*ngFor` work?
132. What is the newer Angular control-flow syntax?
133. What is `trackBy`?
134. Why is `trackBy` important for performance?
135. How do you create a custom directive?
136. How do you access the host element from a directive?
137. What is `ElementRef`?
138. Why should direct DOM manipulation generally be avoided?
139. What is `Renderer2`?
140. Pure vs impure pipes.
141. When should you create an impure pipe?
142. Why can impure pipes hurt performance?
143. How do you create a custom pipe?

---

# 11. Performance Optimization ⭐⭐⭐

Very important for experienced developers.

144. How do you improve Angular application performance?
145. What is lazy loading?
146. What is `OnPush`?
147. What is `trackBy`?
148. How do you optimize large lists?
149. What is Angular CDK virtual scrolling?
150. How do you reduce unnecessary API calls?
151. How do you implement API caching?
152. How do you reduce bundle size?
153. What is tree shaking?
154. What is code splitting?
155. How do you identify performance bottlenecks?
156. How would you optimize a page taking 5–10 seconds to load?
157. How would you optimize a table containing 10,000 records?
158. How do you prevent memory leaks?
159. What are common causes of memory leaks in Angular?
160. How would you optimize images/assets?
161. What is lazy loading of images?
162. How do you optimize change detection?

---

# 12. TypeScript ⭐⭐⭐

For 5+ years Angular, don't prepare Angular alone.

163. `interface` vs `type`.
164. `any` vs `unknown`.
165. `never` vs `void`.
166. Union vs intersection types.
167. Generics.
168. Generic constraints.
169. Utility types:

```typescript
Partial
Required
Pick
Omit
Readonly
Record
```

170. What are mapped types?
171. What are conditional types?
172. What is type narrowing?
173. What are type guards?
174. What is `keyof`?
175. What is `typeof` in TypeScript?
176. What is `infer`?
177. Optional properties vs optional parameters.
178. Enum vs union type.
179. Access modifiers.
180. Abstract classes.
181. Method overriding.
182. Method overloading.
183. What is structural typing?
184. What are decorators?

---

# 13. Dependency Injection ⭐⭐

185. What is Dependency Injection?
186. Why does Angular use DI?
187. What is an Angular provider?
188. Difference between:

```typescript
providedIn: 'root'
```

and

```typescript
providers: []
```

189. What is hierarchical injection?
190. What happens when the same service is provided at component level?
191. Singleton service vs multiple service instances.
192. What are injection tokens?
193. What is `InjectionToken`?
194. What is `useClass`?
195. What is `useValue`?
196. What is `useFactory`?
197. What is `useExisting`?

---

# 14. State Management

198. What is state management?
199. When do you need NgRx?
200. When should you NOT use NgRx?
201. Explain:

```text
Store
Action
Reducer
Selector
Effect
```

202. What is an NgRx Effect?
203. Reducer vs Effect.
204. Selector vs direct Store subscription.
205. How do you prevent unnecessary selector emissions?
206. NgRx vs BehaviorSubject-based state management.
207. What is Signal-based state management?
208. Signals vs RxJS Observables.
209. When would you use Signals vs RxJS?

---

# 15. Angular Signals ⭐

For modern Angular interviews, prepare these.

210. What is a Signal?
211. What is `signal()`?
212. What is `computed()`?
213. What is `effect()`?
214. Signal vs Observable.
215. What is `set()`?
216. What is `update()`?
217. How do signals interact with change detection?
218. How do you convert Observable → Signal?
219. How do you convert Signal → Observable?
220. When should you prefer Signals?
221. Can Signals replace RxJS completely?

---

# 16. Testing ⭐⭐

222. What is unit testing?
223. What should you test in an Angular component?
224. What is Jasmine?
225. What is Karma?
226. What is Jest?
227. How do you test a service?
228. How do you mock an HTTP request?
229. How do you test an HTTP interceptor?
230. How do you test an Observable?
231. How do you test asynchronous code?
232. What is `fakeAsync()`?
233. What is `tick()`?
234. Difference between `fakeAsync`, `waitForAsync`, and `async`.
235. How do you mock dependencies?
236. What is TestBed?
237. How do you test component `@Input()`?
238. How do you test component `@Output()`?
239. How do you test route guards?
240. How do you test reactive forms?

---

# 17. Angular Security

241. How does Angular protect against XSS?
242. What is Angular sanitization?
243. What is `DomSanitizer`?
244. When can `bypassSecurityTrustHtml()` be dangerous?
245. Where should JWT tokens be stored?
246. How do you protect Angular routes?
247. Does route guard provide real backend security?
248. How do you prevent unauthorized API access?
249. What is CSRF?
250. What is CORS?

---

# 18. Architecture ⭐⭐⭐

For **5+ years**, expect architecture questions.

251. How would you structure a large Angular application?
252. Feature-based vs layer-based folder structure.
253. How do you separate business logic from UI?
254. Where should API calls be placed?
255. Where should transformation/mapping logic be placed?
256. How would you design reusable components?
257. Smart vs dumb/presentational components.
258. How do you avoid tightly coupled components?
259. How would you design a shared component library?
260. How would you handle global error handling?
261. How would you implement logging?
262. How would you implement authentication?
263. How would you implement authorization?
264. How would you handle environment-specific configuration?
265. How do you organize a large Angular monorepo?

---

# 19. Real-World Scenario Questions ⭐⭐⭐

These are **especially important** for senior interviews.

### Scenario 1

> An API is being called 10 times when the user clicks a button once. How would you debug it?

Possible areas:

* Multiple subscriptions
* Component lifecycle
* `shareReplay`
* Event binding
* Multiple `async` subscriptions
* Change detection

---

### Scenario 2

> A page takes 8 seconds to load. How would you investigate?

Think about:

```text
Network
 ↓
API calls
 ↓
Bundle size
 ↓
Change detection
 ↓
DOM rendering
 ↓
RxJS subscriptions
 ↓
Images/assets
```

---

### Scenario 3

> Search API is getting called for every key press.

Solution:

```typescript
valueChanges.pipe(
  debounceTime(300),
  distinctUntilChanged(),
  switchMap(...)
)
```

---

### Scenario 4

> Multiple components request the same API.

How would you prevent duplicate requests?

```typescript
shareReplay(1)
```

or a service-level cache.

---

### Scenario 5

> User changes route while an API request is running.

How would you cancel the request?

```typescript
takeUntil(...)
```

or appropriate RxJS/Angular request cancellation patterns.

---

### Scenario 6

> A table has 50,000 records and Angular is very slow.

What would you do?

* Server-side pagination
* Virtual scrolling
* `OnPush`
* `trackBy`
* Avoid expensive template functions
* Reduce DOM elements
* Lazy rendering

---

### Scenario 7

> JWT expires while 5 API requests are running.

How would you implement token refresh without sending 5 refresh requests?

This is a **very good senior-level question**.

Expected concepts:

```text
Interceptor
   ↓
401
   ↓
Refresh token
   ↓
Share refresh request
   ↓
Queue/retry pending requests
```

---

# 20. Coding Questions

You should also practice coding rather than only theoretical questions.

### TypeScript

1. Implement `debounce()`.
2. Implement `throttle()`.
3. Remove duplicates from an array.
4. Group objects by property.
5. Find duplicate objects.
6. Implement a deep clone.
7. Flatten a nested array.
8. Implement a custom `filter()`.
9. Implement a custom `map()`.
10. Implement a cache using `Map`.

### RxJS

11. Implement search with `debounceTime + switchMap`.
12. Combine three APIs.
13. Retry an API three times.
14. Cache an API response.
15. Cancel an HTTP request.
16. Prevent duplicate API calls.
17. Sequential API calls.
18. Parallel API calls.
19. Handle API errors without terminating the stream.

### Angular

20. Create a reusable modal.
21. Create a custom directive.
22. Create a custom validator.
23. Create a reusable table component.
24. Implement pagination.
25. Implement search + filtering + sorting.
26. Implement authentication guard.
27. Implement HTTP interceptor.
28. Implement API caching.
29. Implement parent-child communication.
30. Build a dynamic reactive form.

---

# Most Important Topics for Your 5+ Years Interview

If your preparation time is limited, I would prioritize them like this:

| Priority     | Topic                    |
| ------------ | ------------------------ |
| 🔴 Very High | RxJS                     |
| 🔴 Very High | Change Detection         |
| 🔴 Very High | Angular Architecture     |
| 🔴 Very High | Performance Optimization |
| 🔴 Very High | HTTP Interceptors        |
| 🔴 Very High | TypeScript               |
| 🔴 Very High | Component Communication  |
| 🟠 High      | Reactive Forms           |
| 🟠 High      | Routing & Guards         |
| 🟠 High      | Dependency Injection     |
| 🟠 High      | Testing                  |
| 🟠 High      | State Management         |
| 🟠 High      | Signals                  |
| 🟡 Medium    | Directives               |
| 🟡 Medium    | Pipes                    |
| 🟡 Medium    | Angular Security         |

### A particularly good preparation order for you

Since you're already working with **Angular + TypeScript + RxJS**, I'd suggest:

**Week 1:** Angular fundamentals + lifecycle + DI
**Week 2:** RxJS fundamentals + operators
**Week 3:** Advanced RxJS + real-world scenarios
**Week 4:** Change detection + performance
**Week 5:** TypeScript advanced concepts
**Week 6:** Forms + Routing + HTTP + Interceptors
**Week 7:** Architecture + NgRx/Signals
**Week 8:** Testing + coding + mock interviews

And don't just memorize answers. For a **5+ year interview**, be prepared to explain **why you chose an approach, what alternatives exist, and what trade-offs you considered**.

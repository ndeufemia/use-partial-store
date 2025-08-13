<p align="center">
  <img width="400" height="400" alt="usePartialStore Logo" src="https://github.com/user-attachments/assets/9da0814b-4e7b-4fae-9f22-0faa51795bfe" />
</p>

<p align="center">
  <em>Type-safe dot-path selectors for Zustand and beyond</em>
</p>


## ✨ Overview

**usePartialStore** is a tiny TypeScript utility that lets you **select only specific parts of an object** (including deeply nested properties) using a `"parent.child.grandchild"` **dot-path syntax** — **with full type safety and IDE autocompletion**.  

It’s designed to work seamlessly with [Zustand](https://github.com/pmndrs/zustand) stores, but can also be used with any plain JavaScript or TypeScript object.

---

## 🚀 Features

- 🔍 **Dot-path selection** — `"a.b.c"` syntax to pick nested values  
- 🛡 **Type-safe** — full TypeScript inference & IDE autocompletion  
- ⚡ **Flexible** — works with Zustand, vanilla objects, or any state container  
- 🪶 **Lightweight** — minimal footprint, **zero dependencies** (except Lodash helpers)  
- 🎯 **Convenient** — internally uses [`lodash/get`](https://lodash.com/docs/4.17.15#get) and [`lodash/set`](https://lodash.com/docs/4.17.15#set)  

> ⚠️ **Hook rule note**: Passing `useStore` directly into `usePartialStore` breaks the React rule of hooks (must be called at the top level). Use with care or opt for the reducer approach.

---

## 📦 Installation

```bash
npm install use-partial-store
# or
yarn add use-partial-store
````

---

## 💡 Usage

### 1️⃣ With Zustand — Direct Hook Usage

```ts
import { usePartialStore } from 'use-partial-store';
import { useStore } from './store';

const MyComponent = () => {
  const { user, settings } = usePartialStore(useStore, [
    'user.name',
    'user.email',
    'settings.theme'
  ]);

  return (
    <div>
      <p>{user.name} ({user.email})</p>
      <p>Theme: {settings.theme}</p>
    </div>
  );
};
```

---

### 2️⃣ With Zustand — Reducer Approach (Hook-Safe)

```ts
import { createStoreSelector } from 'use-partial-store';
import { useStore } from './store';

const selector = createStoreSelector(['user.name', 'settings.theme']);

const MyComponent = () => {
  const { user, settings: { theme } } = useStore(selector);

  return (
    <div>
      <p>{user.name}</p>
      <p>Theme: {theme}</p>
    </div>
  );
};
```

---

### 3️⃣ With Vanilla Objects

```ts
import { createStoreSelector } from 'use-partial-store';

const data = {
  user: { name: 'John', email: 'john@example.com' },
  settings: { theme: 'dark' }
};

const selector = createStoreSelector(['user.email', 'settings.theme']);

console.log(selector(data));
// { user: { email: 'john@example.com' }, settings: { theme: 'dark' } }
```

---

## ⚙️ How it Works

`use-partial-store` internally uses:

* [`lodash/get`](https://lodash.com/docs/4.17.15#get) and [`lodash/set`](https://lodash.com/docs/4.17.15#set) for safe nested property access & assignment.
* [Lodash repository](https://github.com/lodash/lodash) attribution for their utility functions.

---

## 🛠 API

### `createStoreSelector<T>(paths: Path<T>[])`

Creates a reducer function to extract only the specified paths from an object.

### `usePartialStore<T>(useStore, paths: Path<T>[])`

React hook version that integrates directly with Zustand's `useStore` hook.

---

## 📄 License

[use-partial-store](https://github.com/ndeufemia/use-partial-store) © 2025 by [Nico Deufemia](https://github.com/ndeufemia/) is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)![](https://mirrors.creativecommons.org/presskit/icons/cc.svg)![](https://mirrors.creativecommons.org/presskit/icons/by.svg)




---

## 👤 Author

**Nico Deufemia**
[<img src="https://cdn.jsdelivr.net/gh/simple-icons/simple-icons/icons/linkedin.svg" alt="LinkedIn" height="16"/> LinkedIn](https://www.linkedin.com/in/ndeufemia/) • [GitHub](https://github.com/ndeufemia)

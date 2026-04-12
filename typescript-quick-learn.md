# TypeScript 快速学习指南

> 🎯 目标：从零开始，1-2 周内能用 TypeScript 进行实际开发
> 📖 适合：有 JavaScript 基础的开发者（如果没有，请先学习 JS）
> ⏱️ 预计学习时间：30-50 小时

---

## 1. 为什么选择 TypeScript？

### 1.1 语言定位

- **诞生**：2012 年，微软 Anders Hejlsberg（C# 之父）主导设计
- **设计哲学**：JavaScript 的超集 — 给 JS 加上类型系统，编译后变回 JS
- **核心价值**：
  - 🛡️ 编译时发现错误，而非运行时崩溃
  - 📖 代码即文档，类型就是最好的注释
  - 🧠 IDE 智能提示，开发效率翻倍
  - 🏗️ 大型项目必备，团队协作利器

### 1.2 谁在用？

| 公司 | 使用场景 |
|------|---------|
| Microsoft | VS Code、Azure、Office 365 |
| Google | Angular 框架（官方语言） |
| Airbnb | 全面迁移至 TypeScript |
| Slack | 桌面客户端 |
| Stripe | API 和 SDK |

- **GitHub Star**：100k+（最受欢迎的编程语言之一）
- **State of JS 调查**：连续多年满意度最高的 JS 工具
- **趋势**：几乎所有新的 JS 项目都默认使用 TypeScript

### 1.3 TypeScript vs JavaScript 一览

| 特性 | JavaScript | TypeScript |
|------|-----------|-----------|
| 类型系统 | 动态类型 | 静态类型（可选） |
| 编译 | 直接运行 | 需编译为 JS |
| 错误发现 | 运行时 | 编译时 |
| IDE 支持 | 基础 | 极强（自动补全、重构） |
| 学习曲线 | 低 | 中（需学类型系统） |
| 适合项目 | 小型/原型 | 中大型/团队协作 |
| 生态 | npm 全部可用 | npm 全部可用 + 类型定义 |

---

## 2. 环境搭建（10 分钟上手）

### 2.1 安装

```bash
# 前提：已安装 Node.js
node --version  # 确认已安装

# 全局安装 TypeScript
npm install -g typescript

# 验证安装
tsc --version  # 应输出 Version 5.x.x

# 安装 ts-node（直接运行 TS 文件，无需手动编译）
npm install -g ts-node

# 更现代的选择：tsx（更快，零配置）
npm install -g tsx
```

### 2.2 编辑器推荐

| 工具 | 推荐理由 | 必装插件 |
|------|---------|---------|
| **VS Code**（首选） | 微软出品，TS 原生支持最佳 | ESLint, Prettier, Pretty TypeScript Errors |
| WebStorm | 内置 TS 支持，重构能力强 | 内置全套 |
| Cursor | AI + TS 类型推断 | 内置 |

### 2.3 Hello World

```bash
# 创建项目
mkdir hello-ts && cd hello-ts
npm init -y

# 初始化 TypeScript 配置
tsc --init
```

```typescript
// hello.ts
const greeting: string = "Hello, TypeScript! 🚀";
console.log(greeting);

// 感受类型的力量
function add(a: number, b: number): number {
  return a + b;
}

console.log(add(1, 2));    // 3
// console.log(add("1", 2)); // ❌ 编译错误！不能把 string 传给 number
```

```bash
# 方式1：编译后运行
tsc hello.ts && node hello.js

# 方式2：直接运行（推荐）
tsx hello.ts
```

### 2.4 tsconfig.json 推荐配置

```json
{
  "compilerOptions": {
    "target": "ES2022",
    "module": "NodeNext",
    "moduleResolution": "NodeNext",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "declaration": true,
    "sourceMap": true
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

> 💡 **关键配置**：`"strict": true` 开启所有严格检查，新项目务必开启！

---

## 3. 语法速查表

### 3.1 基本类型

| 类型 | 语法 | 示例 |
|------|------|------|
| 字符串 | `string` | `let s: string = "hello";` |
| 数字 | `number` | `let n: number = 42;` |
| 布尔 | `boolean` | `let b: boolean = true;` |
| 数组 | `T[]` 或 `Array<T>` | `let arr: number[] = [1, 2, 3];` |
| 元组 | `[T1, T2]` | `let t: [string, number] = ["age", 25];` |
| 枚举 | `enum` | `enum Color { Red, Green, Blue }` |
| any | `any` | `let x: any = "anything";` ⚠️ 尽量避免 |
| unknown | `unknown` | `let x: unknown = getData();` ✅ 比 any 安全 |
| void | `void` | `function log(): void { console.log("hi"); }` |
| never | `never` | `function fail(): never { throw new Error(); }` |
| null/undefined | `null / undefined` | `let n: null = null;` |

### 3.2 类型注解 vs 类型推断

```typescript
// 显式注解（你告诉 TS 类型）
let name: string = "Alice";
let age: number = 25;

// 类型推断（TS 自动推断，推荐！更简洁）
let name = "Alice";   // TS 推断为 string
let age = 25;         // TS 推断为 number
let arr = [1, 2, 3];  // TS 推断为 number[]

// 💡 原则：能推断的就不写，推断不了的才注解
// 函数参数必须注解，返回值通常可以推断
function greet(name: string) {  // 参数必须注解
  return `Hello, ${name}`;      // 返回值自动推断为 string
}
```

### 3.3 函数类型

```typescript
// 基本函数
function add(a: number, b: number): number {
  return a + b;
}

// 箭头函数
const multiply = (a: number, b: number): number => a * b;

// 可选参数（?）
function greet(name: string, greeting?: string): string {
  return `${greeting ?? "Hello"}, ${name}!`;
}
greet("Alice");           // "Hello, Alice!"
greet("Alice", "Hi");     // "Hi, Alice!"

// 默认参数
function greet(name: string, greeting: string = "Hello"): string {
  return `${greeting}, ${name}!`;
}

// 剩余参数
function sum(...nums: number[]): number {
  return nums.reduce((a, b) => a + b, 0);
}

// 函数类型定义
type MathFn = (a: number, b: number) => number;
const divide: MathFn = (a, b) => a / b;
```

### 3.4 联合类型与字面量类型

```typescript
// 联合类型 — 可以是多种类型之一
let id: string | number;
id = "abc";  // ✅
id = 123;    // ✅
// id = true; // ❌

// 字面量类型 — 限定具体值
type Direction = "up" | "down" | "left" | "right";
let dir: Direction = "up";  // ✅
// dir = "diagonal";        // ❌

// 类型收窄（Narrowing）
function printId(id: string | number) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());  // TS 知道这里是 string
  } else {
    console.log(id.toFixed(2));     // TS 知道这里是 number
  }
}
```

---

## 4. 核心概念详解

### 4.1 接口（Interface）

**一句话理解**：定义对象的"形状"——规定对象必须有哪些属性和方法。

**类比**：接口就像一份"入职体检表"——不管你是谁，只要你的体检项目都合格（属性都满足），就能通过。

```typescript
// 定义接口
interface User {
  id: number;
  name: string;
  email: string;
  age?: number;           // 可选属性
  readonly createdAt: Date; // 只读属性
}

// 使用接口
function createUser(data: User): User {
  return { ...data, createdAt: new Date() };
}

const user = createUser({
  id: 1,
  name: "Alice",
  email: "alice@example.com",
  createdAt: new Date(),
});

// user.createdAt = new Date(); // ❌ 只读属性不能修改

// 接口继承
interface Admin extends User {
  role: "admin" | "superadmin";
  permissions: string[];
}

// 接口合并（同名接口自动合并）
interface User {
  avatar?: string;  // 自动添加到 User 接口
}
```

**实际应用**：API 响应类型定义、组件 Props、数据库模型。

### 4.2 类型别名（Type Alias）

**一句话理解**：给类型起个名字，可以定义任何类型（不仅是对象）。

```typescript
// 基本类型别名
type ID = string | number;
type Status = "active" | "inactive" | "banned";

// 对象类型
type Point = {
  x: number;
  y: number;
};

// 函数类型
type Callback = (error: Error | null, data: unknown) => void;

// 交叉类型（合并多个类型）
type Timestamped = {
  createdAt: Date;
  updatedAt: Date;
};

type UserWithTimestamp = User & Timestamped;

// 条件类型（高级）
type IsString<T> = T extends string ? "yes" : "no";
type A = IsString<string>;  // "yes"
type B = IsString<number>;  // "no"
```

> 💡 **Interface vs Type**：
> - `interface`：适合定义对象形状，支持继承和合并
> - `type`：更灵活，支持联合类型、交叉类型、映射类型
> - 经验法则：对象用 `interface`，其他用 `type`

### 4.3 泛型（Generics）

**一句话理解**：让类型也能当"参数"传递，写一次代码适用于多种类型。

**类比**：泛型就像一个"万能模具"——同一个模具，倒入巧克力就做巧克力，倒入冰淇淋就做冰淇淋，形状一样但内容不同。

```typescript
// 没有泛型 — 要么用 any（不安全），要么写多个函数
function firstNumber(arr: number[]): number | undefined {
  return arr[0];
}
function firstString(arr: string[]): string | undefined {
  return arr[0];
}

// ✅ 使用泛型 — 一个函数搞定所有类型
function first<T>(arr: T[]): T | undefined {
  return arr[0];
}

first([1, 2, 3]);       // 返回类型自动推断为 number | undefined
first(["a", "b"]);      // 返回类型自动推断为 string | undefined

// 泛型约束
interface HasLength {
  length: number;
}

function logLength<T extends HasLength>(item: T): void {
  console.log(item.length);
}

logLength("hello");     // ✅ string 有 length
logLength([1, 2, 3]);   // ✅ array 有 length
// logLength(123);      // ❌ number 没有 length

// 泛型接口
interface ApiResponse<T> {
  code: number;
  message: string;
  data: T;
}

type UserResponse = ApiResponse<User>;
type BookListResponse = ApiResponse<Book[]>;

// 泛型工具类型（内置）
type Partial<T>;    // 所有属性变可选
type Required<T>;   // 所有属性变必选
type Readonly<T>;   // 所有属性变只读
type Pick<T, K>;    // 选取部分属性
type Omit<T, K>;    // 排除部分属性
type Record<K, V>;  // 键值对类型

// 实际使用
type UserUpdate = Partial<User>;  // 所有字段可选，用于更新
type UserPreview = Pick<User, "id" | "name">;  // 只要 id 和 name
```

**实际应用**：API 响应封装、数据容器、工具函数库。

### 4.4 类型守卫与类型收窄

**一句话理解**：在运行时检查类型，让 TypeScript 在不同分支中"知道"具体类型。

```typescript
// typeof 守卫
function padLeft(value: string, padding: string | number): string {
  if (typeof padding === "number") {
    return " ".repeat(padding) + value;  // TS 知道 padding 是 number
  }
  return padding + value;  // TS 知道 padding 是 string
}

// instanceof 守卫
class Dog { bark() { return "Woof!"; } }
class Cat { meow() { return "Meow!"; } }

function speak(animal: Dog | Cat): string {
  if (animal instanceof Dog) {
    return animal.bark();   // TS 知道是 Dog
  }
  return animal.meow();    // TS 知道是 Cat
}

// in 守卫
interface Fish { swim(): void; }
interface Bird { fly(): void; }

function move(animal: Fish | Bird) {
  if ("swim" in animal) {
    animal.swim();  // TS 知道是 Fish
  } else {
    animal.fly();   // TS 知道是 Bird
  }
}

// 自定义类型守卫（最强大）
interface ApiError {
  code: number;
  message: string;
}

function isApiError(error: unknown): error is ApiError {
  return (
    typeof error === "object" &&
    error !== null &&
    "code" in error &&
    "message" in error
  );
}

// 使用
try {
  await fetchData();
} catch (error) {
  if (isApiError(error)) {
    console.log(error.code);     // TS 知道有 code 属性
    console.log(error.message);  // TS 知道有 message 属性
  }
}
```

### 4.5 枚举与常量

**一句话理解**：定义一组命名常量，让代码更可读、更安全。

```typescript
// 数字枚举
enum Direction {
  Up = 0,
  Down = 1,
  Left = 2,
  Right = 3,
}

// 字符串枚举（推荐，更可读）
enum Status {
  Active = "ACTIVE",
  Inactive = "INACTIVE",
  Banned = "BANNED",
}

function setStatus(status: Status) {
  console.log(`Setting status to ${status}`);
}
setStatus(Status.Active);  // "Setting status to ACTIVE"

// ✅ 更推荐：const 枚举（编译后会被内联，零运行时开销）
const enum HttpStatus {
  OK = 200,
  NotFound = 404,
  ServerError = 500,
}

// ✅✅ 最推荐：用 as const 替代枚举
const STATUS = {
  Active: "ACTIVE",
  Inactive: "INACTIVE",
  Banned: "BANNED",
} as const;

type Status2 = (typeof STATUS)[keyof typeof STATUS];
// "ACTIVE" | "INACTIVE" | "BANNED"
```

### 4.6 类型工具与映射类型

**一句话理解**：TypeScript 内置了一套"类型变换工具"，可以基于已有类型生成新类型。

```typescript
interface User {
  id: number;
  name: string;
  email: string;
  password: string;
}

// Partial — 所有属性变可选（用于更新操作）
type UserUpdate = Partial<User>;
// { id?: number; name?: string; email?: string; password?: string; }

// Pick — 选取部分属性
type UserPublic = Pick<User, "id" | "name" | "email">;
// { id: number; name: string; email: string; }

// Omit — 排除部分属性
type UserWithoutPassword = Omit<User, "password">;
// { id: number; name: string; email: string; }

// Record — 键值对映射
type UserRoles = Record<string, "admin" | "user" | "guest">;
// { [key: string]: "admin" | "user" | "guest" }

// 组合使用（实际场景）
type CreateUserInput = Omit<User, "id">;  // 创建时不需要 id
type UpdateUserInput = Partial<Omit<User, "id">>;  // 更新时 id 不能改，其他可选

// 自定义映射类型
type Nullable<T> = {
  [K in keyof T]: T[K] | null;
};

type NullableUser = Nullable<User>;
// { id: number | null; name: string | null; ... }
```

### 4.7 模块与声明文件

**一句话理解**：TypeScript 的模块系统和 JS 一样，但多了类型导出和 `.d.ts` 声明文件。

```typescript
// types.ts — 导出类型
export interface User {
  id: number;
  name: string;
}

export type ApiResponse<T> = {
  code: number;
  data: T;
};

// service.ts — 导入并使用
import type { User, ApiResponse } from "./types";  // import type 只导入类型

async function getUser(id: number): Promise<ApiResponse<User>> {
  const res = await fetch(`/api/users/${id}`);
  return res.json();
}

// 为没有类型的 JS 库写声明文件
// my-lib.d.ts
declare module "my-lib" {
  export function doSomething(input: string): number;
  export interface Config {
    debug: boolean;
    timeout: number;
  }
}
```

### 4.8 装饰器（Decorators）

**一句话理解**：给类、方法、属性"贴标签"，自动添加额外行为。

```typescript
// 需要在 tsconfig.json 中开启：
// "experimentalDecorators": true

// 方法装饰器 — 自动记录日志
function Log(target: any, key: string, descriptor: PropertyDescriptor) {
  const original = descriptor.value;
  descriptor.value = function (...args: any[]) {
    console.log(`调用 ${key}，参数:`, args);
    const result = original.apply(this, args);
    console.log(`${key} 返回:`, result);
    return result;
  };
}

class Calculator {
  @Log
  add(a: number, b: number): number {
    return a + b;
  }
}

const calc = new Calculator();
calc.add(1, 2);
// 输出：调用 add，参数: [1, 2]
// 输出：add 返回: 3
```

**实际应用**：NestJS 的 `@Controller`、`@Get`、`@Injectable` 等。

---

## 5. 实战项目

### 项目 1：类型安全的 Todo 应用（入门级，约 30 分钟）

**目标**：练习接口、类型注解、枚举

```typescript
// todo.ts
import * as readline from "readline";

// 定义类型
enum Priority {
  Low = "LOW",
  Medium = "MEDIUM",
  High = "HIGH",
}

interface Todo {
  id: number;
  text: string;
  done: boolean;
  priority: Priority;
  createdAt: Date;
}

// Todo 管理器
class TodoManager {
  private todos: Todo[] = [];
  private nextId = 1;

  add(text: string, priority: Priority = Priority.Medium): Todo {
    const todo: Todo = {
      id: this.nextId++,
      text,
      done: false,
      priority,
      createdAt: new Date(),
    };
    this.todos.push(todo);
    return todo;
  }

  toggle(id: number): Todo | undefined {
    const todo = this.todos.find((t) => t.id === id);
    if (todo) todo.done = !todo.done;
    return todo;
  }

  remove(id: number): boolean {
    const index = this.todos.findIndex((t) => t.id === id);
    if (index === -1) return false;
    this.todos.splice(index, 1);
    return true;
  }

  list(filter?: "all" | "done" | "pending"): Todo[] {
    switch (filter) {
      case "done":
        return this.todos.filter((t) => t.done);
      case "pending":
        return this.todos.filter((t) => !t.done);
      default:
        return [...this.todos];
    }
  }

  stats(): { total: number; done: number; pending: number } {
    const done = this.todos.filter((t) => t.done).length;
    return {
      total: this.todos.length,
      done,
      pending: this.todos.length - done,
    };
  }
}

// 使用
const manager = new TodoManager();
manager.add("学习 TypeScript 基础", Priority.High);
manager.add("完成实战项目", Priority.Medium);
manager.add("阅读官方文档", Priority.Low);

manager.toggle(1);

console.log("📋 所有任务:");
manager.list().forEach((todo) => {
  const icon = todo.done ? "✅" : "⬜";
  const priority = { LOW: "🟢", MEDIUM: "🟡", HIGH: "🔴" }[todo.priority];
  console.log(`  ${icon} ${priority} [${todo.id}] ${todo.text}`);
});

console.log("\n📊 统计:", manager.stats());
```

```bash
tsx todo.ts
```

### 项目 2：类型安全的 HTTP 客户端（进阶级，约 1 小时）

**目标**：练习泛型、类型守卫、异步、错误处理

```typescript
// api-client.ts

// 类型定义
interface ApiResponse<T> {
  code: number;
  message: string;
  data: T;
}

interface ApiError {
  code: number;
  message: string;
  details?: string;
}

type Result<T> =
  | { success: true; data: T }
  | { success: false; error: ApiError };

// 类型安全的 HTTP 客户端
class ApiClient {
  constructor(private baseUrl: string) {}

  private async request<T>(
    method: string,
    path: string,
    body?: unknown
  ): Promise<Result<T>> {
    try {
      const url = `${this.baseUrl}${path}`;
      const options: RequestInit = {
        method,
        headers: { "Content-Type": "application/json" },
        body: body ? JSON.stringify(body) : undefined,
      };

      const response = await fetch(url, options);
      const json = await response.json();

      if (!response.ok) {
        return {
          success: false,
          error: {
            code: response.status,
            message: json.message ?? "请求失败",
          },
        };
      }

      return { success: true, data: json as T };
    } catch (error) {
      return {
        success: false,
        error: {
          code: 0,
          message: error instanceof Error ? error.message : "未知错误",
        },
      };
    }
  }

  get<T>(path: string): Promise<Result<T>> {
    return this.request<T>("GET", path);
  }

  post<T>(path: string, body: unknown): Promise<Result<T>> {
    return this.request<T>("POST", path, body);
  }

  put<T>(path: string, body: unknown): Promise<Result<T>> {
    return this.request<T>("PUT", path, body);
  }

  delete<T>(path: string): Promise<Result<T>> {
    return this.request<T>("DELETE", path);
  }
}

// 使用示例
interface User {
  id: number;
  name: string;
  email: string;
}

interface Post {
  id: number;
  title: string;
  body: string;
  userId: number;
}

async function main() {
  const api = new ApiClient("https://jsonplaceholder.typicode.com");

  // 获取用户 — 返回类型自动推断
  const userResult = await api.get<User>("/users/1");
  if (userResult.success) {
    console.log("👤 用户:", userResult.data.name);  // TS 知道 data 是 User
  } else {
    console.error("❌ 错误:", userResult.error.message);  // TS 知道有 error
  }

  // 获取文章列表
  const postsResult = await api.get<Post[]>("/posts?_limit=3");
  if (postsResult.success) {
    console.log("\n📝 文章列表:");
    postsResult.data.forEach((post) => {
      console.log(`  - [${post.id}] ${post.title}`);
    });
  }

  // 创建文章
  const newPost = await api.post<Post>("/posts", {
    title: "TypeScript 真好用",
    body: "类型安全让开发更愉快",
    userId: 1,
  });
  if (newPost.success) {
    console.log("\n✅ 创建成功:", newPost.data.title);
  }
}

main();
```

```bash
tsx api-client.ts
```

### 项目 3：Express + TypeScript REST API（综合级，约 2 小时）

**目标**：综合运用类型系统构建完整后端服务

```bash
# 初始化项目
mkdir ts-api && cd ts-api
npm init -y
npm install express
npm install -D typescript @types/express @types/node tsx
npx tsc --init
```

```typescript
// src/types.ts
export interface Book {
  id: number;
  title: string;
  author: string;
  year: number;
  isbn?: string;
}

export type CreateBookInput = Omit<Book, "id">;
export type UpdateBookInput = Partial<CreateBookInput>;

export interface ApiResponse<T> {
  success: boolean;
  data?: T;
  error?: string;
}

// src/store.ts
import { Book, CreateBookInput, UpdateBookInput } from "./types";

class BookStore {
  private books: Book[] = [
    { id: 1, title: "TypeScript 编程", author: "Boris Cherny", year: 2019 },
    { id: 2, title: "深入理解 TypeScript", author: "Basarat", year: 2020 },
  ];
  private nextId = 3;

  findAll(): Book[] {
    return [...this.books];
  }

  findById(id: number): Book | undefined {
    return this.books.find((b) => b.id === id);
  }

  create(input: CreateBookInput): Book {
    const book: Book = { id: this.nextId++, ...input };
    this.books.push(book);
    return book;
  }

  update(id: number, input: UpdateBookInput): Book | undefined {
    const book = this.findById(id);
    if (!book) return undefined;
    Object.assign(book, input);
    return book;
  }

  delete(id: number): boolean {
    const index = this.books.findIndex((b) => b.id === id);
    if (index === -1) return false;
    this.books.splice(index, 1);
    return true;
  }
}

export const bookStore = new BookStore();

// src/app.ts
import express, { Request, Response } from "express";
import { bookStore } from "./store";
import { ApiResponse, Book, CreateBookInput } from "./types";

const app = express();
app.use(express.json());

// 获取所有书籍
app.get("/api/books", (_req: Request, res: Response<ApiResponse<Book[]>>) => {
  res.json({ success: true, data: bookStore.findAll() });
});

// 获取单本书籍
app.get("/api/books/:id", (req: Request, res: Response<ApiResponse<Book>>) => {
  const book = bookStore.findById(parseInt(req.params.id));
  if (!book) {
    res.status(404).json({ success: false, error: "书籍未找到" });
    return;
  }
  res.json({ success: true, data: book });
});

// 创建书籍
app.post("/api/books", (req: Request<{}, {}, CreateBookInput>, res: Response<ApiResponse<Book>>) => {
  const { title, author, year } = req.body;
  if (!title || !author || !year) {
    res.status(400).json({ success: false, error: "title, author, year 为必填" });
    return;
  }
  const book = bookStore.create({ title, author, year });
  res.status(201).json({ success: true, data: book });
});

// 删除书籍
app.delete("/api/books/:id", (req: Request, res: Response<ApiResponse<Book>>) => {
  const success = bookStore.delete(parseInt(req.params.id));
  if (!success) {
    res.status(404).json({ success: false, error: "书籍未找到" });
    return;
  }
  res.json({ success: true });
});

const PORT = 3000;
app.listen(PORT, () => {
  console.log(`🚀 TypeScript API 运行在 http://localhost:${PORT}`);
});
```

```bash
tsx src/app.ts
```

---

## 6. 常见陷阱与调试

### 6.1 Top 10 新手错误

**1. 滥用 `any`**
```typescript
// ❌ 用 any 就等于放弃了 TypeScript
function process(data: any) {
  return data.foo.bar;  // 运行时可能崩溃，TS 不会警告
}

// ✅ 用 unknown + 类型守卫
function process(data: unknown) {
  if (typeof data === "object" && data !== null && "foo" in data) {
    // 安全访问
  }
}
```

**2. 忘记处理 `null/undefined`**
```typescript
// ❌
const users: User[] = [];
const first = users[0];
console.log(first.name);  // 运行时崩溃！

// ✅ 可选链 + 空值合并
console.log(first?.name ?? "未知用户");
```

**3. 类型断言滥用**
```typescript
// ❌ 强制断言（危险）
const data = fetchData() as User;  // 如果不是 User 呢？

// ✅ 类型守卫（安全）
function isUser(data: unknown): data is User {
  return typeof data === "object" && data !== null && "name" in data;
}
```

**4. 对象字面量多余属性检查**
```typescript
interface Config {
  host: string;
  port: number;
}

// ❌ 直接传字面量会检查多余属性
// const config: Config = { host: "localhost", port: 3000, debug: true };
// Error: 'debug' does not exist in type 'Config'

// ✅ 通过变量传递可以绕过（但不推荐）
const raw = { host: "localhost", port: 3000, debug: true };
const config: Config = raw;  // OK，但 debug 被忽略
```

**5. 枚举的坑**
```typescript
// ❌ 数字枚举可以接受任意数字
enum Status { Active, Inactive }
const s: Status = 999;  // 不报错！

// ✅ 用字符串枚举或 as const
const STATUS = { Active: "active", Inactive: "inactive" } as const;
```

### 6.2 调试技巧

```typescript
// 1. 查看推断类型 — 鼠标悬停在变量上（VS Code）

// 2. 使用 satisfies 检查类型但保留推断
const config = {
  width: 100,
  height: 200,
} satisfies Record<string, number>;
// config.width 的类型是 100（字面量），而非 number

// 3. 临时查看复杂类型
type Expand<T> = T extends infer O ? { [K in keyof O]: O[K] } : never;
type Debug = Expand<UserWithTimestamp>;  // 悬停查看展开后的类型
```

---

## 7. 生态与工具链

### 7.1 包管理

```bash
# 安装带类型的包
npm install express
npm install -D @types/express  # 类型定义

# 很多现代包自带类型，无需额外安装
npm install zod        # 自带类型
npm install axios      # 自带类型
```

### 7.2 必知库/框架

| 库名 | 用途 | 类型支持 |
|------|------|---------|
| **Zod** | 运行时类型验证 | 原生 TS |
| **tRPC** | 端到端类型安全 API | 原生 TS |
| **Prisma** | 类型安全 ORM | 原生 TS |
| **Next.js** | React 全栈框架 | 原生 TS |
| **NestJS** | 企业级后端框架 | 原生 TS |
| **Vitest** | 测试框架 | 原生 TS |
| **ts-pattern** | 模式匹配 | 原生 TS |
| **Effect** | 函数式错误处理 | 原生 TS |

### 7.3 测试

```typescript
// math.test.ts（使用 Vitest）
import { describe, it, expect } from "vitest";
import { add } from "./math";

describe("add", () => {
  it("应该正确相加两个数", () => {
    expect(add(1, 2)).toBe(3);
  });

  it("应该处理负数", () => {
    expect(add(-1, 1)).toBe(0);
  });
});
```

---

## 8. 学习路线图

### 🗓️ 第 1 周：基础类型
- [ ] Day 1-2：基本类型注解 + 类型推断
- [ ] Day 3-4：接口 + 类型别名 + 联合类型
- [ ] Day 5-6：函数类型 + 泛型基础
- [ ] Day 7：完成项目 1（类型安全 Todo）

### 🗓️ 第 2-4 周：进阶类型
- [ ] Week 2：泛型深入 + 类型守卫 + 类型收窄
- [ ] Week 3：工具类型 + 映射类型 + 条件类型
- [ ] Week 4：完成项目 2 + 项目 3

### 🗓️ 第 2-3 月：实战深入
- [ ] Month 2：学习 Next.js / NestJS + Prisma
- [ ] Month 3：高级模式（类型体操）+ 开源贡献

### 📚 推荐资源

| 类型 | 资源名 | 适合阶段 |
|------|--------|---------|
| 官方文档 | [TypeScript Handbook](https://www.typescriptlang.org/docs/) | 全阶段 |
| 练习 | [Type Challenges](https://github.com/type-challenges/type-challenges) | 进阶 |
| 书籍 | 《Programming TypeScript》 | 入门→进阶 |
| 工具 | [TypeScript Playground](https://www.typescriptlang.org/play) | 全阶段 |

---

## 9. 速查备忘录（Cheat Sheet）

```
╔══════════════════════════════════════════════════════════════╗
║                  TypeScript 速查卡                           ║
╠══════════════════════════════════════════════════════════════╣
║ 基本    let x: string = "hi";  const n: number = 1;         ║
║ 数组    let a: number[] = [1,2];  Array<string>              ║
║ 元组    let t: [string, number] = ["a", 1];                  ║
║ 联合    let id: string | number;                             ║
║ 字面量  type Dir = "up" | "down" | "left" | "right";         ║
║ 接口    interface User { name: string; age?: number; }       ║
║ 类型    type Point = { x: number; y: number };               ║
║ 泛型    function first<T>(arr: T[]): T | undefined           ║
║ 断言    value as string  /  <string>value                    ║
║ 守卫    typeof / instanceof / in / is                        ║
║ 工具    Partial / Required / Pick / Omit / Record            ║
║ 空安全  ?. (可选链)  ?? (空值合并)  ! (非空断言)               ║
║ 导入    import type { User } from "./types";                 ║
║ 只读    readonly / Readonly<T> / as const                    ║
╚══════════════════════════════════════════════════════════════╝
```

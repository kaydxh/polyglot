# JavaScript 快速学习指南

> 🎯 目标：从零开始，1-2 周内能用 JavaScript 进行实际开发
> 📖 适合：编程初学者或从其他语言转来的开发者
> ⏱️ 预计学习时间：40-60 小时

---

## 1. 为什么选择 JavaScript？

### 1.1 语言定位

- **诞生**：1995 年，Brendan Eich 在 Netscape 用 10 天创造
- **设计哲学**：灵活、动态、多范式（面向对象 + 函数式）
- **应用领域**：
  - 🌐 Web 前端（浏览器唯一原生语言）
  - 🖥️ Web 后端（Node.js）
  - 📱 移动应用（React Native / Expo）
  - 🖥️ 桌面应用（Electron）
  - 🤖 AI/ML（TensorFlow.js）

### 1.2 谁在用？

| 公司 | 使用场景 |
|------|---------|
| Google | Chrome V8 引擎、Angular、各类 Web 服务 |
| Meta | React、React Native |
| Netflix | Node.js 后端服务 |
| Uber | 实时地图、Node.js 微服务 |
| Airbnb | 全栈 JavaScript |

- **TIOBE 排名**：长期 Top 10
- **GitHub 最活跃语言**：连续多年第一
- **npm 包数量**：200 万+（全球最大包注册表）

---

## 2. 环境搭建（10 分钟上手）

### 2.1 安装 Node.js

```bash
# macOS（使用 Homebrew）
brew install node

# Windows（使用 winget）
winget install OpenJS.NodeJS.LTS

# Linux（Ubuntu/Debian）
curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash -
sudo apt-get install -y nodejs

# 验证安装
node --version   # 应输出 v20.x.x 或更高
npm --version    # 应输出 10.x.x 或更高
```

### 2.2 编辑器推荐

| 工具 | 推荐理由 | 必装插件 |
|------|---------|---------|
| **VS Code**（首选） | 免费、轻量、JS 生态最佳支持 | ESLint, Prettier, JavaScript (ES6) code snippets |
| WebStorm | JetBrains 出品，智能补全强 | 内置全套 |
| Cursor | AI 辅助编程 | 内置 AI 补全 |

### 2.3 Hello World

```bash
# 创建项目目录
mkdir hello-js && cd hello-js

# 创建文件
touch hello.js
```

```javascript
// hello.js
console.log("Hello, JavaScript! 🚀");

// 试试变量
const name = "开发者";
console.log(`你好，${name}！欢迎学习 JavaScript`);
```

```bash
# 运行
node hello.js
# 输出：
# Hello, JavaScript! 🚀
# 你好，开发者！欢迎学习 JavaScript
```

### 2.4 浏览器控制台（交互式体验）

打开任意浏览器 → 按 `F12` → 切换到 `Console` 标签 → 直接输入 JS 代码：

```javascript
// 在浏览器控制台中尝试
1 + 1                    // 2
"hello".toUpperCase()    // "HELLO"
[1, 2, 3].map(x => x * 2)  // [2, 4, 6]
```

---

## 3. 语法速查表

### 3.1 变量与类型

| 概念 | 语法 | 示例 |
|------|------|------|
| 变量声明（可变） | `let` | `let count = 0;` |
| 常量声明（不可变） | `const` | `const PI = 3.14;` |
| ~~旧式声明~~（避免使用） | `var` | `var old = "别用";` |
| 数字 | `number` | `let n = 42; let f = 3.14;` |
| 字符串 | `string` | `let s = "hello";` |
| 布尔 | `boolean` | `let b = true;` |
| 空值 | `null / undefined` | `let a = null; let b;` |
| 数组 | `Array` | `let arr = [1, 2, 3];` |
| 对象 | `Object` | `let obj = { name: "JS" };` |

### 3.2 字符串操作

| 操作 | 语法 | 示例 |
|------|------|------|
| 模板字符串 | `` `${}` `` | `` `Hello ${name}` `` |
| 拼接 | `+` | `"a" + "b"  // "ab"` |
| 长度 | `.length` | `"hello".length  // 5` |
| 查找 | `.includes()` | `"hello".includes("ell")  // true` |
| 替换 | `.replace()` | `"hello".replace("h", "H")` |
| 分割 | `.split()` | `"a,b,c".split(",")  // ["a","b","c"]` |
| 大小写 | `.toUpperCase()` | `"hi".toUpperCase()  // "HI"` |

### 3.3 控制流

```javascript
// if / else
if (score >= 90) {
  console.log("优秀");
} else if (score >= 60) {
  console.log("及格");
} else {
  console.log("不及格");
}

// 三元运算符
const result = score >= 60 ? "通过" : "未通过";

// for 循环
for (let i = 0; i < 5; i++) {
  console.log(i);  // 0, 1, 2, 3, 4
}

// for...of（遍历值）
const fruits = ["🍎", "🍌", "🍊"];
for (const fruit of fruits) {
  console.log(fruit);
}

// while 循环
let count = 0;
while (count < 3) {
  console.log(count++);
}

// switch
switch (day) {
  case "Monday":
    console.log("周一");
    break;
  case "Friday":
    console.log("周五");
    break;
  default:
    console.log("其他");
}
```

### 3.4 函数

```javascript
// 函数声明
function greet(name) {
  return `Hello, ${name}!`;
}

// 箭头函数（推荐）
const greet = (name) => `Hello, ${name}!`;

// 默认参数
const greet = (name = "World") => `Hello, ${name}!`;

// 剩余参数
const sum = (...nums) => nums.reduce((a, b) => a + b, 0);
sum(1, 2, 3);  // 6

// 解构参数
const printUser = ({ name, age }) => {
  console.log(`${name} is ${age}`);
};
printUser({ name: "Alice", age: 25 });
```

### 3.5 数据结构

| 结构 | 创建 | 添加 | 访问 | 遍历 |
|------|------|------|------|------|
| 数组 | `[1, 2, 3]` | `.push(4)` | `arr[0]` | `.forEach()` / `for...of` |
| 对象 | `{ a: 1 }` | `obj.b = 2` | `obj.a` / `obj["a"]` | `Object.entries()` |
| Map | `new Map()` | `.set(k, v)` | `.get(k)` | `.forEach()` / `for...of` |
| Set | `new Set()` | `.add(v)` | `.has(v)` | `.forEach()` / `for...of` |

---

## 4. 核心概念详解

### 4.1 作用域与闭包

**一句话理解**：变量的"可见范围"，闭包让函数"记住"它诞生时的环境。

**类比**：作用域像房间的墙壁——房间里的人能看到房间内的东西，也能透过窗户看到外面，但外面的人看不到房间里的东西。闭包就像你离开房间时带走了一张房间的照片。

```javascript
// 作用域
let global = "我是全局的";

function outer() {
  let outerVar = "我是外层的";
  
  function inner() {
    let innerVar = "我是内层的";
    console.log(global);    // ✅ 能访问全局
    console.log(outerVar);  // ✅ 能访问外层
    console.log(innerVar);  // ✅ 能访问自己
  }
  
  inner();
  // console.log(innerVar); // ❌ 不能访问内层
}

// 闭包的实际应用：计数器
function createCounter() {
  let count = 0;  // 这个变量被"记住"了
  return {
    increment: () => ++count,
    getCount: () => count,
  };
}

const counter = createCounter();
counter.increment();  // 1
counter.increment();  // 2
counter.getCount();   // 2
```

**实际应用**：事件处理器、数据封装、函数工厂、防抖/节流。

### 4.2 异步编程（Promise / async-await）

**一句话理解**：JavaScript 是单线程的，异步让它能"同时"处理多件事而不阻塞。

**类比**：你在餐厅点了菜（发起异步请求），不需要站在厨房门口等（阻塞），而是回到座位继续聊天（执行其他代码），菜好了服务员会端过来（回调/Promise 完成）。

```javascript
// ❌ 回调地狱（旧方式，避免）
getData(function(a) {
  getMoreData(a, function(b) {
    getEvenMoreData(b, function(c) {
      console.log(c);
    });
  });
});

// ✅ Promise
function fetchUser(id) {
  return new Promise((resolve, reject) => {
    setTimeout(() => {
      if (id > 0) resolve({ id, name: "Alice" });
      else reject(new Error("无效 ID"));
    }, 1000);
  });
}

fetchUser(1)
  .then(user => console.log(user))
  .catch(err => console.error(err));

// ✅✅ async/await（最推荐）
async function main() {
  try {
    const user = await fetchUser(1);
    console.log(user);  // { id: 1, name: "Alice" }
    
    // 并行请求
    const [user1, user2] = await Promise.all([
      fetchUser(1),
      fetchUser(2),
    ]);
    console.log(user1, user2);
  } catch (err) {
    console.error("出错了:", err.message);
  }
}

main();
```

**实际应用**：API 请求、文件读写、数据库操作、定时任务。

### 4.3 数组高阶方法

**一句话理解**：用函数式的方式处理数组，比 for 循环更简洁、更安全。

```javascript
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];

// map — 转换每个元素
const doubled = numbers.map(n => n * 2);
// [2, 4, 6, 8, 10, 12, 14, 16, 18, 20]

// filter — 筛选元素
const evens = numbers.filter(n => n % 2 === 0);
// [2, 4, 6, 8, 10]

// reduce — 累积计算
const sum = numbers.reduce((acc, n) => acc + n, 0);
// 55

// find — 找到第一个匹配
const firstBig = numbers.find(n => n > 5);
// 6

// some / every — 条件检查
numbers.some(n => n > 5);   // true（至少一个满足）
numbers.every(n => n > 0);  // true（全部满足）

// 链式调用（实际场景：处理用户列表）
const users = [
  { name: "Alice", age: 25, active: true },
  { name: "Bob", age: 17, active: true },
  { name: "Charlie", age: 30, active: false },
  { name: "Diana", age: 22, active: true },
];

const result = users
  .filter(u => u.active)           // 只要活跃用户
  .filter(u => u.age >= 18)        // 只要成年人
  .map(u => u.name)                // 只取名字
  .sort();                         // 排序
// ["Alice", "Diana"]
```

### 4.4 解构与展开运算符

**一句话理解**：从对象/数组中快速"拆包"取值，或把多个东西"合并"到一起。

```javascript
// 对象解构
const user = { name: "Alice", age: 25, city: "Beijing" };
const { name, age } = user;
console.log(name);  // "Alice"

// 重命名
const { name: userName } = user;

// 默认值
const { country = "China" } = user;

// 数组解构
const [first, second, ...rest] = [1, 2, 3, 4, 5];
// first=1, second=2, rest=[3,4,5]

// 展开运算符 — 合并对象
const defaults = { theme: "dark", lang: "zh" };
const userPrefs = { lang: "en" };
const config = { ...defaults, ...userPrefs };
// { theme: "dark", lang: "en" }  后面的覆盖前面的

// 展开运算符 — 合并数组
const arr1 = [1, 2];
const arr2 = [3, 4];
const merged = [...arr1, ...arr2];  // [1, 2, 3, 4]

// 实际应用：React 中更新状态
const [state, setState] = useState({ count: 0, name: "test" });
setState(prev => ({ ...prev, count: prev.count + 1 }));
```

### 4.5 模块系统（ES Modules）

**一句话理解**：把代码拆分成独立文件，按需导入导出，保持代码整洁。

```javascript
// math.js — 导出
export const PI = 3.14159;

export function add(a, b) {
  return a + b;
}

export default function multiply(a, b) {
  return a * b;
}

// app.js — 导入
import multiply, { PI, add } from "./math.js";

console.log(PI);           // 3.14159
console.log(add(1, 2));    // 3
console.log(multiply(3, 4)); // 12

// 按需导入（重命名）
import { add as sum } from "./math.js";

// 导入全部
import * as math from "./math.js";
math.add(1, 2);
```

### 4.6 错误处理

**一句话理解**：程序出错时优雅地处理，而不是让整个应用崩溃。

```javascript
// 基本 try-catch
try {
  const data = JSON.parse("invalid json");
} catch (error) {
  console.error("解析失败:", error.message);
} finally {
  console.log("无论成功失败都执行");
}

// 自定义错误
class ValidationError extends Error {
  constructor(field, message) {
    super(message);
    this.name = "ValidationError";
    this.field = field;
  }
}

function validateAge(age) {
  if (typeof age !== "number") {
    throw new ValidationError("age", "年龄必须是数字");
  }
  if (age < 0 || age > 150) {
    throw new ValidationError("age", "年龄范围无效");
  }
  return true;
}

// 异步错误处理
async function fetchData(url) {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}`);
    }
    return await response.json();
  } catch (error) {
    console.error("请求失败:", error.message);
    return null;  // 返回默认值
  }
}
```

### 4.7 this 关键字

**一句话理解**：`this` 指向"谁调用了这个函数"，箭头函数除外（它继承外层的 `this`）。

```javascript
// 对象方法中的 this
const user = {
  name: "Alice",
  greet() {
    console.log(`Hi, I'm ${this.name}`);  // this = user
  },
};
user.greet();  // "Hi, I'm Alice"

// ⚠️ 常见陷阱：this 丢失
const greet = user.greet;
greet();  // "Hi, I'm undefined" — this 不再指向 user

// ✅ 解决方案1：bind
const boundGreet = user.greet.bind(user);
boundGreet();  // "Hi, I'm Alice"

// ✅ 解决方案2：箭头函数（继承外层 this）
const user2 = {
  name: "Bob",
  greet() {
    // 箭头函数继承 greet() 的 this
    const inner = () => console.log(`Hi, I'm ${this.name}`);
    inner();  // "Hi, I'm Bob"
  },
};
```

### 4.8 原型与类

**一句话理解**：JavaScript 用原型链实现继承，`class` 是语法糖让它看起来更像传统 OOP。

```javascript
// 现代 class 语法（推荐）
class Animal {
  constructor(name) {
    this.name = name;
  }
  
  speak() {
    console.log(`${this.name} makes a sound`);
  }
}

class Dog extends Animal {
  constructor(name, breed) {
    super(name);  // 调用父类构造函数
    this.breed = breed;
  }
  
  speak() {
    console.log(`${this.name} barks! 🐕`);
  }
  
  // getter
  get info() {
    return `${this.name} (${this.breed})`;
  }
}

const dog = new Dog("Buddy", "Golden Retriever");
dog.speak();  // "Buddy barks! 🐕"
dog.info;     // "Buddy (Golden Retriever)"

// 检查继承关系
dog instanceof Dog;     // true
dog instanceof Animal;  // true
```

---

## 5. 实战项目

### 项目 1：命令行 Todo 应用（入门级，约 30 分钟）

**目标**：练习变量、数组、函数、控制流

```javascript
// todo.js
const readline = require("readline");

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout,
});

const todos = [];

function showMenu() {
  console.log("\n📋 Todo 应用");
  console.log("1. 添加任务");
  console.log("2. 查看任务");
  console.log("3. 完成任务");
  console.log("4. 删除任务");
  console.log("5. 退出");
}

function addTodo(text) {
  todos.push({ text, done: false, createdAt: new Date() });
  console.log(`✅ 已添加: ${text}`);
}

function listTodos() {
  if (todos.length === 0) {
    console.log("📭 暂无任务");
    return;
  }
  todos.forEach((todo, i) => {
    const status = todo.done ? "✅" : "⬜";
    console.log(`${i + 1}. ${status} ${todo.text}`);
  });
}

function toggleTodo(index) {
  if (index >= 0 && index < todos.length) {
    todos[index].done = !todos[index].done;
    const status = todos[index].done ? "完成" : "未完成";
    console.log(`📝 "${todos[index].text}" 标记为${status}`);
  } else {
    console.log("❌ 无效编号");
  }
}

function deleteTodo(index) {
  if (index >= 0 && index < todos.length) {
    const removed = todos.splice(index, 1)[0];
    console.log(`🗑️ 已删除: ${removed.text}`);
  } else {
    console.log("❌ 无效编号");
  }
}

function prompt() {
  showMenu();
  rl.question("\n请选择操作: ", (choice) => {
    switch (choice) {
      case "1":
        rl.question("输入任务内容: ", (text) => {
          addTodo(text);
          prompt();
        });
        break;
      case "2":
        listTodos();
        prompt();
        break;
      case "3":
        listTodos();
        rl.question("输入要完成的任务编号: ", (num) => {
          toggleTodo(parseInt(num) - 1);
          prompt();
        });
        break;
      case "4":
        listTodos();
        rl.question("输入要删除的任务编号: ", (num) => {
          deleteTodo(parseInt(num) - 1);
          prompt();
        });
        break;
      case "5":
        console.log("👋 再见！");
        rl.close();
        break;
      default:
        console.log("❌ 无效选择");
        prompt();
    }
  });
}

prompt();
```

```bash
node todo.js
```

### 项目 2：天气查询 CLI 工具（进阶级，约 1 小时）

**目标**：练习异步编程、API 调用、错误处理、模块化

```javascript
// weather.js
const https = require("https");

// 使用免费的 wttr.in API（无需 API Key）
function fetchWeather(city) {
  return new Promise((resolve, reject) => {
    const url = `https://wttr.in/${encodeURIComponent(city)}?format=j1`;
    
    https.get(url, (res) => {
      let data = "";
      res.on("data", (chunk) => (data += chunk));
      res.on("end", () => {
        try {
          resolve(JSON.parse(data));
        } catch (e) {
          reject(new Error("解析天气数据失败"));
        }
      });
    }).on("error", reject);
  });
}

function formatWeather(data, city) {
  const current = data.current_condition[0];
  const forecast = data.weather.slice(0, 3);
  
  let output = `\n🌍 ${city} 天气报告\n`;
  output += "═".repeat(40) + "\n";
  output += `🌡️  温度: ${current.temp_C}°C (体感 ${current.FeelsLikeC}°C)\n`;
  output += `💧 湿度: ${current.humidity}%\n`;
  output += `💨 风速: ${current.windspeedKmph} km/h ${current.winddir16Point}\n`;
  output += `☁️  天气: ${current.weatherDesc[0].value}\n`;
  output += "\n📅 未来三天预报:\n";
  
  forecast.forEach((day) => {
    output += `  ${day.date}: ${day.mintempC}°C ~ ${day.maxtempC}°C\n`;
  });
  
  return output;
}

async function main() {
  const city = process.argv[2] || "Beijing";
  
  console.log(`🔍 正在查询 ${city} 的天气...`);
  
  try {
    const data = await fetchWeather(city);
    console.log(formatWeather(data, city));
  } catch (error) {
    console.error(`❌ 查询失败: ${error.message}`);
    console.log("💡 提示: 请检查城市名称是否正确");
  }
}

main();
```

```bash
node weather.js Beijing
node weather.js "New York"
```

### 项目 3：简易 HTTP 服务器 + REST API（综合级，约 2 小时）

**目标**：综合运用模块化、异步、错误处理、HTTP 协议

```javascript
// server.js — 不依赖任何第三方库的纯 Node.js REST API
const http = require("http");
const url = require("url");

// 内存数据库
let books = [
  { id: 1, title: "JavaScript 高级程序设计", author: "Matt Frisbie", year: 2020 },
  { id: 2, title: "你不知道的 JavaScript", author: "Kyle Simpson", year: 2015 },
];
let nextId = 3;

// 路由处理
const routes = {
  "GET /api/books": (req, res) => {
    sendJSON(res, 200, books);
  },

  "GET /api/books/:id": (req, res, params) => {
    const book = books.find((b) => b.id === parseInt(params.id));
    if (!book) return sendJSON(res, 404, { error: "书籍未找到" });
    sendJSON(res, 200, book);
  },

  "POST /api/books": async (req, res) => {
    const body = await parseBody(req);
    if (!body.title || !body.author) {
      return sendJSON(res, 400, { error: "title 和 author 为必填" });
    }
    const book = { id: nextId++, ...body };
    books.push(book);
    sendJSON(res, 201, book);
  },

  "DELETE /api/books/:id": (req, res, params) => {
    const index = books.findIndex((b) => b.id === parseInt(params.id));
    if (index === -1) return sendJSON(res, 404, { error: "书籍未找到" });
    const deleted = books.splice(index, 1)[0];
    sendJSON(res, 200, { message: "已删除", book: deleted });
  },
};

// 工具函数
function sendJSON(res, status, data) {
  res.writeHead(status, { "Content-Type": "application/json; charset=utf-8" });
  res.end(JSON.stringify(data, null, 2));
}

function parseBody(req) {
  return new Promise((resolve, reject) => {
    let body = "";
    req.on("data", (chunk) => (body += chunk));
    req.on("end", () => {
      try {
        resolve(body ? JSON.parse(body) : {});
      } catch {
        reject(new Error("无效的 JSON"));
      }
    });
  });
}

function matchRoute(method, pathname) {
  for (const [pattern, handler] of Object.entries(routes)) {
    const [routeMethod, routePath] = pattern.split(" ");
    if (method !== routeMethod) continue;

    const routeParts = routePath.split("/");
    const pathParts = pathname.split("/");
    if (routeParts.length !== pathParts.length) continue;

    const params = {};
    const match = routeParts.every((part, i) => {
      if (part.startsWith(":")) {
        params[part.slice(1)] = pathParts[i];
        return true;
      }
      return part === pathParts[i];
    });

    if (match) return { handler, params };
  }
  return null;
}

// 创建服务器
const server = http.createServer(async (req, res) => {
  const { pathname } = url.parse(req.url);
  const method = req.method;

  console.log(`${method} ${pathname}`);

  const route = matchRoute(method, pathname);
  if (route) {
    try {
      await route.handler(req, res, route.params);
    } catch (error) {
      sendJSON(res, 500, { error: "服务器内部错误" });
    }
  } else {
    sendJSON(res, 404, { error: "路由未找到" });
  }
});

const PORT = 3000;
server.listen(PORT, () => {
  console.log(`🚀 服务器运行在 http://localhost:${PORT}`);
  console.log("📚 试试以下命令:");
  console.log(`  curl http://localhost:${PORT}/api/books`);
  console.log(`  curl -X POST -H "Content-Type: application/json" -d '{"title":"新书","author":"作者"}' http://localhost:${PORT}/api/books`);
});
```

---

## 6. 常见陷阱与调试

### 6.1 Top 10 新手错误

**1. `==` vs `===`**
```javascript
// ❌ 宽松比较（会类型转换）
0 == ""      // true 😱
null == undefined  // true 😱

// ✅ 严格比较（推荐始终使用）
0 === ""     // false ✅
null === undefined  // false ✅
```

**2. 变量提升（Hoisting）**
```javascript
// ❌ var 会提升
console.log(x);  // undefined（不报错！）
var x = 5;

// ✅ let/const 不会提升
console.log(y);  // ReferenceError ✅
let y = 5;
```

**3. 异步陷阱**
```javascript
// ❌ forEach 中的 await 不会等待
[1, 2, 3].forEach(async (n) => {
  await doSomething(n);  // 不会按顺序执行！
});

// ✅ 使用 for...of
for (const n of [1, 2, 3]) {
  await doSomething(n);  // 按顺序执行
}

// ✅ 或并行执行
await Promise.all([1, 2, 3].map(n => doSomething(n)));
```

**4. 浮点数精度**
```javascript
// ❌
0.1 + 0.2 === 0.3  // false 😱 (0.30000000000000004)

// ✅
Math.abs(0.1 + 0.2 - 0.3) < Number.EPSILON  // true
```

**5. 数组/对象是引用类型**
```javascript
// ❌ 浅拷贝陷阱
const a = [1, 2, 3];
const b = a;
b.push(4);
console.log(a);  // [1, 2, 3, 4] — a 也被改了！

// ✅ 深拷贝
const c = [...a];           // 展开运算符（浅拷贝）
const d = structuredClone(a); // 深拷贝（推荐）
```

**6. `typeof null` 的 bug**
```javascript
typeof null  // "object" 😱（这是 JS 的历史 bug）

// ✅ 正确判断 null
value === null
```

**7. 回调中的 this 丢失**
```javascript
// ❌
class Timer {
  constructor() { this.seconds = 0; }
  start() {
    setInterval(function() {
      this.seconds++;  // this 不是 Timer！
    }, 1000);
  }
}

// ✅ 使用箭头函数
class Timer {
  constructor() { this.seconds = 0; }
  start() {
    setInterval(() => {
      this.seconds++;  // ✅ 箭头函数继承外层 this
    }, 1000);
  }
}
```

### 6.2 调试技巧

```javascript
// 1. console 家族
console.log("普通日志");
console.error("错误信息");
console.warn("警告信息");
console.table([{ a: 1 }, { a: 2 }]);  // 表格展示
console.time("计时");
// ... 代码 ...
console.timeEnd("计时");  // 计时: 123ms

// 2. debugger 断点
function buggyFunction(data) {
  debugger;  // 在 Chrome DevTools 中会暂停
  return data.map(item => item.name);
}

// 3. Node.js 调试
// node --inspect hello.js
// 然后在 Chrome 打开 chrome://inspect
```

---

## 7. 生态与工具链

### 7.1 包管理器

```bash
# npm（内置）
npm init -y              # 初始化项目
npm install express      # 安装依赖
npm install -D nodemon   # 安装开发依赖
npm run start            # 运行脚本

# pnpm（推荐，更快更省空间）
npm install -g pnpm
pnpm install express
```

### 7.2 必知库/框架（Top 10）

| 库名 | 用途 | 安装命令 |
|------|------|---------|
| **Express** | Web 服务器框架 | `npm i express` |
| **React** | UI 组件库 | `npx create-react-app my-app` |
| **Next.js** | React 全栈框架 | `npx create-next-app` |
| **Vue.js** | 渐进式 UI 框架 | `npm create vue@latest` |
| **Axios** | HTTP 客户端 | `npm i axios` |
| **Lodash** | 工具函数库 | `npm i lodash` |
| **Day.js** | 日期处理 | `npm i dayjs` |
| **Zod** | 数据验证 | `npm i zod` |
| **Jest** | 测试框架 | `npm i -D jest` |
| **ESLint** | 代码检查 | `npm i -D eslint` |

### 7.3 测试

```javascript
// math.test.js（使用 Jest）
const { add, multiply } = require("./math");

describe("数学函数", () => {
  test("加法", () => {
    expect(add(1, 2)).toBe(3);
    expect(add(-1, 1)).toBe(0);
  });

  test("乘法", () => {
    expect(multiply(3, 4)).toBe(12);
  });
});
```

```bash
npx jest
```

---

## 8. 学习路线图

### 🗓️ 第 1 周：基础入门
- [ ] Day 1-2：环境搭建 + 变量、类型、运算符
- [ ] Day 3-4：控制流 + 函数 + 作用域
- [ ] Day 5-6：数组方法 + 对象 + 解构
- [ ] Day 7：完成项目 1（Todo 应用）

### 🗓️ 第 2-4 周：进阶提升
- [ ] Week 2：异步编程（Promise / async-await）+ 错误处理
- [ ] Week 3：模块系统 + 类与原型 + this
- [ ] Week 4：完成项目 2 + 学习 Node.js 基础

### 🗓️ 第 2-3 月：实战深入
- [ ] Month 2：学习 React 或 Vue + 完成项目 3
- [ ] Month 3：学习 Next.js / Nuxt + 个人项目

### 📚 推荐资源

| 类型 | 资源名 | 适合阶段 |
|------|--------|---------|
| 官方文档 | [MDN Web Docs](https://developer.mozilla.org/zh-CN/) | 全阶段 |
| 在线课程 | [freeCodeCamp](https://www.freecodecamp.org/) | 入门 |
| 书籍 | 《JavaScript 高级程序设计》（红宝书） | 进阶 |
| 练习 | [LeetCode](https://leetcode.cn/) / [Codewars](https://www.codewars.com/) | 全阶段 |

---

## 9. 速查备忘录（Cheat Sheet）

```
╔══════════════════════════════════════════════════════════╗
║                 JavaScript 速查卡                        ║
╠══════════════════════════════════════════════════════════╣
║ 变量    let x = 1;  const Y = 2;                        ║
║ 字符串  `Hello ${name}`                                  ║
║ 数组    [1,2,3].map/filter/reduce/find/some/every        ║
║ 对象    { key: value }  解构: const {a, b} = obj         ║
║ 函数    const fn = (a, b) => a + b                       ║
║ 展开    [...arr]  {...obj}                               ║
║ 异步    async/await + try/catch                          ║
║ 模块    import/export                                    ║
║ 判断    === (严格)  typeof  instanceof                    ║
║ 循环    for...of(值)  for...in(键)  .forEach()           ║
║ 空值    ?? (空值合并)  ?. (可选链)                         ║
║ 解构    const {a, b: alias, c = default} = obj           ║
╚══════════════════════════════════════════════════════════╝
```

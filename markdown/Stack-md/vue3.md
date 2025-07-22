# 前端开发

## [Node](https://nodejs.org/zh-cn)

### [pnpm](https://pnpm.io/zh/)

设置阿里镜像源
```vue
pnpm config set registry https://registry.npmmirror.com/
```

### [Koa](https://koajs.com/#introduction)

```vue
app.use：注册中间件（函数），所有请求都会经过这里。
ctx（context）：上下文对象，包含请求和响应的所有信息。
ctx.body：设置响应内容。
```

#### 中间件
```vue
-koa-bodyparser：解析 POST 请求体
-@koa/cors：跨域
-koa-static：静态资源服务
```
#### 异步和错误处理
```vue
app.use(async (ctx, next) => {
  try {
    await next();
  } catch (err) {
    ctx.status = err.status || 500;
    ctx.body = '服务器错误';
  }
});
```

### [Axios](https://www.axios-http.cn/) [express](https://expressjs.com/zh-cn/)

### Typescript

### [TypeORM](https://typeorm.io/)

#### 创建koa-ts-server
```vue
koa-ts-server/
├── src/
│   ├── routes/         # 路由
│   ├── controllers/    # 控制器
│   ├── config/         # 配置
│   ├── middleware/     # 中间件
│   └── index.ts        # 入口文件
├── package.json
└── tsconfig.json
```
#### 初始化、安装依赖
```vue
pnpm init
pnpm add koa koa-router koa-bodyparser
pnpm add -D typescript @types/node @types/koa @types/koa-router @types/koa-bodyparser ts-node nodemon
pnpm add mysql2
```

#### 配置tsconfig.json
```vue
{
  "compilerOptions": {
    "target": "ES2020",
    "module": "commonjs",
    "lib": ["ES2020"],
    "outDir": "./dist",
    "rootDir": "./src",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```
#### 创建入口文件、跨域
```vue
# src/index.ts

import Koa from 'koa';
import Router from 'koa-router';
import bodyParser from 'koa-bodyparser';
import cors from '@koa/cors';

import userRouter from './routes/user';

const app = new Koa();
const router = new Router();

# 配置 cors

app.use(cors({
  origin: '*', // 允许所有来源
  // origin: 'http://localhost:5173', // 或者指定特定域名
  credentials: true, // 允许发送 cookie
  allowMethods: ['GET', 'POST', 'PUT', 'DELETE', 'OPTIONS'], // 设置允许的 HTTP 方法
  allowHeaders: ['Content-Type', 'Authorization', 'Accept'], // 设置允许的 HTTP 头
  exposeHeaders: ['WWW-Authenticate', 'Server-Authorization'] // 设置允许暴露的头
}));

# 其他中间件

app.use(bodyParser());

# 路由

router.get('/', async (ctx) => {
  ctx.body = {
    message: 'Hello Koa + TypeScript!'
  };
});

# 注册路由

app.use(router.routes()).use(router.allowedMethods());
app.use(userRouter.routes()).use(userRouter.allowedMethods());

# 启动服务

const PORT = process.env.PORT || 3000;
app.listen(PORT, () => {
  console.log(`Server running on http://localhost:${PORT}`);
});
```

#### 路由注册
```vue
# src/routes/user.ts

import Router from 'koa-router';
import { getUserList } from '../controllers/user';

const router = new Router({
  prefix: '/api/users'
});

router.get('/', getUserList);

router.get('/', async (ctx) => {
  ctx.body = {
    users: [
      { id: 1, name: 'User 1' },
      { id: 2, name: 'User 2' }
    ]
  };
});

router.post('/', async (ctx) => {
  const user = ctx.request.body;
  ctx.body = {
    message: 'User created',
    user
  };
});

export default router;
```
#### 配置JSON
```vue
# package.json
{
  "name": "koa-ts-server",
  "version": "1.0.0",
  "scripts": {
    "dev": "nodemon",
    "build": "tsc",
    "start": "node dist/index.js"
  }
}

# nodemon.json
{
  "watch": ["src"],
  "ext": ".ts,.js",
  "ignore": [],
  "exec": "ts-node ./src/index.ts"
}
```
#### 数据库配置文件
```vue
# src/config/db.ts

import mysql from 'mysql2/promise';

# 创建连接池
export const pool = mysql.createPool({
  host: 'localhost',      // 数据库地址
  user: 'root',           // 数据库用户名
  password: '你的密码',    // 数据库密码
  database: '你的数据库',  // 数据库名
  port: 3306,             // 端口号，默认3306
  waitForConnections: true,
  connectionLimit: 10,
  queueLimit: 0
});
```
#### 代码中使用
```vue
# src/controllers/user.ts
import { Context } from 'koa';
import { pool } from '../config/db';

export const getUserList = async (ctx: Context) => {
  try {
    const [rows] = await pool.query('SELECT * FROM users');
    ctx.body = {
      code: 0,
      data: rows
    };
  } catch (error) {
    ctx.body = {
      code: 1,
      message: '数据库查询失败',
      error
    };
  }
};
```

## Vue3

### 表格数据请求

```vue
  后端配置数据库、开放响应接口
  前端配置跨域、生成请求接口、组件中导入调用接口
  ```

### 钩子函数

```vue
  onMounted 钩子，组件挂载后获取数据
  computed 是一个计算属性
  数据查找过滤:前端过滤、后端过滤
```

### 组件注册

### 生命周期



## Midway框架

### 

```vue
  Controller（控制器）
    处理HTTP请求，是API接口的入口
    接收前端请求参数
    调用Service层处理业务逻辑
    返回处理结果给前端

  Entity（实体）
    定义数据库表结构，映射数据库表
    定义表字段及其类型
    设置字段的验证规则
    定义字段的默认值
    配置字段的索引

  Service（服务）
    处理业务逻辑
    处理数据验证
    调用数据库操作
    处理事务
```

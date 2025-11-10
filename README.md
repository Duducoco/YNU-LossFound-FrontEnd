# YNU-Loss-Found 校园失物招领系统

一个帮助校园师生快速找回遗失物品的失物招领网站。用户可以发布寻物启事或招领启事，系统支持智能邮箱提醒功能，让失物更快回到失主手中。

**技术栈**: Vue 3 + Element Plus + Vue Router + Vuex + Axios + 阿里云 OSS

**后端仓库**: [AlphaGogoo/YNU-LossFound-BackEnd](https://github.com/AlphaGogoo/YNU-LossFound-BackEnd)

## 核心功能

### 用户认证
- **注册/登录**: 支持用户注册和登录，基于 token 的身份验证
- **个人中心**: 查看和修改个人信息、修改密码

### 发布启事
- **寻物启事**: 丢失物品的用户可发布寻物信息（物品名称、丢失时间/地点、图片、联系方式）
- **招领启事**: 拾到物品的用户可发布招领信息
- **图片上传**: 支持上传物品图片，使用阿里云 OSS 存储

### 智能提醒
- **邮箱通知**: 发布招领启事时，若填写了失主的学号/手机号/邮箱，系统会自动发送邮件通知失主
- **快速联系**: 邮件中包含拾取者的联系方式，方便失主快速取回物品

### 信息广场
- **寻物广场**: 浏览所有寻物启事
- **招领广场**: 浏览所有招领启事
- **我的发布**: 查看和管理自己发布的寻物/招领信息

## 快速开始

### 前置要求
- Node.js
- npm
- 阿里云 OSS 账号（用于图片存储）

### 安装步骤

1. 克隆项目到本地
```bash
git clone git@github.com:AlphaGogoo/YNU-LossFound-FrontEnd.git
cd YNU-LossFound-FrontEnd
```

2. 安装依赖
```bash
npm install
```

3. 配置阿里云 OSS

编辑 `src/utils/index.js` 文件中的 `createOSSClient()` 函数，填入你的 OSS 配置：

```js
export function createOSSClient() {
    return new OSS({
        bucket: 'your-bucket-name',      // 你的 bucket 名称
        region: 'your-region',           // 例如: oss-cn-beijing
        accessKeyId: 'your-access-key',
        accessKeySecret: 'your-secret-key'
    })
}
```

4. 启动开发服务器
```bash
npm run serve
```

项目将运行在 `http://127.0.0.1:8080`，API 请求会自动代理到后端 `http://127.0.0.1:8888`

### 其他命令

**构建生产版本**
```bash
npm run build
```

**代码检查**
```bash
npm run lint
```

## 项目结构

```
src/
├── views/          # 页面组件
│   ├── Lost.vue    # 寻物广场
│   ├── Found.vue   # 招领广场
│   ├── Post.vue    # 发布启事
│   ├── Me.vue      # 个人中心
│   ├── Login.vue   # 登录
│   └── Register.vue # 注册
├── components/     # 业务组件
├── router/         # 路由配置
├── store/          # Vuex 状态管理
├── request/        # API 请求封装
├── utils/          # 工具函数
└── assets/         # 静态资源
```

## 开发说明

- 使用 Vue 3 Composition API 和 Options API
- UI 组件库使用 Element Plus
- 路由采用 Hash 模式
- 使用 sessionStorage 存储用户 token
- 需要登录的页面通过路由守卫保护

## License

MIT
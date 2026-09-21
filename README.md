# 淘宝订单详情页复刻（静态网页）

复刻淘宝/电商"交易成功"订单详情页的单文件静态网页，支持动态配置核心字段，可直接部署到 Render。

## 文件结构

```
├── index.html        # 页面（HTML + CSS + 原生 JS，单文件）
└── img/product.jpg   # 默认商品图
```

## 动态配置方式（三选一）

### 1. URL 查询参数（部署后最方便，无需改代码）

```
https://你的域名.onrender.com/?title=商品标题&price=9.9&origPrice=19.9&name=张三&phone=138****8888&address=广东省 佛山市 南海区 XXX&createTime=2026-09-01 16:39:46&img=https://xxx.com/a.jpg&orderId=123456&shopName=某某旗舰店
```

支持的参数：

| 参数 | 说明 | 默认值 |
|---|---|---|
| `img` / `image` | 商品图片 URL | img/product.jpg |
| `title` | 商品标题 | 波点发夹标题 |
| `spec` | 商品规格 | 蓝咖撞色波点BB夹【四件套】 |
| `qty` | 数量 | 1 |
| `price` | 实付价 | 4.99 |
| `origPrice` | 原价 | 5.99 |
| `discount` | 共减金额 | 1 |
| `name` | 收货人 | 困 |
| `phone` | 电话 | 86-189****0880 |
| `address` | 收货地址 | 广东省 佛山市 南海区 里水镇… |
| `orderId` | 订单号 | 5127217527457057230 |
| `tradeNo` | 支付宝交易号 | 2026090123… |
| `payMethod` | 支付方式 | 支付宝支付 |
| `createTime` / `payTime` / `shipTime` | 创建/付款/发货时间 | 2026-09-01 … |
| `shopName` / `shopDesc` | 店铺名称 / 描述 | 万千少女梦 |
| `status` | 订单状态 | 已签收 |

> 不传 `discount` 时，「共减」会按 `原价 - 实付价` 自动计算。

### 4. 配置面板里生成分享链接

点配置面板的「生成配置链接并复制」，会把当前所有非默认值拼成 URL 参数复制到剪贴板，直接发给别人即可复现同一份数据。

### 2. 内置配置面板

点击页面右下角 **⚙ 按钮**，表单填写（支持上传本地图片），保存后写入浏览器 localStorage，立即生效。

### 3. 编辑代码默认值

修改 `index.html` 顶部 `<script>` 中的 `DEFAULTS` 对象。

## 部署到 Render（静态站点）

1. **推送到 GitHub**：
   ```bash
   git init
   git add .
   git commit -m "init: taobao order page replica"
   git remote add origin https://github.com/<你的用户名>/<仓库名>.git
   git push -u origin main
   ```
2. 登录 [render.com](https://render.com) → **New** → **Static Site**
3. 连接刚才的 GitHub 仓库
4. 构建设置：
   - **Build Command**：留空
   - **Publish Directory**：`./`（仓库根目录）
5. 点 **Create Static Site**，几十秒后得到 `https://xxx.onrender.com` 地址
6. 用 URL 参数即可动态展示不同订单数据，例如：
   `https://xxx.onrender.com/?title=测试商品&price=9.9`

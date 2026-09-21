# 淘宝订单详情页生成器（静态网页）

复刻淘宝/电商「交易成功」订单详情页，**配置页 + 详情页** 双页结构，支持动态配置核心字段，可直接部署到 Render。

## 文件结构

```
├── index.html        # 配置页：填表单 → 点「生成订单详情」→ 跳转详情页
├── order.html        # 详情页：淘宝订单页复刻，纯 URL 参数驱动
└── img/product.jpg   # 默认商品图
```

## 使用流程

1. 打开 `index.html`（配置页）
2. 填写：**商品图**（URL 或上传本地图片）、**商品标题**、**金额**（实付/原价）、**收货地址**、**下单时间**（创建/付款/发货）、订单号、店铺名、订单状态
3. 表单改动时右侧（桌面端）自动实时预览；移动端点右下「预览效果」抽屉查看
4. 点 **「生成订单详情」** → 跳转到 `order.html?...` 完整还原页面
5. 点 **「复制链接」** → 复制带全部参数的详情页链接，发给任何人看到的都是同一份数据
6. 详情页右下「✎ 编辑数据」可回到配置页继续修改再生成

## 动态配置字段

支持 URL 参数（`order.html?title=商品名&price=9.9&...`）与配置页表单两种方式，字段一致：

| 参数 | 说明 | 默认值 |
|---|---|---|
| `img` / `imageUrl` | 商品图片 URL（或 base64） | img/product.jpg |
| `title` | 商品标题 | 波点发夹标题 |
| `spec` | 商品规格 | 蓝咖撞色波点BB夹【四件套】 |
| `qty` | 数量 | 1 |
| `price` | 实付金额 | 4.99 |
| `origPrice` | 原价 | 5.99 |
| `discount` | 共减金额（不传则按 原价−实付价 自动算） | 自动 |
| `name` / `phone` | 收货人 / 电话 | 困 / 86-189****0880 |
| `address` | 收货地址 | 广东省 佛山市 南海区 里水镇… |
| `orderId` | 订单号（配置页可一键随机生成） | 5127217527457057230 |
| `tradeNo` | 支付宝交易号 | 2026090123… |
| `payMethod` | 支付方式 | 支付宝支付 |
| `createTime` / `payTime` / `shipTime` | 下单/付款/发货时间 | 2026-09-01 … |
| `shopName` / `shopDesc` | 店铺名称 / 描述 | 万千少女梦 |
| `status` | 订单状态 | 已签收 |

## 部署到 Render（静态站点）

1. **推送到 GitHub**：
   ```bash
   git init   # 本仓库已初始化
   git add .
   git commit -m "init"
   git remote add origin https://github.com/<你的用户名>/<仓库名>.git
   git push -u origin main
   ```
2. 登录 [render.com](https://render.com) → **New** → **Static Site**
3. 连接刚才的 GitHub 仓库
4. 构建设置：
   - **Build Command**：留空
   - **Publish Directory**：`./`（仓库根目录）
5. 点 **Create Static Site**，几十秒后得到 `https://xxx.onrender.com`
6. 打开首页即配置页；详情链接形如 `https://xxx.onrender.com/order.html?title=测试&price=9.9`

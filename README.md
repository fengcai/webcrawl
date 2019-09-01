# QQ微信 112908676
# 下载地址
2019.08.30 版本2.4.0 ，下载地址：https://share.weiyun.com/5hmFnXA

**<font color=red>下载结束如遇360弹出压缩包解密提醒，请直接取消忽略</font>**

![360提示请取消](https://github.com/fengcai/webcrawl/blob/master/cancel1.png "360提示请取消")
# 注意
1. 不建议在云主机上使用下单软件，可能会遇到这个问题，请点击[链接](https://bbs.aliyun.com/read/589025.html?page=e "链接")
2. 所用账号至少有一个收货地址
3. 自动付款需要同时设置支付密码，并保证余额足够支付订单，支付失败将无法继续下一单
4. 由于软件内核的问题，如果使用的是有店铺的卖家账户登录的淘宝，有可能无法正常下单，近期无计划修复
5. 自动下单的前提：已登录淘宝，至少提供购买商品链接以及购买数量
6. 因为没有定时器，所以暂时不支持秒杀抢购等场景
7. Excel单元格中的内容不能出现回车换行
8. 大部分第一次使用不成功的主要原因是Excel文件的结构与tb_order_in.js不一致导致的，请注意检查
# 操作视频
2019.03.07更新
- 优酷：https://v.youku.com/v_show/id_XNDA4OTE2OTE1Mg==.html
- YouTube：https://youtu.be/YL9-VTuarSs
# 功能简介
- 多账号登录（通过多开）
- 批量自动下单
- 自动打开商品页（支持淘宝联盟链接地址）
- 自动选择SKU属性
- 一键格式化收货地址（单次购买时）
- 支持导入自定义格式的Excel格式（批量下单时）
- 自动过滑动验证码（限收费版）
- 自动领取优惠券
- 自动选择购买数量
- 自动修改收件人及地址信息
- 自动留言
- 自动提交
- 自动付款（可选）
- 自动备注（待开发）
# 使用步骤
## 进入工具导航，选择自动下单（Excel）版
![auto_buy](https://github.com/fengcai/webcrawl/blob/master/auto_buy.png "auto_buy")
## 进入自动下单软件后，点击设置
![点击设置](https://github.com/fengcai/webcrawl/blob/master/auto_buy_setting.png "点击设置")
## 导入批量下单文件
![打开](https://github.com/fengcai/webcrawl/blob/master/import_buy.png "打开")
## 查看导入的数据
![check](https://github.com/fengcai/webcrawl/blob/master/listed_order.png "check")
## 批量下单设置
- 设置完了，直接点击`立即购买`（或`加入购物车`按钮即可）
- 自动付款需要勾选自动付款项并同时提供付款密码
- 需要自行保证付款方式有足够的资金，否则付款失败，软件会自动停止
![setting](https://github.com/fengcai/webcrawl/blob/master/buy_setting.png "setting")

# Excel文件格式说明
- 每个Excel的第一行默认表示列名称，请自行对照示例文档
- `\root_crawl\tb_order_in.js`中的名称必须与Excel中相应的列名称一致，可以自行根据实际情况修改
- 如下代码块表示文件`\root_crawl\tb_order_in.js`表示支持的列名称预定义
```javascript
/*
 自动下单，本地读取Excel的设置
 由于是通用的设置，所以Excel列只需要根据需要提供即可
 比如自动下单Excel需要的列：订单编号/商品/SKU/数量....
 比如自动备注Excel需要的列：订单编号/备注...
 比如自动退款Excel需要的列：订单编号/退款描述
*/
var buy_local_setting =
{
  //            列定义   : 列名称，这里的列名称要跟excel中的列名称一模一样
              "order_id": "订单编号" // 订单编号
    ,            "title": "标题"
    ,              "sku": "SKU"   // 有的商品没有sku
    ,         "quantity": "数量"
    ,      "coupons_url": "优惠券"  // 优惠券链接
    ,         "item_url": "商品"    // 商品链接
    ,  "recharge_mobile": "充值号码"  // QQ号，或手机号，或其他号码
    ,    "receiver_name": "收货人姓名"
    ,   "receiver_phone": "收货手机"
    , "receiver_address": "收货地址"  // 此处的地址不包括收件人姓名，手机号，如：江苏省 南京市 建邺区 虹苑新寓四村
    ,     "full_address": "地址信息"  // 完整的收货地址信息，如：孙悟空,13800138000,江苏省 南京市 建邺区 虹苑新寓四村,000000
    ,         "province": "省"        // 有的平台可以分类导出地址信息
    ,             "city": "市"
    ,           "county": "区"
    ,           "street": "街道"
    ,      "addr_detail": "详细地址"
    ,          "message": "买家留言"  // 如果需要购买时填写到订单里，需要提供此内容
    ,             "flag": "备注（颜色）" // 红色/黄色/绿色/蓝色/紫色
    ,             "memo": "备注（文字）" // 订单购买后需要标记备注，需要提供此内容
    ,      "rate_status": "评价"
    ,      "refund_type": "退款类型" // 可选，仅退款，退货退款
    ,       "good_state": "商品状态"  // 可选，仅退款的话，需要提供商品状态，未收到货，已收到货
    ,    "refund_reason": "退款原因" // 可选
    ,      "refund_desc": "退款说明"
};
```
## 优惠券
- 目前软件可以处理的优惠券有两类，分别是店铺优惠券和商品优惠券
- 店铺券需要同时提供店铺券的URL和所购商品的URL
- 商品券可以只提供商品券的URL
### Excel中填写示例
![优惠券设置](https://github.com/fengcai/webcrawl/blob/master/quan_excel.png "优惠券设置")
## 购买商品
如下图中箭头所指，取自商品页面浏览器的地址栏，根据该链接软件可以直接进入商品页开始购买
支持淘宝联盟链接，如https://s.click.taobao.com/b9EB9Mw
![商品链接](https://github.com/fengcai/webcrawl/blob/master/product_link.png)
## SKU格式
### 正确的格式
3XL;K9805黑白色(短裤)
### 错误的格式
k9805黑白色(短裤）；3XL
### 错误原因：
- 分隔符使用了中文的分号
- SKU中的英文字母与淘宝的大小写不符，括号不符
### 注意
- 没有SKU的商品，不填即可
- 多个SKU的顺序可以任意，比如上面的，写成尺码;颜色或颜色;尺码都不影响软件的处理
- 多个SKU使用英文标点分号; 进行分组分割，不能使用中文标点
- 你提供的SKU与淘宝商品SKU必须完全一致，比如英文大小写，中英文标点符号
SKU数据取自如下图中，对于没有SKU的不填内容即可

![正确的SKU](https://github.com/fengcai/webcrawl/blob/master/right_sku.png "正确的SKU")
## 收件地址
### 格式一
姓名,手机号,省 市 区县 街道 详细地址门牌号,邮政编码
#### 示例
孙悟空,13800138000,江苏省 南京市 建邺区 虹苑新寓四村,000000
#### 对应的Excel设置
![示例1](https://github.com/fengcai/webcrawl/blob/master/full_address.png "示例1")
### 格式二
#### 对应的Excel设置
![分开的地址](https://github.com/fengcai/webcrawl/blob/master/split_address.png "分开的地址")
## 使用默认收件地址
在Excel文件中不提供相应的列即可

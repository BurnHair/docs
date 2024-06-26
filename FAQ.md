# 1. 如何使用
**也可以点击令牌右侧的 “聊天” 按钮使用**

## 登录
* 使用 GitHub 账号即可登录
* 您也可以通过[购买任意金额的兑换码](https://shop.burn.hair/)，使用订单编号和兑换码登录

## 创建令牌

令牌 - 添加新的令牌。
<img src="https://assets.burn.hair/token.png" width="100%" />

添加成功之后，回到上级页面复制你的 token  
<img src="https://assets.burn.hair/use_token.png" width="100%" />


## 调用 API
[参考文档](https://github.com/BurnHair/docs)

# 2. 怎么签到
[网站](https://burn.hair/check_in) 和[机器人](https://t.me/burn_hair_bot)均可签到。

# 3. 如何充值

到这里🫱 [兑换码购买](https://shop.burn.hair/)

支持 TRX、银行卡、支付宝、 Google Pay和Apple Pay。购买后得到 key，去[充值页面](https://burn.hair/topup)激活即可
<img src="https://assets.burn.hair/topup.png" width="100%" />

# 4. 访问不稳定
* 如有需要，我通常会在北京时间的凌晨1-2点更新服务，这个时间段内可能请求会有少量失败
* 有些时候请求会失败，再试一次也许就好了
* 本站使用了 Cloudflare，如果您遇到不稳定、断流等问题，可能需要自行解决网络问题，也可私聊我了解详情


# 5. 为什么日志里显示的模型来回变？我明明只使用4
如果你用 NextChat 的话，这是正常的，NextChat 有一个功能会[自动生成 title](https://github.com/BurnHair/issues/issues/8#issuecomment-2024848273)，默认模型就是 3.5 

# 6. 计费规则
与官方计费规则一样，按照提示和补全计费。以下图为例：
<img width="597" alt="pricing" src="https://github.com/BurnHair/docs/assets/14024832/dc712e0c-3256-49e0-b80b-2153a9994ba2">
```
>>> 2415/1000000*0.5+498/1000000*1.5
.0019545000
```
# 7. 免费用户和付费用户的区别
目前免费用户的QPS（每秒请求次数）为10，付费用户为50。需要更多并发请发邮件或私聊我。

# 8. 如何判断是否支持 function call
可以[看这里](https://github.com/orgs/BurnHair/discussions/110)

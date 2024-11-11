# 1. 网址
## OpenAI
https://bunr.hair

## 非 OpenAI，包含 Anthropic Claude，更多模型添加中
https://api.burn.hair


# 2. 如何使用
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
[参考文档](https://github.com/BurnHair/docs) 或 使用 ChatGPTNextWeb 和 LobeChat

# 3. 怎么签到
[网站](https://burn.hair/check_in) 和[机器人](https://t.me/burn_hair_bot)均可签到。

# 4. 如何充值
直接在令牌页面购买，免去兑换步骤，使用加密货币充值更可加赠 10%

或[兑换码购买](https://shop.burn.hair/)，支持银行卡、支付宝、 Google Pay和Apple Pay。购买后得到 key，去[充值页面](https://burn.hair/topup)激活即可
<img src="https://assets.burn.hair/topup.png" width="100%" />


# 5. 访问不稳定
* 有些时候请求会失败，再试一次就好了
* 本站使用了 Cloudflare，如果您遇到不稳定、断流等问题，可能需要自行解决网络问题
* 也可以使用中国大陆加速地址 `https://cn-test.burn.hair`

# 6. 为什么日志里显示的模型来回变？我明明只使用4
如果你用 NextChat 的话，这是正常的，NextChat 有一个功能会[自动生成 title](https://github.com/BurnHair/issues/issues/8#issuecomment-2024848273)，默认模型就是 3.5 

# 7. 计费规则
与官方计费规则一样，按照提示和补全计费。以下图为例：
<img width="597" alt="pricing" src="https://github.com/BurnHair/docs/assets/14024832/dc712e0c-3256-49e0-b80b-2153a9994ba2">
```
>>> 2415/1000000*0.5+498/1000000*1.5
.0019545000
```

# 8. 免费用户和付费用户的区别
只有主站 https://burn.hair 才有区别
* 对于聊天：目前免费用户的QPS（每秒请求次数）为2，付费用户为30。
* 对于非聊天，两者分别为1/10

对于小分队 https://api.burn.hair 没有用户分组

# 9. 小分队如何切换用户分组
令牌 - 编辑 - 令牌分组，有如下对应关系
* default：默认分组，第三方接口
* vip： Anthropic Claude 官方接口

# 10. 如何判断是否支持 function call
可以[看这里](https://github.com/BurnHair/docs/blob/master/函数调用.md)

# 11. 汇率
加密货币的汇率均是10分钟更新一次；法币的汇率为1天更新一次

# 12. 内容审查
我们会选择性的把输入内容发送给 Mistral AI、Google Cloud Compute 或 OpenAI 来进行文本安全审查，此请求不包含个人信息。

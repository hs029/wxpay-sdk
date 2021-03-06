微信支付 Java SDK
------

2018最新最全微信支付集成SDK，一行代码调用微信支付，更多丰富接口注释和例子，包含基础支付功能（网页授权、各种签名、统一下单、退款、对账单、用户信息获取）、验收用例指引（沙箱支付、支付验收、免充值产品开通）、商户平台（现金红包、企业付款到用户、代金券或立减优惠）、公众平台（微信卡券、社交立减金活动）、小程序（生成永久二维码、发送模版消息）等等功能。

本项目依托于 [微信支付开发者文档](https://pay.weixin.qq.com/wiki/doc/api/index.html)，对文档中的接口进行二次封装，从而为小伙伴们提供一个`拿来即用`的支付sdk工具。

相关的sdk文档已经更新，请进入以下地址查看：

文档地址：https://yclimb.gitbook.io/wxpay

gitbook：https://github.com/YClimb/wxpay-gitbook


## 如何接入自身项目？

```
现在一般是有两种方式，pom 引用 jar 包和直接 copy，详情如下：

1.第一种是直接把当前项目 clone 下来当作一个支付中间件，修改关键的支付参数后 deploy 到个人或者公司的私服中去，其他项目引用 jar 包；
2.第二种是直接把我的 sdk 中 java 下的目录和文件拷贝到你的项目中，放到 java 项目路径下；

释：两种方式各有利弊，jar 方式比较灵活，独立项目，但是修改参数要注意历史版本兼容和及时推包到私服，否则报错；
直接拷贝的方式就比较简单，不独立，修改起来方便，但是如果有多个公众号或者小程序，或者多个项目需要使用，则需要拷贝到多个项目中，麻烦不容易管理，比较复杂；
具体如何选择，看朋友们自身项目决定吧，建议公司级别项目使用第一种，更弹性可扩展。
```

## 项目结构
首先需要简单说明整个 `wxpay-sdk` 的项目结构，主体结构如下所示：
    
    - wxpay-sdk
        - src
            - main
                - java
                    - com.weixin.pay
                        - card              // 微信卡券
                        - constants         // 常量文件
                        - redis             // redis工具类
                        - util              // 支付工具类（支付、签名、加密解密）
                        - xxx class         // 支付实体类，基础配置信息
                - test
                    - controller
                        - xxx class         // 测试的相关类
        - .gitignore
        - pom.xml                           // 引用包
        - README.md
        



提供微信支付的基础功能，脱胎于微信官方Java-SDK，进行二次封装后，提供一系列的方法；
基础方法主要在 `com.weixin.pay.WXPay` 、 `com.weixin.pay.util.WXUtils`类下，此项目包含的微信支付功能主要分为以下几个部分，这里列举一些主要功能，具体的详细功能查询作者gitbook或者公众号查看。

### 1. 基础支付功能

 `com.weixin.pay.WXPay` ：
 
 |方法名 | 说明 |
 |--------|--------|
 |microPay| 刷卡支付 |
 |unifiedOrder | 统一下单|
 |chooseWXPayMap | 微信支付二次签名|
 |orderQuery | 查询订单 |
 |reverse | 撤销订单 |
 |closeOrder|关闭订单|
 |refund|申请退款|
 |refundQuery|查询退款|
 |downloadBill|下载对账单|
 |report|交易保障|
 |shortUrl|转换短链接|
 |authCodeToOpenid|授权码查询openid|

    

### 2. 验收用例

支付验收指引：`https://pay.weixin.qq.com/wiki/doc/api/jsapi.php?chapter=23_1`

 `controller.TestWXPay` ：
 
 |方法名 | 说明 |
 |--------|--------|
 |unifiedOrder | 统一下单|
 |orderQuery | 查询订单 |
 |reverse | 撤销订单 |
 |closeOrder|关闭订单|
 |refund|申请退款|
 |refundQuery|查询退款|

### 3. 商户平台-现金红包

 `com.weixin.pay.WXPay` ：
 
 |方法名 | 说明 |
 |--------|--------|
 |sendRedPack| 企业向指定微信用户的openid发放指定金额红包 |
 |getRedPackInfo| 查询红包记录 |

### 4. 商户平台-代金券或立减优惠

 `com.weixin.pay.WXPay` ：
 
 |方法名 | 说明 |
 |--------|--------|
 |sendCoupon| 发放代金券 |
 |queryCouponsInfo| 查询代金券信息 |
 |queryCouponStock| 查询代金券批次 |

### 5. 公众平台-微信卡券

 `com.weixin.pay.util.WXUtils` ：
 
 |方法名 | 说明 |
 |--------|--------|
 |getAccessToken| 获取微信全局accessToken |
 |getJsapiAccessTokenByCode| 网页授权获取用户信息时用于获取access_token以及openid |
 |getJsapiUserinfo| 通过access_token和openid请求获取用户信息 |
 |getWxCardApiTicket| 获取卡券 api_ticket 的 api |
 |getWxApiTicket| 获取卡券 api_ticket 的 api |

### 6. 公众平台-社交立减金活动

 `com.weixin.pay.util.WXUtils` ：
 
 |方法名 | 说明 |
 |--------|--------|
 |getCardList| 根据代金券批次ID得到组合的cardList |
 |createCardActivity| 创建支付后领取立减金活动接口 |


### 7. 小程序

 `com.weixin.pay.util.WXUtils` ：
 
 |方法名 | 说明 |
 |--------|--------|
 |getMiniBaseUserInfo| 获取小程序静默登录返回信息 |
 |getWxMiniQRImg| 生成带参数的小程序二维码[] |

## 微信支付调用示例

具体示例及文章可以查看作者的sdk文档，地址如下：

文档地址：https://yclimb.gitbook.io/wxpay

或者在本文末扫码关注作者微信公众号，加作者微信&加入讨论群与大家一起讨论。

 `微信公众号网页授权` ：
```$xslt
https://yclimb.gitbook.io/wxpay/pay/authorize
```

 `统一下单接口` ：

```$xslt
public Map<String, String> saveWxPayUnifiedOrder(Payment payment, User user) throws Exception {
    if (payment == null) {
        return null;
    }
    if (user == null) {
        return null;
    }

    // 1.调用微信统一下单接口
    WXPay wxPay = new WXPay(WXPayConfigImpl.getInstance());
    Map<String, String> resultMap = wxPay.unifiedOrder(...);

    // 1.1.记录付款流水
    ...

    // 下单失败，进行处理
    if (WXPayConstants.FAIL.equals(resultMap.get(WXPayConstants.RETURN_CODE)) ||
            WXPayConstants.FAIL.equals(resultMap.get(WXPayConstants.RESULT_CODE))) {

        // 处理结果返回，无需继续执行
        resultMap.put(WXPayConstants.RESULT_CODE, WXPayConstants.FAIL);
        resultMap.put(WXPayConstants.ERR_CODE_DES, resultMap.get(WXPayConstants.RETURN_MSG));
        return resultMap;
    }

    // 1.2.获取prepay_id、nonce_str
    String prepay_id = resultMap.get("prepay_id");
    String nonce_str = resultMap.get("nonce_str");

    // 2.根据微信统一下单接口返回数据组装微信支付参数，返回结果
    return wxPay.chooseWXPayMap(prepay_id, nonce_str);
}
```

 `支付结果通知` ：
```$xslt
https://yclimb.gitbook.io/wxpay/pay/wxnotify
```

 `查询订单和关闭订单` ：
```$xslt
https://yclimb.gitbook.io/wxpay/pay/orderquery
```

 `申请退款、退款回调接口、查询退款` ：
```$xslt
https://yclimb.gitbook.io/wxpay/refund/refund
```


    
基础调用方式如上所述，统一返回值为 `Map<String, String>`，详细信息见实体类，文档会实时更新，尽情期待！！！
    
    
关注作者微信公众号，点击下方`讨论群`，扫码即可加入`微信支付讨论群`与小伙伴一起探讨哦～
---

![关注我的公众号](https://img-blog.csdn.net/20180130111432962?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvWUNsaW1i/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

---



## License
BSD

# 微信小程序

## 是否可以跳转到公众号
1. 登录小程序后台 设置>关联设置>关联公众号
2. [可以出现组件的场景](https://developers.weixin.qq.com/miniprogram/dev/component/official-account.html)
  * 当小程序从扫二维码场景（场景值1011）打开时
  * 当小程序从扫小程序码场景（场景值1047）打开时
  * 当小程序从聊天顶部场景（场景值1089）中的「最近使用」内打开时，若小程序之前未被销毁，则该组件保持上一次打开小程序时的状态
  * 当从其他小程序返回小程序（场景值1038）时，若小程序之前未被销毁，则该组件保持上一次打开小程序时的状态

# 微信公众号

## 微信分享
  > 常见问题
  * history模式需要每次都进行授权配置
  * 页面location.href与配置的路径可能不符合， 需要alert比对
  * 分享后链接会多参数 ?from= 需要执行 replace(/\?.*#/, '?#')

## 微信支付
  * ?#/ 请在hash前加入?号不然有可能支付失败

## 跳转关注公众号
  * http://mp.weixin.qq.com/mp/getmasssendmsg?__biz=[公众号]==#wechat_webview_type=124&wechat_redirect
  * `biz后的[公众号] 需要通过pc访问需要跳转的公众号页面负责链接查看到`

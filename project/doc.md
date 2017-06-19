## 项目简介

### 业务关系

申请单 1:n 票据单（付款、收款） 1:1 订单


表：user_auth
设置联合唯一：UNIQUE (`auth_type`, `auth_key`)
被锁定，被删除的用户不能再用此账号重复注册。


账号绑定
```
会员主账号
绑定第三方
一个主账号只能绑定一种类型的一个三方账号
一种类型的一个三方账号也只能绑定一个主账号
```


会员层级（membership）
MongoDB 单个文档有16M的限制，内嵌不要太多，可以用引用替代
如下，仅仅保留父节点id即可
```
{
    "user_id": "",
    "user_pid": "",
}
```

会员登录日志（login_log_member）
```
{
    "user_id": "",
    "time": "",
    "ip": "",
}
```

后台登录日志（login_log_admin）
```
{
    "user_id": "",
    "time": "",
    "ip": "",
}
```

后台操作日志（operation_log_admin）
```
{
    "admin_id": "",
    "op_type": "",
    "op_content": "",
    "time": "",
    "ip": "",
}
```

### 用户中心

用户等级
统计条（钱包，积分）
快捷入口
图片上传
邀请
激活

### 用户订单

列表进入详细页面
订单详细页面内容：
订单信息（创建时间，金额）
对方银行信息（收款、付款）


### 系统配置


### 新增单据


## 利息配置

申请类型钱包余额变化    申请成功    生成订单    订单支付    订单确认

投资申请钱包余额变化    余额不变    余额不变    奖励利息    余额不变    15天后本息进入钱包（扣除锁定金额） （上一级，上两级，上三级）推广利息
提现申请钱包余额变化    余额减少    余额不变    余额不变    奖励利息


投资申请：推送延时队列，15天后如果订单确认成功，本息进入钱包，
apply_interest_on_principal
{'user_id': 0, 'apply_put_id': 0, 'apply_time': ''}


订单支付：


订单确认逻辑：
判断是否满足奖励规则：奖励
判断是否满足惩罚规则：惩罚
执行确认
投资方计算上级推广利息（三级）



打款，确认 产生的 收益变化，积分变化


留言，投诉

时间配置，修改了没有小效果，队列创建的时候就定死了


实名认证接口
http://www.apistore.cn/data/?k=%E5%AE%9E%E5%90%8D

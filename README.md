**前言**

Safety_monitoring 工具，算是我使用java写的第一个安全监测工具。

目前为第一版，故存在很多的不足，在以后会慢慢的进行完善。

**功能介绍**

现有功能主要有6个，分别为：

- ssh端口被爆破预警

- 异地登录（省份）预警
- 非常用登陆IP预警
- 非白名单登录地址预警
- 非常用账号登录预警
- 非常用登陆时间预警

发生异常情况，主要通过邮件进行告警通知，所以有一点需要注意的就是，个人外网主机25端口不能被屏蔽。

注意：又更新了一版，因不可抗拒因素，导致无法开启25端口的可以使用 Safety_monitoring1.jar 版本的，该版本使用ssl的465端口进行发信。

**使用截图**

![1](https://raw.githubusercontent.com/shiyan-520/Safety/master/img/1.png)

![2](https://raw.githubusercontent.com/shiyan-520/Safety/master/img/2.png)

**使用方法**

由于工具目前只支持linux系统主机，所以建议使用任务计划进行周期性检测，参考设置如下：

```java
输入命令
        crontab -e
建议默认使用任务检测计划    
        */5 * * * * java -jar /home/shiyan/Safety/Safety_monitoring.jar 2
        * */1 * * * java -jar /home/shiyan/Safety/Safety_monitoring.jar 3
        每5分钟检测一下是否有恶意用户爆破，每1小时检测下是否有非本省用户登录成功
        
根据需求添加任务计划
        * */1 * * * java -jar /home/shiyan/Safety/Safety_monitoring.jar 4,6,7

```

参数1，也就是日志记录功能目前还未实现，其它参数均已实现。

**相关配置信息**

（以下列出的配置信息为部分可修改的配置信息，其余未展示的配置参数无修改）

cat /home/shiyan/Safety/properties/mailconfig.properties

```properties
# 发件人地址
senderAddress = xxx@qq.com
# 收件人地址
recipientAddress = xxx@qq.com
# 发件人账户名
senderAccount = xxx@qq.com
# 发件人账户密码
senderPassword = xxxxxx
# 发信人的服务器地址
senderServerPathParameter = smtp.qq.com
```

cat /home/shiyan/Safety/properties/testingconfig.properties

```properties
# 特权用户白名单
privilegedUserWhiteList = root,shiyan
# 高危风险频次数
highRiskFailureTimes = 3
# 登录地区白名单（以省份为标准）
regionWhiteList = 河南
# 常用登陆地址
commonLoginAddress = 安阳,郑州
# 常用登陆IP
commonLoginIp = 127.0.0.9
# 常用登陆账号
commonLoginAccounts = shiyan
# 正常操作时间区间
commonLoginTime = 20:00:00-21:00:00
```

**后续优化信息**

1. 增加操作日志记录功能
2. 增加缓存机制，减少网络请求
3. 优化现有代码，使其更加简洁
4. 按需求新增新的安全监测点
5. 对异常情况产生的报错信息进行美化

**个人联系方式**

如果有好的功能需求可以发我邮箱：

mail：506130869@qq.com



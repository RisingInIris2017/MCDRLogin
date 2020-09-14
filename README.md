# MCDRLogin - 基于 MCDR 的 MARYT 服务器登录插件
Auth/Login plugin for MCDR
## 逻辑设计
1. 当玩家登录时，获取玩家的 UUID。
2. 开始倒计时，倒计时时间可调。
3. 玩家需在倒计时时间内输入登录命令，可能是密码，也可能是加了别的东西的密码。例如：
```
!!login 密码
```

4. 密码正确，则倒计时结束。密码错误，倒计时继续。
5. 倒计时时间到，将玩家踢出服务器。
## 编程难点
这个问题会随着编程进程的推进而增加，想到多少写多少
### UUID 的获取
不仅是 MARYT 服务器，有需要使用登录插件的服务器都是离线服。
在开发初期**可能**不必考虑正版/离线的问题。
目前有两种可能的思路：
1. 使用现成的 UUIDAPI。
https://github.com/RisingInIris2017/MCDReforgedPlugins/tree/master/UUIDAPI
<br>这一方法的缺陷是需要频繁调用来自一个国外网站的 API，如果服务器到该网站的连接不畅通，很有可能会导致登录插件的工作异常。
<br>但是这个 UUIDAPI 的代码仍然是重要的参考。
2. 从服务端的username.json读取玩家的UUID。
<br>这种方法的好处是节省了大量的服务端联网等待时间，对于已经在username.json中留下痕迹的老玩家，必须采用这种方法。
<br>对于从未登录过服务器，首次登录的新玩家，有待测试。
3. 使用 https://gist.github.com/yushijinhun/69f68397c5bb5bee76e80d192295f6e0 中的算法生成离线 UUID。
<br>不确定这个方法是否仍然适用于 1.16+，有待测试。

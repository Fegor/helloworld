# helloworld

张德坤
4 个月前（修改过）
作为ssr-plus的contributor，我说几句ssrp和passwall的差异，及一些看法的纠正。
1. ssrp没有停更，更新地址在https://github.com/fw876/helloworld L大固件内想集成ssrp只需将编译根目录里面的feeds.conf.default文件内Helloworld前的 # 删除即可
2. L大固件集成ssrp后，DNS有三套，一套是默认wan口DNS，二是你在插件设置的外网DNS，三是Netflix分流所用的DNS。所以科学上网不需要使用SmartDNS和Turbo ACC中的DNS加速，使用运营商默认DNS即可，如果运营商DNS有劫持，把接口中Lan口DNS设置为你想要的即可，要是运营商强行抢答或劫持53端口，请在浏览器中使用DoH或DoT。
3. 对于自动切换功能，ssrp的逻辑是切过去看能不能wget到www.google.com这个网页，而不是看能不能ping通，passwall用的是haproxy，切换只看能否ping通。这对VPS梯子用户区别不大，但是对机场用户影响很大。
4. 所谓的“旁路由”是ks搞出来的，真正的名字是“单臂路由”。
5. ssrp支持socks5套娃模式，K2P+N1也能跑出400M。具体实现如下，K2P做主路由，N1网关设为K2P并关闭DHCP。N1正常订阅选好节点，并在服务端开启socks5服务器，K2P的ssrp节点设置为N1的socks5节点，并在访问控制排除代理N1的IP。这样做有一个好处，传统单臂路由解决方案中，一旦单臂路由故障或不能上网，会导致无法访问所有网站。而套娃模式中，N1故障也仅仅会导致无法科学上网，不影响国内网站访问。
6. 少折腾DNS，默认即可。正常网络环境下，几毫秒的延迟根本感受不到。如果你相信DNS能提升你的网速，建议使用PDNSD + DNSForwarder + DNSEncrypto + ChinaDNS-NG + SmartDNS + AdGuardHome + Pi-Hole +DNSMASQ + ssr-plus + ssr-Jeo + passwall + clash + openclash + helloworld来达到万兆网速

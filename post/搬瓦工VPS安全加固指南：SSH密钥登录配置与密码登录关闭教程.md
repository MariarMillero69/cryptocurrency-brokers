# 搬瓦工VPS安全加固指南：SSH密钥登录配置与密码登录关闭教程

使用搬瓦工VPS搭建节点后，许多用户往往忽略服务器安全设置。由于默认SSH端口为22且采用密码验证机制，极易遭受暴力破解攻击。本文将详细解析如何通过密钥登录改造和密码登录关闭，有效提升服务器安全等级。

👉 [【建议收藏】2025年搬瓦工最新优惠套餐整理汇总 - 每日更新最新可用优惠码](https://bit.ly/banwagon)

---

## 一、本地密钥对生成流程

### Windows系统操作步骤
1. 下载安装[PuTTYgen密钥生成工具](https://the.earth.li/~sgtatham/putty/latest/w64/puttygen.exe)
2. 选择RSA加密类型，密钥长度设置为4096位
3. 生成过程中需在空白区域移动鼠标加速熵池积累
4. 生成完成后执行：
   - 菜单栏选择`Conversions → Export OpenSSH key`
   - 保存.pem格式私钥文件
   - 完整复制公钥文本内容

---

## 二、服务器公钥部署方案
1. 登录[搬瓦工KiwiVM管理后台](https://bit.ly/banwagon)
2. 导航至`SSH Keys`功能模块
3. 粘贴本地生成的公钥内容
4. 点击`Save SSH Keys`完成密钥绑定
5. 执行系统重装操作激活配置（Install new OS）

> 系统重装时后台将自动注入预设公钥至`/root/.ssh/authorized_keys`文件

---

## 三、密码登录防护关闭教程
### 配置SSH服务参数
bash
nano /etc/ssh/sshd_config

1. 定位`PasswordAuthentication`参数项
2. 修改配置为：`PasswordAuthentication no`
3. 保存操作：
   - Ctrl+X → Y → Enter
4. 重启SSH服务生效配置

通过以上安全设置，可有效防止99%的暴力破解攻击，建议所有搬瓦工VPS用户在服务器初始化阶段完成配置。
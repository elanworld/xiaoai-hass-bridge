# 小爱 - Home Assistant 桥 

这是一个小米水滴平台的技能, 用于将小爱同学与 Home Assistant 系统桥接起来.
(A Shuidi Skill for bridging Xiaoai and Home Assistant)

v2.0
=============
+ 无法处理的情况交给ha语音助手处理
  + 语音助手可支持中文控制
  + 语音助手添加参考: [conversation](https://github.com/shaonianzhentan/conversation)

+ 查询实体不需要配置，自动拉取ha所有实体
+ docker镜像

  + docker run --restart always --name miai-ha-bridge -v /data/flask-tool/config:/app/config alanwoods/flask-mi-homeassistant


## 词汇

- 技能名称, 即在水滴平台中给技能定义的名称, 本文档后文中将记作 AA
- 直接指令, 即唤醒后直接下达指令, 无需显式地进入技能再下达指令, 指令执行完毕后自动退出技能
  - 指令格式为: 小爱同学, 让 AA 查一下当前室内温度
- 技能内连续指令, 即显式地进入技能, 后续可不用唤醒连续下达指令, 指令执行完毕后不会自动退出技能, 需显式的退出或超时退出
  - 进入技能: 小爱同学, 打开 AA
  - 退出技能: 小爱同学, 退出 AA
  - 技能内指令: 打开餐厅灯 / 关闭卧室灯 / 查一下室内温度 / 将窗帘打开一半
- 指令动词, 即打开/关闭/升起/降下等加于操作对象上的动作

## 实现的功能

- 查询只读传感器的数据, 动词可以为: 查一下, 报一下, 或者 xxx 是多少
- 控制开关量, 比如light/switch/script/scene 等所有支持 homeassistant.turn_on/turn_off 的entity, 动词可以为: 打开, 开一下, 关闭, 关上
- 帘子类设备, 即 Home Assistant 中的 Cover 类设备, 动词为: 打开, 升起, 关上, 关闭, 降下, 停止
  - 此类设备支持 set position

## 例子

- 小爱同学, 让 AA 查一下当前室内温度
- 小爱同学, 打开 AA / 进入 AA
  - 打开餐厅灯
  - 当前室内温度是多少?
  - 查一下室外温度
  - 降下晾衣架
  - 将窗帘打开一半
  - 升起卷帘
  - 退出 AA
- 小爱同学, 让 AA 记一下打开餐厅灯 (见`已知的限制`)

## 已知的限制

- 对于直接指令, 目前水滴预留给开发者的动词只有: 查一下, 记一下, 所以如果想通过直接指令控制某设备, 所下的指令就会比较别扭: "小爱同学, 让 AA 记一下打开餐厅灯"
- Cover 类设备 set position 目前只支持"一半", 例如: "把窗帘打开一半"

## 安装部署

- 由于此类 skill 通过审核的可能性不大, 所以必须开发者帐号
- 对音箱喊"小爱同学, 打开开发者模式", 重启之前无需再次激话开发者模式
- 部署 skill 后台服务, 请参照https://bbs.hassbian.com/thread-2404-1-1.html
- Tips:
  - 如果已经做好了到家里宽带的 DDNS, 可将此脚本直接跑在运行 Home Assistant 的主机上, 例如树莓派/NAS
  - SSL/HTTPS 是必须, 安装过程自行搜索
  

## 感谢
- syjjx @ bbs.hassbian.com
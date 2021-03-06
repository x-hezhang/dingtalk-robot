# 功能

- 发送消息到钉钉机器人。
- 支持所有钉钉机器人消息类型。
- 钉钉机器人支持多种安全设置，建议在设置时选择IP地址。
- [钉钉机器人开发文档](https://ding-doc.dingtalk.com/document#/org-dev-guide/qf2nxq)

# 安装

```bash
1. 安装该模块
pip install dingdingrobot
```

# 使用

- 获取钉钉机器人的 `access_token`

  创建机器人时，会返回一个 `webhook` 的地址，如 `https://oapi.dingtalk.com/robot/send?access_token=053e5481723dbe9b2e7765ece20118fa5963909d50f05ea6ae58214e9`，则 `access_token` 为 `053e5481723dbe9b2e7765ece20118fa5963909d50f05ea6ae58214e9`

* 使用

  ```python
  key = '053e5481723dbe9b2e7765ece20118fa5963909d50f05ea6ae58214e9'

  import dingdingrobot
  dtrobot = dingdingrobot.DingdingRobot(key)
  ```

* 发送文本消息

  ```python
  # 签名
  dtrobot.send_text(content, at_mobiles=None)

  # content 为要发送的文本内容
  # at_mobiles 需要 @ 人的手机号，可以是列表或字符串。如果要 @所有人，则设置 at_mobiles='all'。
  # @ 多个人时，指定 at_mobiles=['18600000000', '18600000001'] 或 at_mobiles='18600000000,18600000001'
  ```

* 发送 `markdown` 消息

  ```python
  # 签名
  dtrobot.send_markdown(title, contents, at_mobiles=None)
  # title     指定markdwon消息显示的标题
  # contents  为可迭代对象，如列表、元组等。每一行为一个 markdown 格式的字符串。
  # at_mobiles    需要@人的手机号，参考 send_text 中的 at_mobiles
  # 支持的格式参考：https://ding-doc.dingtalk.com/document#/org-dev-guide/qf2nxq/9e91d73c
  ```

* 发送 `link` 类型

  ```python
  # 签名
  dtrobot.send_link(title, text, jump_url, picurl=None)

  # title     消息标题
  # text      消息内容
  # jump_url  点击消息跳转的url
  # picurl    图片的url
  ```

* 发送 `actionCard` 

  ```python
  # 签名
  dtrobot.send_actioncard(title, text, btn_info, btns=False, btn_orientation=0)

  # title     指定 action card的标题
  # text      指定 action card的文本内容
  # btn_info  指定 button 的信息。格式为：[{'btn_title': 'title', 'btn_url': 'button url'}]
  # btns      False整体跳转, True 独立跳转。默认是 False
  # btn_orientation   button的排列方式。0按钮竖直排列，1按钮水平排列
  ```

* 发送 `feedCard`
    
  ```python
  # 签名
  dtrobot.send_feedcard(links)
  
  # links     格式为：[{'link_title': 'link title', 'message_url': 'message url', 'pic_url': 'pictur url'}]
  ```
  

# 示例
```python
key = 'you access token'
dtrobot = dingdingrobot.DingdingRobot(key)

# 发送 text 消息
dtrobot.send_text('123'))

# 发送 markdown 消息
dtrobot.send_markdown(title='123', contents=['# hello world', '> 1', '> 2', '> 3', '4'],
                        at_mobiles='18600010001,18655750614,all')

# 发送 link 消息
dtrobot.send_link(title='MAKA做出好设计', text='MAKA做出好设计', jump_url='https://www.maka.im',
                         picurl='https://img1.maka.im/template/T_XM3SO6TE_t1.jpg'))

# 发送 actionCard
dtrobot.send_actioncard(title='MAKA做出好设计', text='MAKA做出好设计',
                               btn_info=[{'btn_title': 'MAKA官网', 'btn_url': 'https://www.maka.im'},
                                         {'btn_title': 'MAKA做出好设计', 'btn_url': 'https://maka.im'}],
                               btns=True), 1)

# 发送 feedCard
dtrobot.send_feedcard(
    [
        {'link_title': 'MAKA做出好设计', 'message_url': 'https://www.maka.im',
         'pic_url': 'https://res.maka.im/platV5Cms/homepage/icon/Group22%402x.png?x-oss-process=image/format,webp'},
        {'link_title': 'link title', 'message_url': 'https://www.maka.im/muban',
         'pic_url': 'https://img1.maka.im/template/T_XM3SO6TE_t1.jpg'}
    ]
)
```

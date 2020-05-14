# Wechaty-Room-Manager [![Build Status](https://travis-ci.org/JesseWeb/wechaty-room-manager.svg?branch=master)](https://travis-ci.org/JesseWeb/wechaty-room-manager) [![Npm Version](https://img.shields.io/npm/v/wechaty-room-manager.svg?sanitize=true)](https://travis-ci.org/JesseWeb/wechaty-room-manager)

## What is this?

I am wechaty multiple room manager who leterally could do anything.

我是 [wechaty](https://github.com/wechaty/wechaty) 多群管理插件，目标是减轻群管理工作量
## Installation

```bash
npm install wechaty-room-manager@latest
```
## Usage

```javascript
import {Wechaty} from "wechaty"

import {manager} from "wechaty-room-manager"

const bot = new Wechaty({
   name:"wechaty-room-manager"
})

bot.use(manager({
   rooms: [{
      id: "1238716979@chatroom",
      topic: "机器人测试群",//either id or topic , using "===" to compare ｜ id topic二选一即可 建议id避免混淆 使用===比较

      knockKnock:"我要进群",  //机器人拉用户进入该群的口令

      //拉新人入群的欢迎消息
      hiTemp:"欢迎入群，请遵守群规", //@someone 欢迎入群，请遵守群规


      // 为什么使用array？
      // 因为laptop与手机端表情字符存在不一致的情况。且可支持多指令。
      voltSymbol: ['[弱]', '/:MMWeak'], 

      // 该房间的白名单、无法被投票。必须为id，防止修改成同样的alias伪装管理员
      // 注：此whiteList对kickout无效
      whiteList:[
         "botorange_yeah"
      ],
      /*
      *  踢出命令   @someone[炸弹]
      *  注：kickout只有admin才有权限
      *  
      */
      kickoutSymbol: ["[炸弹]", "/:bome"],

      // 被投票次数、超出即自动踢出
      voltCount: 3,
      // 踢出模版 
      // 会在开头自动@被踢出人
      kickoutTemp() {
         return "您已被踢出"   //@someone 您已被踢出
      },
      voltOutTemp(count) {
         return `您已被警告${count}次，您已被踢出群聊`  //@someone 您已被警告${count}次，您已被踢出群聊
      },
      warnTemp(count, voltCount) {
         return `您已被其他人警告次数达到${count}次，请谨慎发言。警告次数达到${voltCount}将被踢出`
      }
   }],
   //全局管理员、拥有高级能力例如直接踢人
   admins: [
      "xyzcain"
   ]
}))

bot.start()
   .catch(console.error)
```

## Test
```bash
npm run test
```

## Build
```bash
npm run build
```
## Maintainers
* @LegendaryJesse - [LegendaryJesse](https://github.com/JesseWeb)

## Copyright & License

* Code & Docs © 2020-now LegendaryJesse|Wechaty
* Code released under the MIT License
* Docs released under Creative Commons



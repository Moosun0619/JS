# 多合一签到脚本（仅Surge,根据sazs34大佬的修改为自己要用的，去掉自己不用的，自用版）--未修改完成，请勿使用

##以下为我自用的，如需全部的可去看sazs34大佬的：https://github.com/sazs34/TaskConfig

**支持列表**

|    名称    | Cookie |                             签到                             |                       感谢                        |     说明     |
| :--------: | :----: | :----------------------------------------------------------: | :-----------------------------------------------: | :----------: |
|  百度贴吧  |   ✅    |                              ✅                               |                      [@chavyleung](https://github.com/chavyleung)                  |              |                     |           
| 网易云音乐 |   ✅    |                              ✅                               |   [@chavyleung](https://github.com/chavyleung)    |              |
|    京东    |   ✅    | [获取](https://github.com/NobyDa/Script/blob/master/JD-DailyBonus/JD_DailyBonus.js) |       [@NobyDa](https://github.com/NobyDa)        | cookie同原版 |
|  微博超话  |   ✅    |                              ✅                               | [@NavePnow](https://github.com/NavePnow/Profiles) | cookie同原版 |

自用脚本地址:

**https://github.com/XYXShawn/JS/blob/master/all_in_one.js**

## 脚本配置说明

打开js文件,最开头的地方就能看到如下一段代码

```javascript
//因为有的人只有其中一个或两个需要进行签到,所以进行了配置化,可以指定签到
const global = {
    log: 1, //日志模式:0不显示 1全部显示 2精简显示,推荐值:1
    sign: { //用于设置哪些需要进行签到,哪些不处理
        baidu_tieba: true,
        iqiyi: true,
        _52pojie: true,
        netease_music: true,
        v2ex: true,
        weibo_super: true,
        china_telecom: true
    },
    data: {
        weibo_super: [
            ["周杰伦", "1008087a8941058aaf4df5147042ce104568da"],
            // ["IU", "100808d4151ccebfbae55e8f7c0f68f6d18e4d"],
            // ["SWITCH", "1008084239f063a3d4fb9d38a0182be6e39e76"],
        ],
        //此处输入要签到的手机号码
        china_telecom: '18851889188'//替换手机号部分即可
    }
}
```

| 节点 |      作用      |                 说明                 |
| :--: | :------------: | :----------------------------------: |
| log  | 在qx中显示日志 | 0不显示 1全部显示 2精简显示,推荐值:1 |
| sign |  控制是否签到  |     true为进行签到,false为不签到     |
| data |    额外参数    |        用于签到脚本中数据配置        |

**额外参数说明**

|     节点      |                             说明                             |
| :-----------: | :----------------------------------------------------------: |
|  weibo_super  | [微博超话名字及编号](https://nave.work/%E5%BE%AE%E5%8D%9A%E8%B6%85%E8%AF%9D%E8%87%AA%E5%8A%A8%E7%AD%BE%E5%88%B0%E8%84%9A%E6%9C%AC.html) |


## Surge配置说明

### MITM

此处需要获取Cookie时直接使用即可

使用完注释掉或者直接放着都行，没什么大影响

```
[mitm]
hostname = tieba.baidu.com, c.tieba.baidu.com, music.163.com, api.m.jd.com, weibo.com
```
###script

以下cookie获取后可注释掉
```
# 此处用于京东cookie获取，当失效时需要手动登录京东网页版https://bean.m.jd.com/ 签到获取Cookie, 待surge弹出获取成功即可 
http-request https:\/\/api\.m\.jd\.com\/client\.action.*functionId=signBean(Index|GroupStageIndex) max-size=0,script-path=https://raw.githubusercontent.com/XYXShawn/JS/master/all_in_one.js
# 此处用于百度贴吧cookie获取，当失效时需手动登录https://tieba.baidu.com/index.html贴吧获取cookie，待弹出获取成功即可
^https?:\/\/tieba.baidu\.com url script-request-header all_in_one.js
# APP端直接进去，点击"我的"即可
https?:\/\/c\.tieba\.baidu\.com\/c\/s\/login url script-request-header all_in_one.js
# 此处用于网易云音乐cookie获取，当失效时需浏览器访问并登录:https://music.163.com/m/login 获取cookie，待弹出获取成功即可
http-request ^https?:\/\/music\.163\.com\/?.? script-path=https://raw.githubusercontent.com/XYXShawn/JS/master/all_in_one.js
# 此处用于微博超话 cookie获取,打开超话页,点击'签到'或'已签到',用完后可以注释掉
;https:\/\/weibo\.com\/p\/aj\/general\/button\?ajwvr=6&api=http:\/\/i\.huati\.weibo\.com\/aj\/super\/checkin url script-request-header all_in_one.js
# 此处用于强制手机浏览器访问电脑端超话页面,用完后可以注释掉
;^https?://weibo\.com/p/[0-9] url request-header (\r\n)User-Agent:.+(\r\n) request-header $1User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/12.0.2 Safari/605.1.15

```

### 定时配置

```
cron "0 30 9 * * *" script-path=https://raw.githubusercontent.com/XYXShawn/JS/master/all_in_one.js
```

## 触发Cookie方式

|                             名称                             |  方式  |                            说明                            |
| :----------------------------------------------------------: | :----: | :--------------------------------------------------------: |
|                           百度贴吧                           | 浏览器 |             https://tieba.baidu.com/index.html             |
|                           百度贴吧                           |  APP   |                   进入APP,点击"我的"即可                   |
|                            网易云                            | 浏览器 |               https://music.163.com/m/login                |
| [微博超话](https://nave.work/%E5%BE%AE%E5%8D%9A%E8%B6%85%E8%AF%9D%E8%87%AA%E5%8A%A8%E7%AD%BE%E5%88%B0%E8%84%9A%E6%9C%AC.html) | 浏览器 | https://weibo.com/p/1008080c5fb650788fe5c7577f0b6ec4a34038 |




### Special thanks：
* [@sazs34](https://github.com/sazs34)

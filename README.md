# Surge4.0自用JS存档

## rrsp(可远程使用）
### 配置 (Surge)
```properties
[Script]
http-response ^https:\/\/api\.rr\.tv(\/user\/privilege\/list|\/ad\/getAll) requires-body=1,max-size=0,script-path=https://raw.githubusercontent.com/XYXShawn/JS/master/rrtv.js

Surge MITM =*.rr.tv
```

## qyxj（仅可本地使用，使用时注意本地路径）
### 配置 (Surge)
```properties
[Script]
http-response ^https:\/\/commerce-api\.faceu\.mobi\/commerce\/v1\/subscription\/ requires-body=1,max-size=0,script-path=script/qyxj.js

Surge MITM = commerce-api.faceu.mobi
```

## 彩云小译（远程）
### 配置 
```properties
####Surge 
[Script]
http-response ^https:\/\/api\.interpreter\.caiyunai\.com\/v1\/user requires-body=1,max-size=0,script-path=cyxy.js
Surge MITM = commerce-api.faceu.mobi

####QX
[Script]
^https:\/\/api\.interpreter\.caiyunai\.com\/v1\/user url script-response-body cyxy.js



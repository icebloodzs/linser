# console 前端功能

## react

> 登陆前：BASE_URL = /api/v1/
>
> 登陆后： BASE_URL = /api/v1/${params}

### 登陆功能
```
 path: /longin
```
- [x] 输入账号密码
- [x] 点击忘记密码，可进行邮箱验证
- [x] 输入内容重置
- [x] 账号密码不能为空    

```js
//登陆方式
method: 'get',
url: 'loginway',
params: {
    random: Number //随机数
},
response: {
    "success":true,"page":"login"
}

//sitedid
method: 'get',
url: 'getsitedid',
params: {
    random: Number //随机数
},
headers: {'Cache-Control': 'no-cache'},
response: 
{
    "success":true,"siteId":"xx322ds"
}

获取密码配置
method: 'get',
url: '/accessmanage/passwordstrategy',
params: {
    random: Number //随机数
},
response: {
    "success": true,
    "minLengthOfPasswordManager": 8,
    "passwordStyleManager": "1",
    "updatePasswordPeroidManager": 3,
    "isAllowRepeatePasswordManager": false,
    "minLengthOfPasswordVPN": 8,
    "passwordStyleVPN": "1",
    "updatePasswordPeroidVPN": 3,
    "isAllowRepeatePasswordVPN": false
}

//登陆
method: 'post',
url: '/login',
body: {  //newPassword为加密后的密文
    username,type,password,isPasswordFormatCorrect
},
params: {
    random: Number //随机数
},
response: {
    "success": true,
    "systemsettings": true,
    "detail": "df",
    "token": "xxxxxxdf",
    "name": "ss123456799",
    "role": "系统管理员",
    "roleCluster": "master",
    "perms": [
        "/api/v1/auth/needAlert",
        "/api/v1/auth/xdfds"
    ]
}

登陆后
method: 'post', 
url: '/menu',
body: { // id: 0 时获取头部一级菜单  id: 1 时获取左侧二级菜单
    id
},
params: {
    random: Number //随机数
},
response: {
   
}

// 忘记密码
method: 'post', //获取验证码 
url: '/forgetpassword/getcaptcha',
body: {
    username,email
},
params: {
    random: Number //随机数
},
response: {
    "success":true,"detail":"xx322ds"
}

method: 'post',//验证验证码 
url: '/forgetpassword/verify',
body: {
    username,email,captcha
},
params: {
    random: Number //随机数
},
response: {
    "success":true,"detail":"xx322ds"
}

获取密码规则
method: 'get',
url: 'passwordstrategy',

重置密码

method: 'post', 
url: '/reset',
body: { //newPassword为加密后的密文
    username,newPassword
},
params: {
    random: Number //随机数
},
response: {
    "success":true,"detail":"xx322ds"
}

退出
'GET /logout'
```

### 404页面

### 账户设置（登陆后的跳转页）

```
path: /accountmanagement
```
* 搜索查询功能（无）
* 添加账号功能
* 可操作性（发送邮件按钮、详细按钮、删除按钮）(无)
* 分页

```js
method: 'post', //获取用户列表
url: '/auth/accountmanagement',
params: {
    random: Number //随机数
},
response: { //其中之一的格式
   "id": "1923641",
    "name": "小明",
    "account": "ciphergate",
    "authcode": "wxRxqe",
    "certificate": "iasod",
    "email": "tian@ciphergateway.com"
}

method: 'post', //添加新用户
url: '/add',
body: { 
    account,email,key,name
},
params: {
    random: Number //随机数
},
response: { 

}
method: 'post', //删除账户
url: '/accountmanagement/delete',
body: { 
    id
},
params: {
    random: Number //随机数
},
response: {
    "success":true
}

```


### 左侧菜单栏（可新建应用）

#### 1. 连接账户

* 账户管理（即为上面的账户设置）
* 证书管理（不可用）

#### 2. 系统工具

* 网络设置
* 软件更新
* 数据备份
* 密钥备份
* 加密转换
* 数据复原

#### 3. 安全审计(✅)
1. 业务日志
```js
path: ftplog
```
> 查询参数
* 时间周期
* 姓名
* 目标系统
* ip地址
* 操作
* 资源
*  事件结果

```js
method: 'post', //
url: '/audit/tcplog',
body: { 
    paging:{
        entries:20,
        page:1
    },
    query:{},
    range:{},
    sort:{
        dec:true,
        orderColumn:'opertime'
    },
    type:"ftplog"
},
params: {
    random: Number //随机数
},
response: {
   "current": 1,
    "total": 9,
    "all": [{}]
}
```

2. 系统日志  （✅）
```
path:systemlog
```
> 查询参数  
* 时间周期
* 管理角色
* 管理员
* ip地址
* 事件描述
* 事件结果

```js
method: 'post', 
url: '/audit/systemlog',
body: { 
    paging:{
        entries:20,
        page:1
    },
    query:{},
    range:{},
    sort:{
        dec:true,
        orderColumn:'opertime'
    },
    type:"systemlog"
},
params: {
    random: Number //随机数
},
response: {
   "current": 1,
    "total": 9,
    "all": [{}]
}
```

3. 密钥日志（无）
```
path:alertlog
```
> 查询参数  
* 时间周期
* 操作人员
* 目标系统
* ip地址
* 事件描述
* 事件级别
* 报警方式

#### 4. 策略配置
1. 采集策略
```
path: collectstrategy
```
* 带分页的tableb表格
```js
method: 'get', 
url: '/collect/get',
params: {
    page:1,
    size:20,
    random: Number //随机数
},
response: {
    "success": true,
    "clusterRole": "audit",
    "data": [{}]
}
```
2. 安全策略
```
path: safestrategy
```
* 可添加配置
* 编辑按钮、删除按钮
* 分页

```js
method: 'get', 
url: '/strategy',
params: {
    random: Number //随机数
},
response: {
   "success": true,
    "clusterRole": "master",
    "list": [{}]
}
```

3. 安全分级
```
path: alertlevel
```
* 编辑按钮、删除按钮
* 可添加新的安全级别
* 分页

```js
method: 'get', 
url: '/alertlevel',
params: {
    random: Number //随机数
},
response: {
   "success": true,
    "clusterRole": "master",
    "data": [{}]
}
```

#### 5. 统计报表 (vue已实现)
1. 实时统计
```
path: /statisticalstatements/keyindicators
```
* 可导出excel
* 时间查询
* 图表与表格展示

2. 自定义统计
```
path: /statisticalstatements/targetstatistic
```
* 可导出excel
* 时间查询
* 基于不同分类展示
* 图表与表格展示

#### 6. 用户管理
```
path: ftpusers
```
* table表格展示（无操作）

#### 7. 设备监控（✅）
```
path: systemmonitor
```
1. 本级监控
* 仪表盘展示
* 饼状图展示

2. 集群监控
```
path:remotemonitor
```
* 图片展示
* 表格展示

### 8. 系统设置

1. 管理员账号
    1. 管理员账号（表格展示）
       ```
        path:managersettings_frame/managersettings
       ```
        * 新建管理员账号
        * 编辑、删除按钮
        * 密码、USBKey重置按钮
        * 是否启用按钮
    ```js
    获取管理员信息
    
    method: 'post', 
    url: '/managersettings',
    params: {
        random: Number //随机数
    },
    body:{
        current:1,
        size:10
    }
    response: {
        "list":[{}],
        "current": 1,
        "size": 10,
        "total": 2,
        "success": true
    }
    
    添加新的管理员
    
    method: 'post', 
    url: '/managersettings/add',
    params: {
        random: Number //随机数
    },
    body:{
        name,role,username,email,cerType,cert
    }
    response: {
       "success":true,"detail":"添加成功！"
    }
    
    编辑管理员信息
    
    method: 'post', 
    url: '/managersettings/update',
    params: {
        random: Number //随机数
    },
    body:{
        name,role,username,email,cerType,cert，active,id
    }
    response: {
      
    }
    
    管理员启用/停用
    
    method: 'post', 
    url: '/managersettings/active',
    params: {
        random: Number //随机数
    },
    body:{
        id,isActive
    }
    response: {
       "success":true
    }
    
    管理员删除
    
    method: 'post', 
    url: '/managersettings/delete',
    params: {
        random: Number //随机数
    },
    body:{
        id
    }
    response: {
       "success":true
    }
    ```

    2. 管理员角色（表格展示）
       ```
        path: managersettings_frame/rolesettings
       ```
        - [x] 新建角色（可配置最大数量、权限）
        - [x] 编辑、删除、查看权限按钮
    ```js
    获取所有角色信息
    'GET pageperms' 
    
    新建或编辑 删除（只传id）
    'GET rolessettings' 
    body:{
        authorizationsForms:[],
        count,name
    }
    
    ```


2. 访问配置
```
path: /access_frame
```
登陆配置

- 允许登录失败次数
- 登录失败锁定时间 
- 空闲注销时间

```js
获取配置

'GET  accessmanage/loginsettings' 

更改配置

'POST  accessmanage/loginsettings' 
body:{ // expire(空闲注销时间),failedLockTime(登录失败锁定时间),retryNumber(允许登录失败次数)
    expire,failedLockTime,retryNumber
}
```
 密码配置

* 最小密码长度
* 字符组合要求

```js
获取配置

'GET  accessmanage/passwordstrategy' 

更改配置

'POST  accessmanage/passwordstrategy' 
body:{ // 最小密码长度,字符组合要求
    minLengthOfPasswordManager,passwordStyleManager
}
```

3. 配置备份
    1. 数据备份
    2. 数据恢复
        - [x] 可选恢复文件
    3. 备份服务器设置
         - [x] 可修改

```js
备份服务器配置

'GET  backupsettings/backup' 

更改服务器配置

'POST  backupsettings/recovery' 
body:{
    name
}

获取备份服务器配置

'GET  backupsettings' 

更改服务器配置

'POST  backupsettings/ftpconfig' 
body:{ // 密码,账号,备份服务器IP,路径
    ftpPassword,ftpUserName,host,serverPath
}
```

4. 基本配置
    - [x] 恢复出厂设置(首次使用需要初始化系统管理员信息)
```
path: basesettings =>
path: personalsettings（初始化）
```
```js
获取验证码
'GET  /systemscheme/getcaptcha' 

验证验证码
'POST  /systemscheme/checkcaptcha' body:{captcha} 

'POST  /dbinit' body:{captcha} //初始化
body:{
    logBackup:{},
    personalInfo:{
        cert,company,confirm,email,name,password,username
    }
}
```

高级配置（未实现）

- 证书配置

- 导入证书
- 表格展示

```js
'POST  /certificatesettings'//导入证书
```

### 9. 网络设置
1. 网络模式

- 旁路设置
```js
'POST  /networkmode'  //保存配置
body:{
    mode,server
}
```

- 反向代理
```js
'POST  /networkmode'  //保存配置
body:{
    inner:[],
    mode,outer
}
```
- 网络接口

```js
保存/修改配置
'GET/POST  network/interface'  
body:{
    inner:[],
    mode,outer
}
```
### 10. teamcenter

1. 策略配置
* 添加新的访问控制策略
* table表格展示

```js
'GET  app/tcstrategy'  //获取配置
params:{
    appName
}
'POST  app/tcstrategy'  //新建配置
body:{
    appName,{}
}
```
2. 行列控制
* 新建
* 开启、预览、编辑、删除按钮
* table表格展示
```js
'GET  /app/strategy'  //获取配置
params:{
    appName,current
'POST  app/tcstrategy'  //新建配置
body:{
    appName,{}
}
```

3. 用户信息
    1. 角色

    * 新建
    * 编辑、删除按钮
    * table表格展示

    2. 账户

    * 新建
    * 编辑、删除按钮
    * table表格展示

4. 表单控制

- 新建
- 查询、编辑、删除
- table表格展示

### 11. U8
- 行列控制
- 用户信息
- 表单控制

### vue项目完成功能

- 登陆功能
- 404页面
- 系统设置
- 安全审计

    - [x] 用户统计(新增)

      ```j s
      'POST  `/appMonitor/queryActivityUser/${startTime}/${endTime}`'  //
      body:{
          currPageNo,dataTimeType,isDownload,pageSize,range,userName
      }
      ```

    - [x] 操作统计(新增)

      ```js
      'GET  /log/statistics/appMonitor/queryOperation' 
      ```

    - [x] 应用日志

      ```
      应用日志
      'POST  /log/appMonitor' 
      body:{
          current,fullTextQuery,query:{},size
      }
      
      自动提示
      'POST  /log/column/completion' 
      body:{
          columnName
      }
      
      日志详情
      'GET  /log/appMonitor/${params}' 
      body:{
         
      }
      ```

- 日志报表



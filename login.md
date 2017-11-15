## 登录

### 登录页获取验证码图片Captcha

<p class="tip">
请求地址: `GET`  `https://sixi.store/captcha`
</p>

响应数据参数:

| 参数       | 类型   |   描述                | 示例值   |
| :----     | :----- |  :----               | :---- |
|  image    | string | 所有页总共具有的记录数量 | dds9cnsgd222.png     |


### 登录后台

<p class="tip">
请求地址: `GET`  `https://sixi.store/login`
</p>

请求参数:

| 参数      | 类型   |  是否必须  | 最大长度 | 默认值 | 描述         | 示例值   |
| :----    | :----- | :----    |  :----  | :---- |  :----       | :---- |
| user     | string |   是     |   32    |   -    | 登录用户名或邮箱 | admin     |
| password | string |   是     |   32    |   -   | 登录密码 | P@ssw0rd  |

响应数据参数:

| 参数        | 类型   |   描述                | 示例值   |
| :----      | :----- |  :----               | :---- |
|  jwt_token | string | jwt验证token | jsdodsne.9932mdssdsds.dxnss    |

## 授权

<p class="danger">
  后台除上面两个接口外,其余所有接口均需auth授权,因此都需要在请求头添加jwt token
</p>

### 获取授权菜单

<p class="tip">
请求地址: `GET`  `https://sixi.store/privilege/menu`
</p>

响应数据参数:

| 参数       | 类型   |   描述                | 示例值   |
| :----     | :----- |  :----               | :---- |
|  menu    | array | 所有具有权限的菜单 | [{"name": "user", "summary": "用户"}] |

响应数据参数`menu`内容说明:

| 参数       | 类型   |   描述  | 示例值  |
| :----     | :----- |  :---- | :----  |
|  id       | string | 菜单id  | 1  |
|  name    | string |  菜单key  | user  |
|  summary  | string | 菜单名  | 用户  |

响应示例:
```json
{
    "code": 10000,
    "data": {
        "menu": [
            {
                "id": 1,
                "name": "user",
                "summary": "用户"
            },
            {
                "id": 2,
                "name": "product",
                "summary": "商品"
            },
            {
                "id": 3,
                "name": "sale",
                "summary": "促销"
            }
        ]
    }
}
```

### 获取一个菜单下的授权页面

<p class="tip">
请求地址: `GET`  `https://sixi.store/privilege/page/{menu}`
</p>

请求地址参数:

| 参数      | 类型   |  是否必须  | 最大长度 | 默认值 | 描述         | 示例值   |
| :----    | :----- | :----    |  :----  | :---- |  :----       | :---- |
| {menu}     | int    | 是        |   11   |    -   | 菜单id       | 1     |

响应数据参数:

| 参数       | 类型   |   描述                | 示例值   |
| :----     | :----- |  :----               | :---- |
|  menu    | array | 所有具有权限的菜单 | [{"name": "user", "summary": "用户管理"}] |

响应数据参数`menu`内容说明:

| 参数       | 类型   |   描述  | 示例值  |
| :----     | :----- |  :---- | :----  |
|  id    | number | 页面id  | 1  |
|  name    | string | 页面key  | user  |
|  summary  | string | 页面名  | 用户管理  |

响应示例:
```json
{
    "code": 10000,
    "data": {
        "menu": [
            {
                "id": 1,
                "name": "user",
                "summary": "用户"
            },
            {
                "id": 2,
                "name": "product",
                "summary": "商品"
            },
            {
                "id": 3,
                "name": "sale",
                "summary": "促销"
            }
        ]
    }
}
```

### 获取一个页面下的授权按钮

<p class="tip">
请求地址: `GET`  `url`
</p>

每个页面请求接口加上请求参数`privilege`,接口返回除页面需要数据外,还会返回按钮授权:

| 参数      | 类型   |  是否必须  | 最大长度 | 默认值 | 描述         | 示例值   |
| :----    | :----- | :----    |  :----  | :---- |  :----       | :---- |
| 其他参数   | -    | -        |   -   |    -   | -       | -    |
| privilege  | number    | 否        |   1   |    0   | 页面权限     | 1     |

响应数据参数:

| 参数       | 类型   |   描述                | 示例值   |
| :----     | :----- |  :----               | :---- |
|  其他参数   | - | - | - |
|  button_privilege   | array | 所有具有权限的按钮 | [{"name": "add-user", "summary": "添加用户"}] |

响应数据参数`menu`内容说明:

| 参数       | 类型   |   描述  | 示例值  |
| :----     | :----- |  :---- | :----  |
|  name    | string | 按钮key  | add-user  |
|  summary  | string | 按钮名  | 添加用户  |

响应示例:
```json
{
    "code": 10000,
    "data": {
        "total": 1,
        "last_page": 1,
        "data": [
            {
                "id": 1,
                "avatar": "1.png",
                "name": "test",
                "sex" : 1
            }
        ],
        "button_privilege": [
            {
                "name": "add-user",
                "summary": "添加用户"
            },
            {
                "name": "edit-user",
                "summary": "编辑用户"
            },
            {
                "name": "delete-user",
                "summary": "删除用户"
            }
        ]
    }
}
```

# Level2

## 场景描述：

小爪的个人记账软件在宿舍里小有名气。室友们纷纷来借用,结果每次都要在小爪的电脑上操作,还得排队等着。更尴尬的是,上次小明在记账时不小心看到了小爪的"深夜零食支出"高达800元/月的秘密...

"要是能像用支付宝一样,每个人在自己手机上就能记账就好了!" 室友小王的抱怨让小爪陷入沉思。

这学期小爪选修了《Web开发技术》,学习了HTTP协议、RESTful API设计,还接触到了主流框架。他突然意识到:如果把记账系统改造成Web服务,不就能让大家随时随地通过手机APP或者网页来记账了吗?

说干就干!小爪决定将之前的命令行记账软件升级为一个完整的后端服务系统。这次要用上MySQL数据库来存储数据,设计规范的RESTful API接口,还要实现用户认证和权限管理,让每个人都有自己独立的账本,再也不用担心隐私泄露了!

但是,从单机程序到Web服务,从文件存储到数据库,从命令行交互到HTTP接口...这些改变让小爪有些发愁。你能帮小爪完成这次技术升级吗?

## 推荐项目使用的技术关键词

1. MYSQL数据库
2. MVC设计模式
3. RESTful API设计规范
4. Apifox接口文档工具等

## 角色要求说明

| 角色     | 职责说明                                                   |
| -------- | ---------------------------------------------------------- |
| 普通用户 | 系统的主要用户，负责记录和管理个人的收支账单，查看统计报表 |
| 管理员   | 系统管理人员，负责用户管理等基础数据的维护                 |

## 业务功能基本要求

### 1. 登录注册功能

实现以下基本功能

1. 实现基本的用户登录与注册
2. 实现基本的用户认证，密码校验
3. 实现密码加密功能（可选）
4. 实现权限拦截

接口例子：

```java
POST /account/api/auth/login
Content-Type: application/json
{
  "username": "123456",
  "password": "123456"
}
```

### 2.用户功能

提供以下api:

1. 添加账单记录
2. 修改账单记录
3. 删除账单记录
4. 查询账单列表
5. 查询账单详情
6. 查询总余额（总收入 - 总支出）
7. 按分类统计收支（可选）
8. 查询个人信息
9. 修改个人信息（昵称等）
10. 修改密码
11. 支持设置和生成周期性账单（如每月房租、每周聚餐等）（可选）

### 3.管理员功能

提供以下api:

1. 查询用户列表
2. 禁用/启用用户
3. 重置用户密码（可选）
4. 查询系统用户总数（可选）
5. 查询用户账单总数（可选）

### 4.高级功能

- 提供以下用户api:
  1. 支持分页、按时间范围查询、按分类查询查询账单列表

  2. 按时间范围统计收支

  3. 用户可设置月度预算（按月、按分类设置）

  4. 实时计算预算使用情况

  5. 预算超支预警（可选）

## 注意事项

1. 可选功能模块部分是否实现取决于对于该项目的规划和时间安排
2. 高级功能模块为加分项，可自己评估是否有时间学习书写
3. 账单分类可自行设计（比如购物，交通，餐饮等等）
4. 所使用技术不限，可使用所选语言的主流框架（如Java使用springboot，python使用fastapi）
5. 本考核不要求全部完成，按照自身时间和学习安排，能实现多少是多少

## 技术要求

1. 遵循RESTful API设计规范
2. 使用Swagger/Apifox等工具编写API文档
3. 实现统一的异常处理和响应格式
4. 合理使用设计模式（推荐使用MVC设计模式）

## 其他要求

1. 专注于后端业务逻辑实现,不要求提供前端页面

2. 要求分包分类，切勿一个包一个类写到底！！！

3. 所有接口可通过Swagger/Apifox等工具测试

4. 代码注释务必写好。标明每一个方法的作用、变量的作用等等

5. 严禁使用中文拼音或其缩写作为名称。在同一个项目中保持统一的命名规范（尽量使用所选语言的命名规范）。命名需要有语义，接近自然语言。尽量少使用临时性命名。

6. 文件编码统一使用UTF-8。避免在其他人查阅你的代码时无法查看注释

7. 强制

   使用git进行版本控制，并且push到github或gitee
   - 仓库必须设置为公开仓库
   - 在编码过程中需要逐步commit，并书写规范的commit message
   - 建议使用issue记录工作进度、需求和规划(非强制)

## 项目交付物

1. 源代码(包含完整的注释)
2. API文档(Swagger/Apifox导出)
3. 项目说明文档(Markdown格式)
   - 项目说明
   - 数据库设计说明
   - 配置说明
   - 使用说明
   - 测试说明
4. 数据库脚本(指定MySQL版本8.0+,可以从找数据库工具导出所有建表语句)

## 部分可能的帮助

这里提供**部分**可能对类的定义和建表语句脚本和请求响应以作示例，自行根据情况修改

### 实体类的定义（以Java为例）

```java
/**
 * 用户实体类
 * 用于存储系统用户信息，包括普通用户和管理员
 */
public class User {
    /** 用户ID */
    private Long id;

    /** 用户名 */
    private String username;

    /** 用户密码 */
    private String password;

    /** 角色：0-普通用户，1-管理员 */
    private Integer role;

    /** 账户状态：0-禁用，1-启用 */
    private Integer status;

    /** 创建时间 */
    private LocalDateTime createTime;

    /** 更新时间 */
    private LocalDateTime updateTime;

    //getter,setter,toString此处省略

}


/**
 * 账单实体类
 * 用于存储用户的收支记录
 */
public class Bill {
    /** 账单ID */
    private Long id;

    /** 用户ID，外键关联用户表 */
    private Long userId;

    /** 账单类型：0-支出，1-收入 */
    private Integer type;

    /** 金额 */
    private Double amount;

    /** 分类名称 */
    private String categoryName;

    /** 账单日期 */
    private LocalDate billDate;

    /** 备注说明 */
    private String remark;

    /** 是否为周期性账单生成的记录：0-否，1-是 */
    private Integer isRecurring;

    /** 关联的周期性账单ID（如果是周期性账单生成的） */
    private Long recurringBillId;

    /** 创建时间 */
    private LocalDateTime createTime;

    /** 更新时间 */
    private LocalDateTime updateTime;

    //getter,setter,toString此处省略
}
```

### 部分建表

```mysql
-- 用户表
CREATE TABLE `user` (
  `id` BIGINT NOT NULL AUTO_INCREMENT COMMENT '用户ID',
  `username` VARCHAR(50) NOT NULL COMMENT '用户名',
  `password` VARCHAR(255) NOT NULL COMMENT '密码（加密存储）',
  `role` TINYINT NOT NULL DEFAULT 0 COMMENT '角色：0-普通用户，1-管理员',
  `status` TINYINT NOT NULL DEFAULT 1 COMMENT '账户状态：0-禁用，1-启用',
  `create_time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `update_time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='用户表';

-- 账单表
CREATE TABLE `bill` (
  `id` BIGINT NOT NULL AUTO_INCREMENT COMMENT '账单ID',
  `user_id` BIGINT NOT NULL COMMENT '用户ID',
  `type` TINYINT NOT NULL COMMENT '账单类型：0-支出，1-收入',
  `amount` DOUBLE NOT NULL COMMENT '金额',
  `category_name` VARCHAR(50) DEFAULT NULL COMMENT '分类名称',
  `bill_date` DATE NOT NULL COMMENT '账单日期',
  `remark` VARCHAR(500) DEFAULT NULL COMMENT '备注说明',
  `is_recurring` TINYINT NOT NULL DEFAULT 0 COMMENT '是否为周期性账单生成：0-否，1-是',
  `recurring_bill_id` BIGINT DEFAULT NULL COMMENT '关联的周期性账单ID',
  `create_time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP COMMENT '创建时间',
  `update_time` DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP COMMENT '更新时间',
  PRIMARY KEY (`id`)
) ENGINE=InnoDB DEFAULT CHARSET=utf8mb4 COMMENT='账单表';
```

### 响应格式（以Java为例）

```java
/**
 * 统一响应结果
 * @param <T> 响应数据类型
 */
public class Result<T> {
    /** 响应码 */
    private Integer code;
    /** 响应消息 */
    private String message;
    /** 响应数据 */
    private T data;
    /** 响应时间戳 */
    private Long timestamp;

    /** 成功响应码 */
    public static final Integer SUCCESS = 200;
    /** 参数错误响应码 */
    public static final Integer PARAM_ERROR = 400;
    /** 未授权响应码 */
    public static final Integer UNAUTHORIZED = 401;
    /** 禁止访问响应码 */
    public static final Integer FORBIDDEN = 403;
    /** 资源不存在响应码 */
    public static final Integer NOT_FOUND = 404;
    /** 服务器错误响应码 */
    public static final Integer ERROR = 500;

    /**
     * 私有构造方法
     */
    private Result() {
        this.timestamp = System.currentTimeMillis();
    }

    /**
     * 成功响应
     */
    public static <T> Result<T> success() {
        Result<T> result = new Result<>();
        result.setCode(SUCCESS);
        result.setMessage("操作成功");
        return result;
    }

    /**
     * 成功响应
     * @param data 响应数据
     */
    public static <T> Result<T> success(T data) {
        Result<T> result = new Result<>();
        result.setCode(SUCCESS);
        result.setMessage("操作成功");
        result.setData(data);
        return result;
    }

    /**
     * 失败响应
     * @param code 错误码
     * @param message 错误信息
     */
    public static <T> Result<T> error(Integer code, String message) {
        Result<T> result = new Result<>();
        result.setCode(code);
        result.setMessage(message);
        return result;
    }

    // getter setter 方法省略
}

/**
 * 分页查询结果
 * @param <T> 数据类型
 */
public class PageResult<T> {
    /** 总记录数 */
    private Long total;
    /** 当前页码 */
    private Integer pageNum;
    /** 每页大小 */
    private Integer pageSize;
    /** 数据列表 */
    private List<T> list;

    // getter setter 方法省略
}
```

### 可能的完整请求及响应

```java
POST /account/api/bill

Request:
{
    "userId": 001,
    "type": 0,
    "amount": 50,
    "categoryName": "购物",
    "remark": "无",
    "isRecurring": 1,
    "recurringBillId": 101
}

Response:
{
    "code": 200,
    "message": "添加成功",
    "data": {
        "id": 1
        "userId": 001,
        "type": 1,
        "amount": 50,
        "categoryName": "购物",
        "billDate": "2026-01-21",
        "remark": "无",
        "isRecurring": 1,
        "recurringBillId": 101,
        "createTime": "2026-01-21",
        "updateTime": "2026-01-21"
    },
    "timestamp": 1678881234567
}

POST /account/api/auth/login
Request:
{
    "username": "小爪",
    "password": "123456"
}

Response:
{
    "code": 200,
    "message": "登录成功",
    "data": {
        "token": "eyJhbGciOiJIUzI1NiJ9...",
        "userInfo": {
            "id": 1,
            "username": "小爪",
            "role": 0,
            "status": 1
        }
    },
    "timestamp": 1678881234567
}
```

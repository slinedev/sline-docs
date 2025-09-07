# Sline Tag API 参考文档

本文档提供了Sline模板引擎中所有可用标签(Tag)的详细说明。

## 目录

- [流程控制](#流程控制)
- [表单相关](#表单相关)
- [客户和账户](#客户和账户)
- [地址和联系信息](#地址和联系信息)
- [订单和支付](#订单和支付)
- [商品和分类](#商品和分类)
- [链接和导航](#链接和导航)
- [媒体和资源](#媒体和资源)
- [模板和组件](#模板和组件)
- [变量和数据](#变量和数据)
- [HTML生成](#html生成)
- [其他工具](#其他工具)

---

## 流程控制

### for

为数组中的每个项渲染一个表达式。

**语法:**
```html
{{#for item in array}}
  expression
{{/for}}
```

**参数:**
- `array` - 需要执行循环的数组
- `item` - 当前循环中的变量值
- `expression` - 每次循环中执行的语句

**描述:** 每个`for`循环都有一个关联的[forloop object](/docs/sline/object/forloop)，其中包含有关循环的信息。

**示例:**
```html
{{#for tag in product.tags}}
  {{forloop.index}}: {{tag}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/for)

### if

如果特定条件为true则呈现表达式。

**语法:**
```html
{{#if condition }}
  expression
{{/if}}
```

**参数:**
- `condition` (expression) - 要判断的条件

**示例:**
1. 基本判断:
```html
{{#if product.price > 30 }}
    product price more than 30
{{/if}}
```

2. else if 条件:
```html
{{#if product.price < 30 }}
    product price less than 30
{{#else if product.price > 30 /}}
    product price more than 30
{{/if}}
```

3. else 条件:
```html
{{#if product.price < 30 }}
    product price less than 30
{{#else/}}
    product price more than 30
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/if)

### switch

根据特定变量的值呈现特定的表达式。

**语法:**
```html
{{#switch variable}}
{{#case condition /}}
  value_1
{{#case condition /}}
  value_2
{{#else/}}
  value_default
{{/switch}}
```

**参数:**
- `variable` (string|boolean|number) - 要进行比较的变量

**示例:**
```html
{{#var val = "apple" /}}

{{#switch val}}
{{#case "cat" /}}
  animal
{{#case "apple" "banana" /}}
  fruit
{{#else/}}
  unknown
{{/switch}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/switch)

### case

用于在switch tag中定义具体的逻辑分支。

**语法:**
```html
{{#switch variable}}
  {{#case first_value /}}
    first_expression
  {{#case second_value /}}
    second_expression
  {{#else/}}
    third_expression
{{/switch}}
```

**参数:**
- `value` (string|number|boolean) - 需要匹配的特定值

**描述:** 通过匹配特定值，将程序执行路由到对应的代码块，核心作用是为多路条件判断提供结构化处理方案，适当使用可以提升代码可读性和可维护性。

**示例:**
```html
{{#switch product.type}}
  {{#case "3c" /}}
    show 3c product
  {{#case "dress" /}}
    show dress product
  {{#else/}}
    show other product
{{/switch}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/case)

---

## 表单相关

### cart_form

根据当前购物车中的商品生成用于创建结帐的表单。

**语法:**
```html
{{#cart_form id="cart-form-id"}}
    your code
{{/cart_form}}
```

**可选参数:**
- `attr` (string) - 你可以添加任意参数来制定HTML属性，该参数应与（包含但不限于data-前缀）属性名和所需值相匹配

**描述:** 购物车表单需要一个cart object作为参数。要了解在主题中使用购物车表单的更多信息，请查阅cart template。

**示例:**
1. 基本使用:
```html
{{#cart_form id="cart-form-id"}}
    your code
    <button type="submit" class="button" name="checkout">checkout</button>
{{/cart_form}}
```

2. 添加class和属性:
```html
{{#cart_form id="cart-form-id" data-attr="attr-test" class="cartFrom"}}
    your code
    <button type="submit" class="button" name="checkout">checkout</button>
{{/cart_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/cart-form)

### customer_form

生成邮件订阅表单。

**语法:**
```html
{{#customer_form}}
    form_content
{{/customer_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的跳转地址，默认为当前页面地址

**表单输入:**
- `contact[email]` (email, 必填) - 邮箱
- `contact[tags]` (string) - 标签，多个用`,`连接，例如：home_page,footer

**示例:**
```html
{{#customer_form}}
    {{#if form.posted_successfully}}
      <div>Success</div>
    {{/if}}
    {{#if form.errors.messages}}
      <div>{{ form.errors.messages }}</div>
    {{/if}}
    <input type="hidden" name="contact[tags]" value="home_page,footer">
    <div class="email">
      <label for="contact[email]">Subscribe Email</label>
      <input type="email" name="contact[email]" placeholder="Please enter your email address" />
    </div>
    <div class="submit">
      <input class="submit-button" type="submit" value="Subscription">
    </div>
{{/customer_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/customer-form)

### contact_form

生成用于向商家提交电子邮件的表单。

**语法:**
```html
{{#contact_form /}} custom code {{/contact_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的重定向URL，默认为当前页面

**表单输入:**
- `contact[email]` (email, 必填) - 邮箱地址
- `attribute[key]` (any, 选填) - 自定义属性，例如：name、phone、birthday

**示例:**
```html
{{#contact_form id="ContactForm"}}
  {{#if form.posted_successfully}}
    <div>Submit Successfully</div>
  {{/if}}

  {{#if form.errors.messages}}
    <div>{{form.errors.messages}}</div>
  {{/if}}

  <div class="fields">
    <label class="field">
      <input type="text" name="contact[name]" title="Name" placeholder="Please enter your name">
    </label>

    <label class="field">
      <input type="email" name="contact[email]" title="Email" placeholder="Please enter your email address" required>
    </label>

    <label class="field">
      <input type="tel" name="contact[phone]" title="Phone" pattern="[0-9\-]*" placeholder="Please enter your phone number">
    </label>

    <div>
      <input type="submit" value="Submit">
    </div>
  </div>
{{/contact_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/contact-form)

### new_comment_form

生成用于博客文章新建评论的表单。

**语法:**
```html
{{#new_comment_form /}} custom code {{/new_comment_form}}
```

**参数:**
- `article` (object) - 文章对象

**表单输入:**
- `comment[author]` (text, 必填) - 评论者名称
- `comment[email]` (email, 必填) - 评论者邮箱地址
- `comment[body]` (body, 必填) - 评论内容

**示例:**
```html
{{#new_comment_form article}}
  {{#if form.posted_successfully}}
    <div>Submit Successfully</div>
  {{/if}}

  {{#if form.errors.messages}}
    <div>{{form.errors.messages}}</div>
  {{/if}}

  <div class="fields">
    <label class="field">
      <input type="text" name="comment[author]" placeholder="Please enter your name" required>
    </label>

    <label class="field">
      <input type="email" name="comment[email]" placeholder="Please enter your email address" required>
    </label>

    <label class="field">
      <textarea name="comment[body]" placeholder="Please enter your comment" required></textarea>
    </label>

    <div>
      <input type="submit" value="Submit">
    </div>
  </div>
{{/new_comment_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/new-comment-form)

---

## 客户和账户

### customer_login_form

生成客户登录表单。

**语法:**
```html
{{#customer_login_form}}
    form_content
{{/customer_login_form}}
```

**可选参数:**
- `thirdLogin` (string) - 开启第三方登录

**表单输入:**
- `customer[email]` (email) - 邮箱。商家开启邮箱注册时可用，使用邮箱登录时必填。`customer[email]`和`customer[phone]`只能同时提交其中之一
- `customer[phone]` (phone) - 手机号。商家开启手机号注册时可用，使用手机号登录时必填。格式为国际电话号码，例如中国手机号码：15600000000
- `customer[code]` (number) - 区号。和`customer[phone]`一起使用，格式为国际电话区号，例如大陆手机区号：86
- `customer[password]` (string, 必填) - 密码。最大长度限制：18，最小长度限制：6

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/customer-login-form)

### create_customer_form

生成注册账号表单。

**语法:**
```html
{{#create_customer_form}}
    form_content
{{/create_customer_form}}
```

**表单输入:**
- `customer[email]` (email) - 邮箱。商家开启邮箱注册时可用，使用邮箱注册时必填。`customer[email]`和`customer[phone]`只能同时提交其中之一
- `customer[phone]` (phone) - 手机号。商家开启手机号注册时可用，使用手机号注册时必填。格式为国际电话号码，例如中国手机号码：15600000000
- `customer[code]` (number) - 区号。和`customer[phone]`一起使用，格式为国际电话区号，例如大陆手机区号：86
- `customer[password]` (string, 必填) - 密码。最大长度限制：18，最小长度限制：6
- `customer[verifycode]` (number) - 验证码，商家开启身份验证时必填
- `customer[first_name]` (string) - 姓氏
- `customer[last_name]` (string) - 名字
- `customer[birthday]` (string) - 生日。格式：`YYYYMMDD`，例如：`19990101`
- `customer[gender]` (number) - 性别。有效枚举值：`1`男、`2`女、`3`保密
- `customer[accepts_marketing]` (boolean) - 客户是否接受电子邮件订阅
- `attribute[your_key]` (string) - 任意你想要收集的客户信息，例如：`<input name="attribute[age]" />`

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/create-customer-form)

### activate_customer_password_form

生成激活账号表单。商家可以给账号未激活的客户发送激活邀请邮件，客户点击邮件中的账号激活链接将进入激活页面，输入密码后即可激活账号。

**语法:**
```html
{{#activate_customer_password_form}}
    form_content
{{/activate_customer_password_form}}
```

**表单输入:**
- `customer[password]` (string, 必填) - 密码。最大长度限制：18，最小长度限制：6
- `customer[accepts_marketing]` (boolean) - 客户是否接受电子邮件订阅

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/activate-customer-password-form)

### reset_customer_password_form

生成忘记密码表单。

**语法:**
```html
{{#reset_customer_password_form}}
    form_content
{{/reset_customer_password_form}}
```

**表单输入:**
- `customer[email]` (email) - 邮箱。商家开启邮箱注册时可用，使用邮箱重置密码时必填。`customer[email]`和`customer[phone]`只能同时提交其中之一
- `customer[phone]` (phone) - 手机号。商家开启手机号注册时可用，使用手机号重置密码时必填。格式为国际电话号码，例如中国手机号码：15600000000
- `customer[code]` (number) - 区号。和`customer[phone]`一起使用，格式为国际电话区号，例如大陆手机区号：86
- `customer[password]` (string, 必填) - 新密码。最大长度限制：18，最小长度限制：6
- `customer[password_confirm]` (string, 必填) - 二次确认新密码。最大长度限制：18，最小长度限制：6
- `customer[verifycode]` (number, 必填) - 验证码

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/reset-customer-password-form)

### update_customer_form

生成更新个人信息表单。

**语法:**
```html
{{#update_customer_form}}
    form_content
{{/update_customer_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的跳转地址，默认为当前页面地址

**表单输入:**
- `customer[first_name]` (string) - 姓氏
- `customer[last_name]` (string) - 名字
- `customer[birthday]` (string) - 生日。格式：`YYYYMMDD`，例如：`19990101`
- `customer[gender]` (number) - 性别。有效枚举值：`1`男、`2`女、`3`保密

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/update-customer-form)

### bind_customer_email_form

生成修改用户邮箱表单。

**语法:**
```html
{{#bind_customer_email_form}}
    form_content
{{/bind_customer_email_form}}
```

**表单输入:**
- `customer[verifycode1]` (number) - 用于验证当前邮箱的验证码，商家开启身份验证时必填
- `customer[email]` (email, 必填) - 邮箱
- `customer[verifycode]` (number) - 用于验证新邮箱的验证码，商家开启身份验证时必填

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/bind-customer-email-form)

### bind_customer_phone_form

生成修改用户手机号表单。

**语法:**
```html
{{#bind_customer_phone_form}}
    form_content
{{/bind_customer_phone_form}}
```

**表单输入:**
- `customer[verifycode1]` (number) - 用于验证当前手机号的验证码，商家开启身份验证时必填
- `customer[phone]` (phone, 必填) - 手机号，格式为国际电话号码，例如中国手机号码：15600000000
- `customer[code]` (number, 必填) - 国际电话区号，例如中国手机区号：86
- `customer[verifycode]` (number) - 用于验证新手机号的验证码，商家开启身份验证时必填

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/bind-customer-phone-form)

### customer_subscribe_form

生成邮箱/手机订阅表单。

**语法:**
```html
{{#customer_subscribe_form}}
    form_content
{{/customer_subscribe_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的跳转地址，默认为当前页面地址

**表单输入:**
- `customer[email]` (email) - 邮箱。订阅邮箱时必填
- `customer[phone]` (phone) - 手机号。订阅手机时必填，手机号格式为国际电话号码，例如中国手机号码：15600000000
- `customer[code]` (number) - 区号。订阅手机时必填，区号为国际电话区号，例如中国手机区号：86

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/customer-subscribe-form)

### customer_unsubscribe_form

生成取消邮箱/手机订阅表单。

**语法:**
```html
{{#customer_unsubscribe_form}}
    form_content
{{/customer_unsubscribe_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的跳转地址，默认为当前页面地址

**表单输入:**
- `customer[unsubscribe_type]` (string, 必填) - 取消订阅类型。有效枚举值：`email`取消邮箱订阅、`phone`取消手机订阅
- `customer[unsubscribe_reason]` (number) - 取消订阅原因。取消邮箱订阅时有效，有效枚举值：`1`我不想接收此类邮件、`2`我收到的邮件数量过多、`3`我未订阅过此类邮件、`4`邮件内容与我无关、`5`邮件内容过长、`6`其他原因
- `customer[other_reason]` (string) - 其他原因，当`customer[unsubscribe_reason]`值为`6`时有效

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/customer-unsubscribe-form)

### delete_customer_form

生成注销账号表单。

**语法:**
```html
{{#delete_customer_form}}
    form_content
{{/delete_customer_form}}
```

**表单输入:**
- `customer[verifycode]` (number, 必填) - 验证码

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/delete-customer-form)

### cancel_delete_customer_form

生成取消注销账号表单。

**语法:**
```html
{{#cancel_delete_customer_form}}
    form_content
{{/cancel_delete_customer_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的跳转地址，默认为当前页面地址

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/cancel-delete-customer-form)

---

## 地址和联系信息

### customer_address_form

生成用于在客户帐户上创建新地址、编辑或删除现有地址的表单。

**语法:**
```html
{{#customer_address_form}}
    form_content
{{/customer_address_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的跳转地址，默认为当前页面地址
- `address_seq` (string) - 地址的id字段，删除地址时传入。可以通过customer object中的addresses字段获取
- `address` (untyped) - 用于编辑地址的地址详细数据。可以通过customer object中的addresses字段获取

**表单输入:**
- `address[first_name]` (string) - 收件人的名
- `address[last_name]` (string) - 收件人的姓
- `address[address1]` (string) - 地址的第一行。通常是街道地址或邮政信箱编号等信息
- `address[address2]` (string) - 地址的第二行。通常是公寓、套房或单元等信息
- `address[city]` (string) - 地址中的城市
- `address[city_code]` (string) - 地址中城市的编码
- `address[company]` (string) - 收件人的公司名称
- `address[country]` (string) - 地址中的国家或区域
- `address[country_code]` (string) - 地址中国家或区域的二位码，遵循ISO 3166-1 (alpha 2)国际标准，例如`US`
- `address[district]` (string) - 地址中的区或县
- `address[district_code]` (string) - 地址中区或县的编码
- `address[phone]` (string) - 收件人的手机号码
- `address[province]` (string) - 地址中的省份
- `address[province_code]` (string) - 地址中省份的编码，该编码可以是自定义编号或者为二位的ISO 3166-2国际编码
- `address[zip]` (string) - 地址的邮编信息
- `address[def]` (boolean) - 是否默认地址。`true`默认地址、`false`非默认地址

**示例:**
1. 新增收货地址:
```html
{{#customer_address_form return_to=routes.account_url}}
<input type="text" name="address[address1]" placeholder="address" />
<input class="submit-button" type="submit" value="submit">
{{/customer_address_form}}
```

2. 编辑收货地址:
```html
{{#customer_address_form address=customer.editing_address return_to=routes.account_url}}
<input type="text" name="address[first_name]" value="{{form.address.first_name}}"/>
<input class="submit-button" type="submit" value="submit">
{{/customer_address_form}}
```

3. 删除收货地址:
```html
{{#for address in customer.addresses}}
    {{#customer_address_form address_seq=address.id}}
        <input class="submit-button" type="submit" value="delete">
    {{/customer_address_form}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/customer-address-form)

### format_address

生成HTML地址显示，其中每个地址组件都根据地址所在地区排序。

**语法:**
```html
{{#format_address address /}}
```

**参数:**
- `address` (object) - address object

**示例:**
```html
{{#format_address address /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/format-address)

### company_account_application_form

生成公司账户申请表单。该功能仅适用于购买了SHOPLINE Enterprise套餐的商家。

**语法:**
```html
{{#company_account_application_form}}
    form_content
{{/company_account_application_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的跳转地址，默认为当前页面地址

**表单输入:**
- `company[email]` (email, 必填) - 公司主要联系人的邮箱
- `company[first_name]` (string) - 公司主要联系人的名字
- `company[last_name]` (string) - 公司主要联系人的姓氏
- `company[company_name]` (string, 必填) - 公司名称
- `company[shipping_address][mobile_phone]` (string) - 收货地址的手机号码
- `company[shipping_address][addr]` (string) - 收货地址的第一行。通常是街道地址或邮政信箱编号等信息
- `company[shipping_address][addr_two]` (string) - 收货地址的第二行。通常是公寓、套房或单元等信息
- `company[shipping_address][country]` (string) - 收货地址中的国家或区域
- `company[shipping_address][country_code]` (string) - 收货地址中国家或区域的二位码，遵循ISO 3166-1 (alpha 2)国际标准，例如`US`
- `company[shipping_address][province]` (string) - 收货地址中的省份
- `company[shipping_address][province_code]` (string) - 收货地址中省份的编码，该编码可以是自定义编号或者为二位的ISO 3166-2国际编码
- `company[shipping_address][city]` (string) - 收货地址中的城市
- `company[shipping_address][city_code]` (string) - 收货地址中城市的编码
- `company[shipping_address][district]` (string) - 收货地址中的区或县
- `company[shipping_address][district_code]` (string) - 收货地址中区或县的编码
- `company[shipping_address][zip_code]` (string) - 收货地址的邮编信息
- `company[billing_address][*]` - 账单地址相关字段，结构与收货地址相同
- `attribute[your_key]` (string) - 任意你想要收集的公司信息，例如：`<input name="attribute[age]" />`

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/company-account-application-form)

---

## 订单和支付

### payment_type_svg

为一个给定的支付类型生成一个HTML `<svg>` 标签。

**语法:**
```html
{{#payment_type_svg "affrim" /}}
```

**参数:**
- `type` (string, 必填) - 付款类型
- `class` (string) - 指定`<svg>`标记的class属性

**示例:**
1. 基本使用:
```html
{{#payment_type_svg "affrim" /}}
```

2. 添加class:
```html
{{#payment_type_svg "affrim" class="payment-svg-class" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/payment-type-svg)

### payment_button

生成一个承载网站快速结账按钮的HTML容器。该filter必须用于网站的product form里。

**语法:**
```html
{{#product_form product}}
    your code
    <div class="form__buttons">
        {{#payment_button/}}
    </div>
{{/product_form}}
```

**描述:** 生成一个HTML容器来承载产品的动态结账按钮。payment_button filter必须在product form内的form对象上使用。

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/payment-button)

---

## 商品和分类

### product_form

生成一个用于将产品款式添加到购物车的表单。该产品表单需要传入一个产品对象作为参数。

**语法:**
```html
{{#product_form product id="productFrom" class="productFrom"}}
    content
{{/product_form}}
```

**参数:**
- `product` (product) - 商品对象
- `HTML attributes` (string) - 可以传入属性名称和属性值参数来指定HTML属性

**语法关键词:**
- `content` - 显示在页面的`<form>`标签内的元素

**示例:**
```html
{{#product_form product id="productFrom" class="productFrom"}}
        <div style="margin-bottom:10px;">
            <input type="number" required step="1" form="product-form-{{section.id}}" name="quantity" min='1' max='999' value='1'/>
        </div>
        {{#var firstProduct = product.variants | first() /}}
        <div style="margin-bottom:10px;">
            <input type="hidden" name="id" value="{{firstProduct | default(product.selected_or_first_available_variant.id)}}" />
        </div>
        <button style="margin-bottom:10px;" class='btn btn-primary' type='submit'>{{ "products.product_list.add_to_cart" | t() }}</button>
        {{#payment_button /}}
    {{/product_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/product-form)

### product_item

生成一个用于存放产品数据的组件。该组件需要传入一个产品对象作为参数。

**语法:**
```html
{{#product_form product class="product-item"}}
    content
{{/product_form}}
```

**参数:**
- `product` (product) - 商品对象
- `HTML attributes` (string) - 可以传入属性名称和属性值参数来指定HTML属性

**语法关键词:**
- `content` - 显示在页面的`<product-item>`标签内的元素

**示例:**
```html
{{#product_item product}}
  <div>product-item</div>
{{/product_item}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/product-item)

## 链接和导航

### link_to_customer_login

生成指向客户登录页面的HTML链接。

**语法:**
```html
{{#link_to_customer_login str /}}
```

**语法关键词:**
- `str` - 链接文本

**示例:**
```html
{{#link_to_customer_login "Log in" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-customer-login)

### link_to_customer_logout

生成指向客户登出页面的HTML链接。

**语法:**
```html
{{#link_to_customer_logout str /}}
```

**语法关键词:**
- `str` - 链接文本

**示例:**
```html
{{#link_to_customer_logout "Logout" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-customer-logout)

### link_to_customer_register

生成指向客户注册页面的HTML链接。

**语法:**
```html
{{#link_to_customer_register str /}}
```

**语法关键词:**
- `str` - 链接文本

**示例:**
```html
{{#link_to_customer_register "Create an account" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-customer-register)

### link_to_tag

生成一个带有`href`属性的HTML `<a>`标签，其链接地址会包含传入的指定标签。点击该标签，即可跳转至当前所在的商品分类列表页。跳转后，页面将过滤并仅展示对应指定标签的商品。

**语法:**
```html
{{#link_to_tag "my_tag" class="link-class" my_attr="abc" }}
  content
{{/link_to_tag}}
```

**参数:**
- `tag` (string) - 产品标签
- `HTML attributes` (string) - 可以传入属性名称和属性值参数来指定HTML属性

**语法关键词:**
- `content` - 显示在页面的`<a>`标签内的文案

**描述:** 目前，仅支持在商品分类列表页使用，其他页面暂不支持。

**示例:**
```html
{{#for tag in collection.all_tags}}
        {{#link_to_tag tag class="link-class" my_attr="abc" }}
            {{tag}}
        {{/link_to_tag}}
    {{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-tag)

### link_to_add_tag

生成一个带有`href`属性的HTML `<a>`标签，其链接地址会包含传入的指定标签。点击该标签，即可跳转至当前所在的商品分类列表页。跳转后，页面将过滤并展示对应指定标签的商品。若页面链接本身已携带其他标签，指定标签会在原有标签基础上追加筛选展示。

**语法:**
```html
{{#link_to_add_tag "my_tag" class="link-class" my_attr="abc" }}
    content
{{/link_to_add_tag}} 
```

**参数:**
- `tag` (string, 必填) - 产品类型
- `HTML attributes` (string) - 可以传入属性名称和属性值参数来指定HTML属性

**语法关键词:**
- `content` - 显示在页面的`<a>`标签内的文案

**描述:** 目前，仅支持在商品分类列表页使用，其他页面暂不支持。

**示例:**
```html
{{#for tag in collection.all_tags}}
    {{#link_to_add_tag tag class="link-class" my_attr="abc" }}
        {{tag}}
    {{/link_to_add_tag}} 
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-add-tag)

### link_to_remove_tag

生成一个带`href`属性的HTML `<a>`标签，点击该标签可跳转至当前所在的分类列表页。跳转后，页面将过滤展示`url`中携带标签对应的商品，同时排除传入标签对应的商品。

**语法:**
```html
{{#link_to_remove_tag "my_tag" class="link-class" my_attr="abc" }}
    content
{{/link_to_remove_tag}} 
```

**参数:**
- `tag` (string, 必填) - 产品类型
- `HTML attributes` (string) - 可以传入属性名称和属性值参数来指定HTML属性

**语法关键词:**
- `content` - 显示在页面的`<a>`标签内的文案

**描述:** 目前，仅支持在分类列表页使用，其他页面暂不支持。

**示例:**
```html
{{#for tag in collection.all_tags}} 
    {{#link_to_add_tag tag class="link-class" my_attr="abc" }}
        {{tag}} 
    {{/link_to_add_tag}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-remove-tag)

### link_to_type

生成一个带有`href`属性的HTML `<a>`标签，点击该标签可跳转至当前所在的分类列表页。该标签的链接会包含传入的指定商品类型，跳转后，新页面将过滤展示对应指定商品类型的商品。

**语法:**
```html
{{#link_to_type "content" class="link-class" my_attr="abc"/}}
```

**参数:**
- `tag` (string) - 商品类型
- `HTML attributes` (string) - 可以传入属性名称和属性值参数来指定HTML属性

**语法关键词:**
- `content` - 显示在页面的`<a>`标签内的文案

**示例:**
```html
{{#for type in collection.all_types}}
    {{#link_to_type type class="link-class" my_attr="abc" /}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-type)

### link_to_vendor

生成一个带有`href`属性的HTML `<a>`标签，点击该标签可跳转至当前所在的分类列表页。该标签的链接会包含传入的指定商品厂商信息，跳转后，新页面将过滤展示对应指定商品厂商的商品。

**语法:**
```html
{{#link_to_vendor "content" class="link-class" my_attr="abc"/}}
```

**参数:**
- `tag` (string) - 商品厂商
- `HTML attributes` (string) - 可以传入属性名称和属性值参数来指定HTML属性

**语法关键词:**
- `content` - 显示在页面的`<a>`标签内的文案

**示例:**
```html
{{#for vendor in collection.all_vendors}}
        {{#link_to_vendor vendor class="link-class" my_attr="abc"/}}
    {{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to-vendor)

### link_to

生成HTML `<a>`标签。

**语法:**
```html
{{#link_to url}}{{/link_to}}
```

**参数:**
- `url` (string) - 需要跳转的url

**示例:**
```html
{{#link_to product.url}}
  {{product.title}}
{{/link_to}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/link-to)

---

## 媒体和资源

### image_tag

生成指定图像的HTML `<img>`标签。

**语法:**
```html
{{#image_tag imageUrl [attribute=any] /}}
```

**参数:**
- `imageUrl` (string) - 通过image_url filter返回的图片CDN链接

**示例:**
```html
{{#image_tag product | image_url(width=100) /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/image-tag)

### video_tag

生成指定视频的播放器 `<video>`标签。

**语法:**
```html
{{#video_tag media /}}
```

**参数:**
- `media` (object) - 媒体对象

**可选参数:**
- `image_size` (string) - 指定视频封面图宽高。格式为`{width}x{height}`，可仅设置宽或者高

**描述:** 目前仅支持`.mp4`格式的视频。

**示例:**
1. 基本使用:
```html
{{#for media in product.media}}
    {{#switch media.media_type}}
        {{#case "video" /}}
            {{#video_tag media /}}
    {{/switch}}
{{/for}}
```

2. 设置封面图宽度:
```html
{{#for media in product.media}}
    {{#switch media.media_type}}
        {{#case "video" /}}
            {{#video_tag media image_size="100x" /}}
    {{/switch}}
{{/for}}
```

3. 添加HTML属性:
```html
{{#for media in product.media}}
    {{#switch media.media_type}}
        {{#case "video" /}}
            {{#video_tag media autoplay=true loop=true /}}
    {{/switch}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/video-tag)

### external_video_tag

生成指定外部视频的播放器 `<iframe>`标签。

**语法:**
```html
{{#external_video_tag videoUrl attribute=any /}}
```

**参数:**
- `videoUrl` (string) - 外部视频URL

**描述:** 目前仅支持YouTuBe的视频链接。

**示例:**
1. 基本使用:
```html
{{#for media in product.media}}
    {{#switch media.media_type}}
        {{#case "external_video" /}}
            {{#if media.host == "youtube"}}
                {{#external_video_tag media | external_video_url(autoplay=true, loop=false) /}}
            {{/if}}
    {{/switch}}
{{/for}}
```

2. 添加HTML属性:
```html
{{#for media in product.media}}
    {{#switch media.media_type}}
        {{#case "external_video" /}}
            {{#if media.host == "youtube"}}
                {{#external_video_tag media | external_video_url(autoplay=true, loop=false) class="video-media-youtube" frameborder="0" /}}
            {{/if}}
    {{/switch}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/external-video-tag)

### placeholder_svg

生成指定名称类型的 `<svg>`标签。

**语法:**
```html
{{#placeholder_svg name /}}
```

**参数:**
- `name` (string) - 指定的名称类型

**可选参数:**
- `class` (string) - 自定义类

**示例:**
1. 基本使用:
```html
{{#placeholder_svg "product-1" /}}
```

2. 添加class属性:
```html
{{#placeholder_svg "product-1" class="custom-class" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/placeholder-svg)

## 模板和组件

### section

渲染静态section。

**语法:**
```html
{{#section "section_name" /}}
```

**参数:**
- `section_name` (string) - 对应sections目录下的section文件夹名字

**描述:** 静态section是指无法在可视化编辑器中拖动改变组件顺序的组件。

**示例:**
```html
{{#section "header" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/section)

### sections

渲染section group，当前组件只允许在`layout`模板中使用。

**语法:**
```html
{{#sections "file_name" /}}
```

**语法关键词:**
- `file_name` - `sections/*.json` sections目录下的json文件名字，比如默认的`sections/header.json`这里需要写成`header`

**示例:**
```html
{{#sections "header" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/sections)

### blocks

渲染当前作用域下的所有block，只能在section和block模板中使用，会自动遍历当前层级所有的block，作用域内会下发`forblock` object，支持做一些特殊逻辑处理，需要搭配block tag渲染内容。

**语法:**
```html
{{#blocks}}
  {{#block /}}
{{/blocks}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/blocks)

### block

渲染当前迭代作用域中的block，需配合blocks tag使用。

**语法:**
```html
{{#blocks}}
  {{#block [hash...] /}}
{{/blocks}}
```

**语法关键词:**
- `hash` - 支持传入参数到block组件

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/block)

### component

渲染指定的公共组件，组件可以是全局组件（component目录下）或者私有section/block组件（对应section/block目录下）。

**语法:**
```html
{{#component file_path [hash...] /}}
```

**语法关键词:**
- `file_path` - 组件文件路径，可以是相对路径或者绝对路径，相对路径需要以`./`开头，绝对路径就是`components/`下的文件
- `hash` - 动态hash参数（key=value），不限制个数，用于传入component中需要的变量参数

**描述:** component组件是隔离作用域的，如果需要外部变量需要手动通过hash参数传入，Sline全局object不限制。

**示例:**
1. 使用全局组件:
```html
{{#component "title" /}}
```

2. 引入私有组件:
```html
{{#component "./title" /}}
```

3. 组件传递参数:
```html
<!--! sections/header/header.html -->
{{#component "./title" title=section.settings.title show=true /}}

<!--! sections/header/title.html -->
{{#if show}}
    {{ title }}
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/component)

### schema

schema是用于定义可视化编辑器动态组件的配置项，标签内的内容是一个json。

**语法:**
```html
{{#schema}}
json_content
{{/schema}}
```

**语法关键词:**
- `json_content` - 可视化编辑器配置

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/schema)

---

## 变量和数据

### var

定义一个变量。

**语法:**
```html
{{#var variable = value /}}
```

**语法关键词:**
- `variable` - 定义的变量名
- `value` - 定义的变量值

**描述:** 变量不可以重复定义，重复定义，当前模板不会有任何输出。需要更新值需要使用set tag。

**示例:**
1. 声明且定义变量:
```html
{{# var brand = product.brand | upcase() /}}
{{ brand }}
```

2. 只声明变量:
```html
{{# var brand /}}
{{#set brand = product.brand /}}
{{ brand }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/var)

### set

修改已有变量的值。

**语法:**
```html
{{#set variable = value /}}
```

**语法关键词:**
- `variable` - 需要修改的变量名
- `value` - 更新的变量值

**描述:** 变量必须要提前使用`var`或者`capture`声明。设置的变量必须要和定义的变量数据类型一致。

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/set)

### capture

创建一个string变量。

**语法:**
```html
{{#capture variable}}
  value
{{/capture}}
```

**参数:**
- `variable` (string) - 需要定义的变量名

**描述:** 您可以使用Sline逻辑和变量创建复杂的字符串。

**示例:**
```html
{{#capture title}}
  {{product.title}} - {{shop.name}}
{{/capture}}

{{{title}}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/capture)

---

## HTML生成

### time_tag

将时间戳转换为HTML `<time>`标记。

**语法:**
```html
{{#time_tag timestring [format=string] /}}
```

**参数:**
- `timestring` (string) - 需要转换的时间字符串

**可选参数:**
- `format` (string) - 日期的格式化类型，支持的类型：`abbreviated_date`、`basic`、`date`、`date_at_time`、`default`、`on_date`，也可使用占位符自定义日期输出的格式

**示例:**
```html
{{#time_tag product.published_at /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/time-tag)

### style

生成HTML `<style>`标签。

**语法:**
```html
{{#style [attr=value]}} content {{/style}}
```

**示例:**
```html
{{#style media="all"}}
.title {
  color: red;
}
{{/style}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/style)

### script

为给定的资源URL生成HTML `<script>`标记。该标签的type属性为`text/javascript`。

**语法:**
```html
{{#script url}}{{/script}}
```

**参数:**
- `url` (string) - 资源URL

**示例:**
```html
{{#script "base/index.js" | asset_url() }}
{{/script}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/script)

### stylesheet

为一个给定的CSS资源URL生成一个HTML `<link>`标签。

**语法:**
```html
{{#stylesheet url [preload=boolean] [media=string] /}}
```

**参数:**
- `url` (string) - CSS资源URL

**可选参数:**
- `preload` (boolean) - 是否需要预加载，该属性为`true`时会对该资产URL也会添加到Link标头中
- `media` (string) - 设置media属性

**示例:**
```html
{{#stylesheet "base/index.css" | asset_url() /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/stylesheet)

### preload_tag

生成一个HTML `<link>`标签，其rel属性为preload，用于优先加载Shopline托管的特定资源。

**语法:**
```html
{{#preload_tag url [as=string] [rel=string] /}}
```

**参数:**
- `url` (string) - 需要预加载的资源url

**可选参数:**
- `as` (string) - 设置`as`属性
- `rel` (string) - 设置`rel`属性

**描述:** 你应该谨慎使用此过滤器。例如，考虑只预加载渲染所需的资源首屏内容。

**示例:**
```html
{{#preload_tag "base/index.js" | asset_url() /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/preload-tag)

### highlight

用一个class属性为`highlight`的HTML `<strong>`标记包裹给定字符串中特定字符串的所有实例。

**语法:**
```html
{{#highlight search}}content{{/highlight}}
```

**参数:**
- `search` (string) - 需要包装的字符串，该字符串必须在`content`中出现

**示例:**
```html
{{#highlight "[AB001]"}}{{product.title}}{{/highlight}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/highlight)

### layout

指定渲染的layout，仅能在html template中使用。

**语法:**
```html
{{#layout name /}}
```

**参数:**
- `name` (string) - 您要使用的布局文件的名称（用引号括起来），或者为无布局（`none`）

**描述:** 默认使用 layouts/theme.html

**示例:**
1. 不使用layout：
```html
{{#layout none /}}
```

2. 使用指定模板：
```html
{{#layout "password" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/layout)

### content

渲染指定类型动态内容。

**语法:**
```html
{{#content content_type /}}
```

**参数:**
- `content_type` (string) - 常量枚举字符串 `header` `footer` `layout` `blocks`

**可适用的内容枚举:**
- `header`：填充页头，仅限在layout中使用
- `footer`：填充页脚，仅限在layout中使用
- `layout`：填充模板内容，仅限在layout中使用
- `blocks`：渲染当前 section/block 下的所有子block

**示例:**
```html
{{#content "blocks" /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/content)

---

## 其他表单和工具

### localization_form

生成用于国家/地区、语言切换的提交表单。

**语法:**
```html
{{#localization_form /}} custom code {{/localization_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的重定向URL，默认为当前页面

**描述:** 此表单标签适用于以下两种类型的表单提交：
- 国家/地区选择器
- 语言选择器

**示例:**
1. 国家/地区选择器：
```html
{{#localization_form enctype="multipart/form-data" accept-charset="UTF-8"}}
  <select name="country_code" onchange="this.form.submit();">
    {{#for country in localization.available_countries}}
      <option value="{{country.iso_code}}" {{#if localization.country.iso_code == country.iso_code}}selected{{/if}}>
        {{country.name}}（{{country.currency.iso_code}}
        {{country.currency.symbol}}）
      </option>
    {{/for}}
  </select>
{{/localization_form}}
```

2. 语言选择器：
```html
{{#localization_form enctype="multipart/form-data" accept-charset="UTF-8"}}
  <select name="locale_code" onchange="this.form.submit();">
    {{#for language in localization.available_languages}}
      <option value="{{language.iso_code}}" {{#if localization.language.endonym_name == language.endonym_name}}selected{{/if}}>
        {{language.endonym_name}}
      </option>
    {{/for}}
  </select>
{{/localization_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/localization-form)

### storefront_password_form

生成店铺密码表单。

**语法:**
```html
{{#storefront_password_form}}
  form_content
{{/storefront_password_form}}
```

**可选参数:**
- `return_to` (string) - 表单提交后的重定向URL，默认为当前页面

**表单输入:**
- `password` (password, 必填) - 店铺密码

**示例:**
```html
{{#storefront_password_form}}
  {{#if form.posted_successfully}}
    <div>Submit Successfully</div>
  {{/if}}

  {{#if form.errors.messages}}
    <div>{{form.errors.messages}}</div>
  {{/if}}

  <div class="fields">
    <label class="field">
      <input type="password" name="password" placeholder="Please enter password" required>
    </label>
    <div>
      <input type="submit" value="Submit">
    </div>
  </div>
{{/storefront_password_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/storefront-password-form)

### order_tracking_form

生成一个查询订单表单，允许客户在不登录的情况下通过账号和订单编号查询订单信息。

**语法:**
```html
{{#order_tracking_form /}} custom code {{/order_tracking_form}}
```

**表单输入:**
- `order_tracking[order_number]` (text, 必填) - 订单编号
- `order_tracking[email]` (email, 选填) - 订单邮箱
- `order_tracking[phone]` (text, 选填) - 订单手机号
- `order_tracking[phone_area_code]` (text, 选填) - 订单手机区号

**示例:**
1. 使用邮箱查询订单：
```html
{{#order_tracking_form id="OrderTrackingForm"}}
  <div class="fields">
    <label class="field">
      <input type="email" name="order_tracking[email]" placeholder="Please enter email" required>
    </label>
    <label class="field">
      <input type="text" name="order_tracking[order_number]" placeholder="Please enter order number" required>
    </label>
    <div>
      <input type="submit" value="Submit">
    </div>
  </div>
{{/order_tracking_form}}
```

2. 使用手机号查询订单：
```html
{{#order_tracking_form id="OrderTrackingForm"}}
  <div class="fields">
    <label class="field">
      <input type="text" name="order_tracking[phone_area_code]" placeholder="Please enter order phone area code" required>
    </label>
    <label class="field">
      <input type="text" name="order_tracking[phone]" placeholder="Please enter phone" required>
    </label>
    <label class="field">
      <input type="text" name="order_tracking[order_number]" placeholder="Please enter order number" required>
    </label>
    <div>
      <input type="submit" value="Submit">
    </div>
  </div>
{{/order_tracking_form}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/order-tracking-form)

### delete_customer_form

生成注销账号表单。

**语法:**
```html
{{#delete_customer_form}}
    form_content
{{/delete_customer_form}}
```

**表单输入:**
- `customer[verifycode]` (number, 必填) - 验证码

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/delete-customer-form)

---

## 其他工具

### metafield_tag

生成包含元字段数据的HTML。

**语法:**
```html
{{#metafield_tag metafield /}}
```

**参数:**
- `metafield` (object) - metafield数据

**支持的元字段类型:**
- `boolean` 布尔值
- `date` 日期
- `date_at_time` 日期与时间
- `json` JSON
- `money` 资金
- `rich_text_field` 富文本
- `multi_line_text_field` 多行文本
- `color` 颜色值
- `number_decimal` 浮点型数字
- `number_integer` 整型数字
- `rating` 评分值
- `url` URL
- `weight` 重量
- `volume` 体积
- `dimension` 尺寸
- `single_line_text_field` 单行文本
- `collection_reference` 分类集合标题
- `page_reference` 页面标题
- `product_reference` 商品标题
- `variant_reference` 变体标题
- `file_reference` 文件URL

**示例:**
```html
{{#var metafield_ns = product | get_metafields("my_fields") /}}

{{#metafield_tag metafield_ns.my_key /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/tag/metafield-tag)

---

## 总结

本文档已完整收录了Sline模板引擎中所有可用的标签，按功能分类整理并提供了详细的使用说明和示例。每个标签都包含：

- 中文描述
- 标准语法格式  
- 详细参数说明
- 实际使用示例
- 官方文档链接

希望这份文档能帮助开发者更好地使用Sline模板引擎的标签功能。

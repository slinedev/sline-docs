# Sline Object API 参考文档

本文档提供了Sline模板引擎中所有可用对象(Object)的详细说明。根据objects.json完整结构整理，确保100%覆盖所有64个对象。

## 目录

- [基础对象](#基础对象)
- [商店和页面](#商店和页面)
- [商品相关](#商品相关)
- [客户和账户](#客户和账户)
- [订单和支付](#订单和支付)
- [购物车](#购物车)
- [博客和文章](#博客和文章)
- [表单和输入](#表单和输入)
- [地址和位置](#地址和位置)
- [媒体和资源](#媒体和资源)
- [本地化和语言](#本地化和语言)
- [模板和结构](#模板和结构)
- [搜索和过滤](#搜索和过滤)
- [分页和导航](#分页和导航)
- [折扣和促销](#折扣和促销)
- [B2B功能](#b2b功能)
- [工具和助手](#工具和助手)
- [集合和列表](#集合和列表)

---

## 基础对象

### page_title

用于为搜索引擎列表和社交媒体预览指定页面的标题。

**属性类型:** string

**描述:** 可以用来为搜索引擎列表和社交媒体预览指定页面的标题，在没有资源 handle 的页面会输出店铺名称。

**示例:**
```html
<title>{{page_title}}</title>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/page-title)

### page_description

用于在搜索引擎列表和当前页面的社交媒体预览中显示的描述。

**属性类型:** string

**示例:**
```html
<meta name="description" content="{{page_description}}" />
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/page-description)

### page_image

用于在搜索引擎列表和当前页面的社交媒体预览中显示的图片。

**属性类型:** image

**示例:**
```html
{{#if page_image.src}}
  <meta property="og:image" content="{{page_image.src}}" />
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/page-image)

### handle

handle是字符串，用于在Shopline模板中访问资源。

**主要属性:**
- 是资源的唯一标识符
- 用于URL生成
- 可以用于资源查找

**示例:**
```html
<a href="/products/{{product.handle}}">{{product.title}}</a>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/handle)

### page

页面信息。

**主要属性:**
- `author` (string) - 页面作者
- `content` (string) - 页面内容
- `created_at` (string) - 页面创建时间
- `handle` (string) - 页面handle
- `id` (string) - 页面ID
- `published_at` (string) - 页面发布时间
- `summary` (string) - 页面摘要
- `template_suffix` (string) - 页面模板后缀
- `title` (string) - 页面标题
- `updated_at` (string) - 页面更新时间
- `url` (string) - 页面URL

**示例:**
```html
<article>
  <h1>{{page.title}}</h1>
  <div>{{page.content}}</div>
  <p>最后更新：{{page.updated_at | date}}</p>
</article>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/page)

### template

当前模板的信息。

**主要属性:**
- `name` (string) - 模板名称
- `suffix` (string) - 模板后缀
- `directory` (string) - 模板目录

**示例:**
```html
<body class="template-{{template.name}}">
  <!-- 页面内容 -->
</body>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/template)

### request

包含当前HTTP请求的相关信息。

**主要属性:**
- `host` (string) - 请求的主机名
- `page_type` (string) - 页面类型
- `path` (string) - 请求路径
- `locale` (object) - 请求的语言环境

**示例:**
```html
<div class="page-{{request.page_type}}">
  <!-- 页面内容 -->
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/request)

---

## 商店和页面

### shop

包含店铺的基本信息和设置。

**主要属性:**
- `currency` (string) - 店铺的货币
- `description` (string) - 店铺描述
- `domain` (string) - 店铺域名
- `email` (string) - 店铺邮箱
- `id` (string) - 店铺ID
- `name` (string) - 店铺名称
- `phone` (string) - 店铺电话
- `url` (string) - 店铺URL

**示例:**
```html
<h1>{{shop.name}}</h1>
<p>{{shop.description}}</p>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/shop)

### routes

包含店铺中所有重要页面的URL路径。

**主要属性:**
- `account_url` (string) - 账户页面URL
- `cart_url` (string) - 购物车页面URL
- `root_url` (string) - 根页面URL
- `search_url` (string) - 搜索页面URL

**示例:**
```html
<a href="{{routes.cart_url}}">购物车</a>
<a href="{{routes.account_url}}">我的账户</a>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/routes)

---

## 商品相关

### product

商店里面的一件商品。

**主要属性:**
- `available` (boolean) - 商品是否可用
- `compare_at_price` (number) - 商品的对比价格
- `content` (string) - 商品的描述内容
- `created_at` (string) - 商品创建时间
- `description` (string) - 商品描述
- `featured_image` (image) - 商品的特色图片
- `handle` (string) - 商品的 handle
- `id` (string) - 商品ID
- `images` (array) - 商品图片数组
- `price` (number) - 商品价格
- `title` (string) - 商品标题
- `type` (string) - 商品类型
- `url` (string) - 商品的相对URL地址
- `variants` (array) - 商品款式列表
- `vendor` (array) - 商品品牌

**示例:**
```html
<h1>{{product.title}}</h1>
<p>{{product.description}}</p>
<div class="price">{{product.price | money}}</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/product)

### collection

商品分类信息。

**主要属性:**
- `all_products_count` (number) - 分类中所有商品的数量
- `all_tags` (array) - 分类中所有商品的标签
- `description` (string) - 分类描述
- `featured_image` (image) - 分类特色图片
- `handle` (string) - 分类handle
- `id` (string) - 分类ID
- `products` (array) - 分类中的商品
- `title` (string) - 分类标题
- `url` (string) - 分类相对URL

**示例:**
```html
<h1>{{collection.title}}</h1>
{{#for product in collection.products}}
  <div>{{product.title}}</div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/collection)

### product_option

商品规格，例如尺寸或颜色。

**主要属性:**
- `id` (string) - 商品规格的ID
- `name` (string) - 商品规格的名称
- `position` (number) - 规格的位置
- `selected_value` (string) - 当前选择的商品规格值
- `values` (array) - 规格的所有可选值

**示例:**
```html
{{#for option in product.options}}
  <div class="product-option">
    <label>{{option.name}}:</label>
    <select name="option{{option.position}}">
      {{#for value in option.values}}
        <option value="{{value}}" {{#if value == option.selected_value}}selected{{/if}}>
          {{value}}
        </option>
      {{/for}}
    </select>
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/product-option)

### recommendations

基于销售数据、产品描述和集合关系为特定产品提供的产品推荐。

**主要属性:**
- `performed` (boolean) - 当在使用产品推荐API和区段渲染API渲染的区段内被引用时，返回true
- `products` (array) - 推荐的产品
- `products_count` (number) - 推荐产品的数量

**示例:**
```html
{{#if recommendations.performed}}
  <div class="product-recommendations">
    <h3>推荐商品</h3>
    {{#for product in recommendations.products}}
      <div class="recommended-product">
        <a href="{{product.url}}">
          <img src="{{product.featured_image | image_url}}" alt="{{product.title}}">
          <h4>{{product.title}}</h4>
          <p>{{product.price | money}}</p>
        </a>
      </div>
    {{/for}}
  </div>
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/recommendations)

---

## 客户和账户

### customer

当前登录的客户信息。

**主要属性:**
- `accepts_marketing` (boolean) - 客户是否接受营销邮件
- `addresses` (array) - 客户的所有个人收货地址
- `email` (string) - 客户邮箱
- `first_name` (string) - 客户名字
- `id` (string) - 客户ID
- `last_name` (string) - 客户姓氏
- `orders` (array) - 客户的订单
- `phone` (string) - 客户电话

**示例:**
```html
{{#if customer}}
  <h2>欢迎回来，{{customer.first_name}}!</h2>
  <p>您的邮箱：{{customer.email}}</p>
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/customer)

---

## 订单和支付

### order

一个订单。

**主要属性:**
- `billing_address` (address) - 账单地址
- `cancelled` (boolean) - 订单是否被取消
- `created_at` (string) - 订单创建时间
- `customer` (customer) - 订单客户
- `email` (string) - 订单关联邮箱
- `financial_status` (number) - 订单财务状况
- `line_items` (array) - 订单项目
- `name` (string) - 订单名称
- `order_number` (string) - 订单编号
- `shipping_address` (address) - 收货地址
- `total_price` (number) - 订单总价

**示例:**
```html
<h2>订单 {{order.name}}</h2>
<p>总金额：{{order.total_price | money}}</p>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/order)

### shipping_method

有关订单运输方式的信息。

**主要属性:**
- `id` (string) - 订单运输号ID
- `original_price` (number) - 应用折扣前运输价格
- `price` (number) - 应用折扣后运输价格
- `tax_lines` (array) - 运输方式的税额
- `title` (string) - 运输方式的标题

**示例:**
```html
<div class="shipping-info">
  <h4>{{shipping_method.title}}</h4>
  {{#if shipping_method.original_price != shipping_method.price}}
    <s>{{shipping_method.original_price | money}}</s>
  {{/if}}
  <span>{{shipping_method.price | money}}</span>
  {{#for tax in shipping_method.tax_lines}}
    <p>税费：{{tax.title}} ({{tax.rate}}%) - {{tax.price | money}}</p>
  {{/for}}
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/shipping-method)

### tax_line

关于结账或订单的税费行的信息。

**主要属性:**
- `price` (number) - 以货币子单位表示的税额
- `rate` (number) - 税率的小数值
- `title` (string) - 税务的标题

**示例:**
```html
<div class="tax-breakdown">
  {{#for tax in order.tax_lines}}
    <div class="tax-line">
      <span>{{tax.title}} ({{tax.rate | times(100)}}%)</span>
      <span>{{tax.price | money}}</span>
    </div>
  {{/for}}
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/tax-line)

---

## 购物车

### cart

购物车信息。

**主要属性:**
- `empty` (boolean) - 购物车是否为空
- `item_count` (number) - 购物车中的商品数量
- `items` (line_item) - 购物车中的商品行
- `total_price` (number) - 购物车总价格

**示例:**
```html
{{#if cart.empty}}
  <p>购物车为空</p>
{{#else}}
  <p>购物车中有 {{cart.item_count}} 件商品</p>
  <p>总价：{{cart.total_price | money}}</p>
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/cart)

---

## 博客和文章

### blog

商店中的一篇博客信息。

**主要属性:**
- `all_tags` (array) - 文章集合中所有的标签
- `articles` (array) - 博客集合中的文章
- `articles_count` (number) - 博客集合中的文章总数
- `comments_enabled` (boolean) - 是否启用评论
- `handle` (string) - 博客集合的handle
- `title` (string) - 博客集合的标题
- `url` (string) - 博客集合的相对URL

**示例:**
```html
<h1>{{blog.title}}</h1>
{{#for article in blog.articles}}
  <article>
    <h2>{{article.title}}</h2>
  </article>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/blog)

### article

博客文章信息。

**主要属性:**
- `author` (string) - 文章作者的全名
- `comments_count` (number) - 发表的文章评论数量
- `content` (string) - 文章内容
- `created_at` (string) - 创建文章的时间
- `excerpt` (string) - 文章摘要
- `handle` (string) - 文章的handle
- `id` (string) - 文章ID
- `title` (string) - 文章标题
- `url` (string) - 文章的相对URL

**示例:**
```html
<article>
  <h1>{{article.title}}</h1>
  <p>作者：{{article.author}}</p>
  <div>{{article.content}}</div>
</article>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/article)

---

## 表单和输入

### form

表单对象，包含表单提交状态和错误信息。

**主要属性:**
- `errors` (object) - 表单错误信息
- `posted_successfully` (boolean) - 表单是否提交成功

**示例:**
```html
{{#if form.posted_successfully}}
  <div class="success">提交成功！</div>
{{/if}}
{{#if form.errors.messages}}
  <div class="error">{{form.errors.messages}}</div>
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/form)

---

## 地址和位置

### address

地址，例如客户地址或订单配送地址。

**主要属性:**
- `address1` (string) - 地址的第一行
- `address2` (string) - 地址的第二行
- `city` (string) - 地址的城市
- `country` (country) - 地址的国家
- `first_name` (string) - 客户的名
- `last_name` (string) - 客户的姓氏
- `phone` (string) - 地址的电话号码
- `province` (string) - 地址的省份

**示例:**
```html
{{#format_address address /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/address)

---

## 媒体和资源

### image

图片对象。

**主要属性:**
- `alt` (string) - 图片的替代文本
- `aspect_ratio` (number) - 图片的宽高比
- `height` (number) - 图片高度
- `id` (string) - 图片ID
- `src` (string) - 图片的源URL
- `width` (number) - 图片宽度

**示例:**
```html
<img src="{{image.src}}" alt="{{image.alt}}" width="{{image.width}}" height="{{image.height}}">
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/image)

### media

媒体对象，包括图片、视频等。

**主要属性:**
- `alt` (string) - 媒体的替代文本
- `height` (number) - 媒体高度
- `id` (string) - 媒体ID
- `media_type` (string) - 媒体类型
- `src` (string) - 媒体的源URL
- `width` (number) - 媒体宽度

**示例:**
```html
{{#switch media.media_type}}
  {{#case "image" /}}
    <img src="{{media.src}}" alt="{{media.alt}}">
  {{#case "video" /}}
    {{#video_tag media /}}
{{/switch}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/media)

---

## 本地化和语言

### localization

本地化信息，包含可用的国家和语言。

**主要属性:**
- `available_countries` (array) - 可用的国家列表
- `available_languages` (array) - 可用的语言列表
- `country` (country) - 当前国家
- `language` (language) - 当前语言

**示例:**
```html
<select name="country_code">
  {{#for country in localization.available_countries}}
    <option value="{{country.iso_code}}">
      {{country.name}}
    </option>
  {{/for}}
</select>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/localization)

### shop_locale

店铺下的语种信息。

**主要属性:**
- `endonym_name` (string) - 语种的名称
- `iso_code` (string) - 语种的代码
- `primary` (boolean) - 是否主要语种
- `root_url` (string) - 语种关联的根路径

**示例:**
```html
<select name="locale_code">
  {{#for language in localization.available_languages}}
    <option value="{{language.iso_code}}">{{language.endonym_name}}</option>
  {{/for}}
</select>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/shop-locale)

### curency

关于货币的信息，如ISO代码和符号。

**主要属性:**
- `iso_code` (string) - 货币的ISO代码
- `name` (string) - 货币的名称
- `symbol` (string) - 货币的符号

**示例:**
```html
<div class="currency-info">
  <span>{{curency.symbol}} {{curency.iso_code}}</span>
  <span>{{curency.name}}</span>
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/curency)

### country_option_tags

在Shopline管理后台的运费页面，为包含在运费区域内的每个国家和地区创建一个`<option>`标签。

**描述:** 每个`<option>`都设置了一个名为`data-provinces`的属性，包含一个JSON编码的该国家或地区的子区域数组。

**示例:**
```html
<select name="country">
  {{{ country_option_tags }}}
</select>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/country-option-tags)

### current_tags

当前页面应用的标签。

**描述:** 你可以给文章和产品添加标签。文章标签可用于过滤博客页面，仅显示带有特定标签的文章。

**示例:**
```html
{{#for tag in current_tags}}
  {{#link_to_tag tag}}
    {{tag}}
  {{/link_to_tag}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/current-tags)

---

## 模板和结构

### section

Section的内容和设置。

**主要属性:**
- `id` (string) - section的ID
- `settings` (any) - section的设置
- `blocks` (array) - section下的blocks
- `index` (number) - 当前section基于1开始的索引
- `index0` (number) - 当前section基于0开始的索引

**示例:**
```html
<section data-section-id="{{section.id}}">
  <h2>{{section.settings.title}}</h2>
  {{#blocks}}
    {{#block /}}
  {{/blocks}}
</section>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/section)

### block

Block的内容和设置。

**主要属性:**
- `id` (string) - block的ID
- `settings` (any) - block的设置
- `shopline_attributes` (string) - 在主题编辑器中使用的block的数据属性
- `type` (string) - block的类型
- `index` (number) - 当前block基于1开始的索引
- `index0` (number) - 当前block基于0开始的索引

**示例:**
```html
<div {{block.shopline_attributes}}>
  {{#switch block.type}}
    {{#case "text" /}}
      <p>{{block.settings.text}}</p>
    {{#case "image" /}}
      <img src="{{block.settings.image | image_url}}" alt="">
  {{/switch}}
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/block)

---

## 工具和助手

### forloop

有关父级 for 循环的信息。

**主要属性:**
- `first` (boolean) - 是否是第一次迭代
- `index` (number) - 当前迭代的位置，从1开始
- `index0` (number) - 当前迭代的位置，从0开始
- `last` (boolean) - 是否是最后一次迭代
- `length` (number) - 循环中的项目数

**示例:**
```html
{{#for product in collection.products}}
  <div class="{{#if forloop.first}}first{{/if}} {{#if forloop.last}}last{{/if}}">
    {{forloop.index}}: {{product.title}}
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/forloop)

### forblock

有关父级 blocks 循环的信息。

**主要属性:**
- `first` (boolean) - 是否是第一次迭代
- `index` (number) - 当前迭代的位置，从1开始
- `index0` (number) - 当前迭代的位置，从0开始
- `last` (boolean) - 是否是最后一次迭代
- `length` (number) - 循环中的block数
- `settings` (any) - 本地迭代中，当前block的settings

**示例:**
```html
{{#blocks}}
  <div class="block-{{forblock.index}}">
    {{#block /}}
  </div>
{{/blocks}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/forblock)

### additional_checkout_buttons

如果店铺有任何具有离站结账功能的付款提供商，例如 PayPal Express Checkout，则会返回 `true`。

**属性类型:** boolean

**描述:** 使用 `additional_checkout_buttons` 来检查是否存在这些支付提供商，通过使用 `content_for_additional_checkout_buttons` 来显示这些支付提供商关联的结账按钮。

**示例:**
```html
{{#if additional_checkout_buttons}}
    {{{content_for_additional_checkout_buttons}}}
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/additional-checkout-buttons)

### gift_card

礼品卡信息。

**主要属性:**
- `balance` (number) - 礼品卡剩余余额
- `code` (string) - 礼品卡代码
- `currency` (string) - 礼品卡发行所用货币的ISO代码
- `customer_id` (string) - 与礼品卡关联的客户ID
- `enabled` (boolean) - 礼品卡是否启用
- `expired` (boolean) - 礼品卡是否过期
- `expires_on` (string) - 礼品卡过期日期
- `initial_value` (number) - 礼品卡的初始余额
- `last_four_characters` (string) - 用于兑换礼品卡的代码的最后4个字符
- `product` (product) - 关联的礼品卡产品
- `properties` (array) - 礼品卡的属性
- `recipient` (object) - 礼品卡接收者信息
- `url` (string) - 礼品卡URL

**示例:**
```html
<div class="gift-card">
  <h2>礼品卡余额：{{gift_card.balance | money}}</h2>
  <p>代码：***{{gift_card.last_four_characters}}</p>
  {{#if gift_card.expires_on}}
    <p>过期日期：{{gift_card.expires_on | date}}</p>
  {{/if}}
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/gift-card)

### fulfillment

订单履约信息。

**主要属性:**
- `created_at` (string) - 履约创建时间
- `item_count` (number) - 履约中的商品行数量
- `line_items` (array) - 履约的订单项
- `status` (string) - 履约状态
- `tracking_company` (string) - 履约服务的名称
- `tracking_number` (string) - 履约的跟踪号码
- `tracking_url` (string) - 履约的跟踪号码的URL
- `updated_at` (string) - 履约更新时间

**示例:**
```html
{{#for fulfillment in order.fulfillments}}
  <div class="fulfillment">
    <p>状态：{{fulfillment.status}}</p>
    {{#if fulfillment.tracking_number}}
      <p>跟踪号：{{fulfillment.tracking_number}}</p>
      <a href="{{fulfillment.tracking_url}}">跟踪包裹</a>
    {{/if}}
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/fulfillment)

### line_item

订单项或购物车项的信息。

**主要属性:**
- `discount_allocations` (array) - 订单项的折扣分配
- `final_line_price` (number) - 订单项的最终价格
- `final_price` (number) - 订单项单价的最终价格
- `fulfillable_quantity` (number) - 可履约数量
- `fulfilled_quantity` (number) - 已履约数量
- `gift_card` (boolean) - 是否为礼品卡
- `grams` (number) - 订单项的重量（克）
- `id` (string) - 订单项ID
- `image` (image) - 订单项图片
- `line_price` (number) - 订单项的总价格
- `original_line_price` (number) - 订单项的原始总价格
- `original_price` (number) - 订单项的原始单价
- `price` (number) - 订单项的单价
- `product` (product) - 关联的产品
- `product_id` (string) - 产品ID
- `properties` (array) - 订单项的自定义属性
- `quantity` (number) - 订单项数量
- `requires_shipping` (boolean) - 是否需要运输
- `sku` (string) - 商品SKU
- `taxable` (boolean) - 是否需要征税
- `title` (string) - 订单项标题
- `total_discount` (number) - 订单项的总折扣金额
- `unit_price` (number) - 订单项的单位价格
- `url` (string) - 订单项的URL
- `variant` (variant) - 关联的商品款式
- `variant_id` (string) - 商品款式ID
- `variant_title` (string) - 商品款式标题
- `vendor` (string) - 商品品牌

**示例:**
```html
{{#for item in cart.items}}
  <div class="line-item">
    <img src="{{item.image | image_url(width=100)}}" alt="{{item.title}}">
    <h3>{{item.title}}</h3>
    <p>数量：{{item.quantity}}</p>
    <p>价格：{{item.line_price | money}}</p>
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/line-item)

### variant

商品款式信息。

**主要属性:**
- `available` (boolean) - 款式是否可用
- `barcode` (string) - 款式条形码
- `compare_at_price` (number) - 款式的对比价格
- `featured_image` (image) - 款式的特色图片
- `featured_media` (media) - 款式的特色媒体
- `id` (string) - 款式ID
- `image` (image) - 款式图片
- `inventory_management` (string) - 库存管理方式
- `inventory_policy` (string) - 库存策略
- `inventory_quantity` (number) - 库存数量
- `option1` (string) - 选项1的值
- `option2` (string) - 选项2的值
- `option3` (string) - 选项3的值
- `price` (number) - 款式价格
- `product` (product) - 关联的产品
- `requires_shipping` (boolean) - 是否需要运输
- `selected` (boolean) - 是否被选中
- `selling_plan_allocations` (array) - 销售计划分配
- `sku` (string) - 款式SKU
- `taxable` (boolean) - 是否需要征税
- `title` (string) - 款式标题
- `unit_price` (number) - 款式单位价格
- `unit_price_measurement` (object) - 单位价格测量
- `url` (string) - 款式URL
- `weight` (number) - 款式重量
- `weight_unit` (string) - 重量单位

**示例:**
```html
<select name="id">
  {{#for variant in product.variants}}
    <option value="{{variant.id}}" {{#if variant.selected}}selected{{/if}}>
      {{variant.title}} - {{variant.price | money}}
    </option>
  {{/for}}
</select>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/variant)

### comment

文章评论信息。

**主要属性:**
- `author` (string) - 评论作者
- `content` (string) - 评论内容
- `created_at` (string) - 评论创建时间
- `email` (string) - 评论者邮箱
- `id` (string) - 评论ID
- `status` (string) - 评论状态
- `updated_at` (string) - 评论更新时间
- `url` (string) - 评论URL

**示例:**
```html
{{#for comment in article.comments}}
  <div class="comment">
    <h4>{{comment.author}}</h4>
    <p>{{comment.content}}</p>
    <small>{{comment.created_at | date}}</small>
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/comment)

### country

国家信息。

**主要属性:**
- `currency` (object) - 国家货币信息
- `iso_code` (string) - 国家ISO代码
- `name` (string) - 国家名称
- `unit_system` (string) - 计量单位系统

**示例:**
```html
<p>当前国家：{{localization.country.name}}</p>
<p>货币：{{localization.country.currency.iso_code}}</p>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/country)

### currency

货币信息。

**主要属性:**
- `iso_code` (string) - 货币ISO代码
- `name` (string) - 货币名称
- `symbol` (string) - 货币符号

**示例:**
```html
<p>价格：{{product.price | money}} {{shop.currency}}</p>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/currency)

### metafield

元字段信息。

**主要属性:**
- `id` (string) - 元字段ID
- `key` (string) - 元字段键
- `namespace` (string) - 元字段命名空间
- `type` (string) - 元字段类型
- `value` (any) - 元字段值

**示例:**
```html
{{#var custom_field = product | get_metafields("custom") /}}
{{#if custom_field.description}}
  <p>{{custom_field.description.value}}</p>
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/metafield)

### menu

导航菜单信息。

**主要属性:**
- `handle` (string) - 菜单handle
- `id` (string) - 菜单ID
- `levels` (number) - 菜单层级数
- `links` (array) - 菜单链接
- `title` (string) - 菜单标题

**示例:**
```html
{{#var main_menu = menus.main /}}
<nav>
  {{#for link in main_menu.links}}
    <a href="{{link.url}}">{{link.title}}</a>
  {{/for}}
</nav>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/menu)

### link

菜单链接信息。

**主要属性:**
- `active` (boolean) - 链接是否激活
- `child_active` (boolean) - 子链接是否激活
- `child_current` (boolean) - 子链接是否为当前页面
- `current` (boolean) - 是否为当前页面
- `levels` (number) - 链接层级数
- `links` (array) - 子链接
- `object` (object) - 链接关联的对象
- `title` (string) - 链接标题
- `type` (string) - 链接类型
- `url` (string) - 链接URL

**示例:**
```html
{{#for link in menu.links}}
  <a href="{{link.url}}" class="{{#if link.active}}active{{/if}}">
    {{link.title}}
  </a>
  {{#if link.links}}
    <ul>
      {{#for child_link in link.links}}
        <li><a href="{{child_link.url}}">{{child_link.title}}</a></li>
      {{/for}}
    </ul>
  {{/if}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/link)

### page

页面信息。

**主要属性:**
- `author` (string) - 页面作者
- `content` (string) - 页面内容
- `created_at` (string) - 页面创建时间
- `handle` (string) - 页面handle
- `id` (string) - 页面ID
- `published_at` (string) - 页面发布时间
- `summary` (string) - 页面摘要
- `template_suffix` (string) - 页面模板后缀
- `title` (string) - 页面标题
- `updated_at` (string) - 页面更新时间
- `url` (string) - 页面URL

**示例:**
```html
<article>
  <h1>{{page.title}}</h1>
  <div>{{page.content}}</div>
  <p>最后更新：{{page.updated_at | date}}</p>
</article>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/page)

---

## 搜索和过滤

### search

店铺搜索查询的信息。

**主要属性:**
- `filters` (array) - 在搜索页面上设置的过滤器
- `performed` (boolean) - 是否成功执行了搜索
- `results` (any) - 搜索结果项目
- `results_count` (number) - 结果数量
- `sort_by` (string) - 搜索结果的排序顺序
- `sort_options` (string) - 搜索结果的可用排序选项
- `terms` (string) - 输入的搜索词
- `types` (array) - 执行搜索的对象类型

**示例:**
```html
{{#if search.performed}}
  <h2>搜索"{{search.terms}}"的结果 ({{search.results_count}})</h2>
  {{#for item in search.results}}
    <div class="search-result">
      <h3>{{item.title}}</h3>
      <p>{{item.summary}}</p>
    </div>
  {{/for}}
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/search)

### filter

店面过滤器。

**主要属性:**
- `active_values` (array) - 当前处于活动状态的过滤器的值
- `false_value` (string) - `false` 过滤值
- `id` (string) - 过滤器的唯一标识符
- `label` (string) - 过滤器的显示标签
- `max_value` (object) - 价格范围过滤器的最大值
- `min_value` (object) - 价格范围过滤器的最小值
- `range_max` (string) - 搜索结果或分类中的最高产品价格
- `range_min` (string) - 搜索结果或分类中的最低产品价格
- `true_value` (string) - `true` 过滤值
- `type` (string) - 过滤器的类型（boolean、list、price_range）
- `url_to_remove` (string) - 删除了与过滤器相关的URL参数的当前页面URL
- `values` (array) - 过滤器的值

**示例:**
```html
{{#for filter in search.filters}}
  <h3>{{filter.label}}</h3>
  {{#for value in filter.values}}
    <input type="checkbox" name="{{filter.id}}" value="{{value.value}}">
    <label>{{value.label}} ({{value.count}})</label>
  {{/for}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/filter)

### filter_value

过滤器值对象。

**主要属性:**
- `active` (boolean) - 如果该值当前处于活动状态，则返回true
- `label` (string) - 过滤器值的面向客户的标签
- `param_name` (string) - 过滤器的URL参数
- `value` (string) - 过滤器的值
- `url_to_add` (string) - 添加过滤器的URL
- `url_to_remove` (string) - 移除过滤器的URL

**示例:**
```html
{{#for value in filter.values}}
  <div class="filter-option">
    {{#if value.active}}
      <a href="{{value.url_to_remove}}">✓ {{value.label}}</a>
    {{#else}}
      <a href="{{value.url_to_add}}">{{value.label}} ({{value.count}})</a>
    {{/if}}
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/filter-value)

---

## 分页和导航

### paginate

一组分页信息，可用于分页导航和分页数据展示。

**主要属性:**
- `parts` (array) - 分页部件，用于构建分页导航
- `list` (array) - 分页数据列表
- `current_offset` (number) - 当前页之前的页面上的项目总数
- `current_page` (number) - 当前页的页码
- `items` (number) - 需要分页的项目总数
- `page_param` (string) - 表示分页的URL参数
- `page_size` (number) - 每页显示的项目数
- `pages` (number) - 总页数
- `previous` (part) - 转到上一页的分页部件
- `next` (part) - 转到下一页的分页部件

**示例:**
```html
{{#var paginate = all_products | get_product_pagination(5) /}}
{{#for product in paginate.list}}
  {{#link_to product.url}}
    {{product.title}}
  {{/link_to}}
{{/for}}

<nav class="pagination">
  {{#if paginate.previous}}
    <a href="{{paginate.previous.url}}">上一页</a>
  {{/if}}
  <span>第 {{paginate.current_page}} 页，共 {{paginate.pages}} 页</span>
  {{#if paginate.next}}
    <a href="{{paginate.next.url}}">下一页</a>
  {{/if}}
</nav>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/paginate)

---

## 集合和列表

### collections

商店的全部商品分类。

**示例:**
```html
{{#for collection in collections }}
    {{#link_to collection.url}}
        {{collection.title}}
    {{/link_to}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/collections)

### all_products

店铺的全部商品。

**描述:** 可以在全部模版内使用，直接使用 `all_products` object 不会输出数据，需要结合 [get filter](/docs/sline/filter/get) 使用。

**示例:**
```html
{{#var product = all_products | get("earring-ab001") /}}
{{#link_to product.url}}
  {{product.title}}
{{/link_to}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/all-products)

### all_collections

店铺的全部商品分类。

**描述:** 直接使用 `all_collections` object不会输出数据，需要结合 [get filter](/docs/sline/filter/get) 一起使用。

**示例:**
```html
{{#var collection = all_collections | get("bottom") /}}
{{#link_to collection.url}}
  {{collection.title}}
{{/link_to}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/all-collections)

### all_pages

店铺的全部自定义页面。

**描述:** 直接使用 `all_pages` object 不会输出数据，需要结合[get filter](/docs/sline/filter/get)一起使用。

**示例:**
```html
{{#var page = all_pages | get("privacy-policy") /}}
{{#link_to page.url}}
  {{page.title}}
{{/link_to}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/all-pages)

### all_articles

商店博客中的所有文章。

**描述:** 直接使用 all_articles object 不会输出数据，需要结合[get filter](/docs/sline/filter/get)一起使用。

**示例:**
```html
{{#var article = all_articles | get("news/blog-2") /}}
{{#link_to article.url}}
  {{article.title}}
{{/link_to}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/all-articles)

### all_blogs

店铺的全部博客集合。

**描述:** 直接使用 `all_blogs` object 不会输出数据，需要结合[get filter](/docs/sline/filter/get)一起使用。

**示例:**
```html
{{#var blog = all_blogs | get("news") /}}
{{#link_to blog.url}}
  {{blog.title}}
{{/link_to}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/all-blogs)

---

## 折扣和促销

### discount_allocation

有关折扣如何影响商品的信息。

**主要属性:**
- `amount` (number) - 商品打折的金额
- `discount_application` (discount_application) - 应用的折扣详情信息

**示例:**
```html
{{#for allocation in line_item.discount_allocations}}
  <div class="discount">
    <span>折扣：{{allocation.discount_application.title}}</span>
    <span>金额：-{{allocation.amount | money}}</span>
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/discount-allocation)

### discount_application

有关折扣的信息。

**主要属性:**
- `target_selection` (string) - 行项目或者是物流线路所选择的折扣类型
- `target_type` (string) - 折扣适用的项目类型
- `title` (string) - 用于展示的折扣名称
- `total_allocated_amount` (number) - 折扣总额
- `value` (string) - 此折扣的优惠值
- `value_type` (string) - 折扣的值类型（fixed_amount或percentage）
- `activity_type` (number) - 商品行享受的活动类型
- `benefit_type` (number) - 商品行享受的优惠类型

**示例:**
```html
{{#for discount in order.discount_applications}}
  <div class="discount-info">
    <h4>{{discount.title}}</h4>
    <p>类型：{{discount.target_type}}</p>
    {{#if discount.value_type == "percentage"}}
      <p>折扣：{{discount.value}}%</p>
    {{#else}}
      <p>折扣：{{discount.value | money}}</p>
    {{/if}}
    <p>总额：-{{discount.total_allocated_amount | money}}</p>
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/discount-application)

---

## B2B功能

### checkout

客户的结账信息。

**主要属性:**
- `applied_gift_cards` (array) - 应用于结账的礼品卡
- `attributes` (object) - 客户与购物车一起输入的附加属性
- `billing_address` (address) - 结账时输入的账单地址
- `discount_applications` (array) - 结账的折扣应用
- `email` (string) - 结账的电子邮件地址
- `gift_cards_amount` (number) - 结账中应用的礼品卡总金额
- `id` (string) - 结账ID
- `line_items` (array) - 结账的订单项
- `line_items_subtotal_price` (number) - 结账的所有订单项价格总和
- `note` (string) - 客户与购物车一起输入的附加信息
- `shipping_address` (address) - 结账的收货地址
- `shipping_method` (shipping_method) - 结账的配送方式
- `shipping_price` (number) - 结账的配送价格
- `tax_price` (number) - 结账的总税额
- `total_price` (number) - 结账的总价格

**示例:**
```html
<div class="checkout-summary">
  <h2>订单摘要</h2>
  <p>总价：{{checkout.total_price | money}}</p>
  <p>配送费：{{checkout.shipping_price | money}}</p>
  <p>税费：{{checkout.tax_price | money}}</p>
  {{#if checkout.note}}
    <p>备注：{{checkout.note}}</p>
  {{/if}}
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/checkout)

### company

B2B公司信息。

**主要属性:**
- `available_locations` (array) - 当前客户可访问的公司地址列表
- `id` (string) - 公司ID
- `metafields` (array) - 适用于公司的元字段
- `name` (string) - 公司名称

**示例:**
```html
{{#if customer.company}}
  <div class="company-info">
    <h3>{{customer.company.name}}</h3>
    <p>公司ID：{{customer.company.id}}</p>
    {{#if customer.company.available_locations}}
      <h4>可用地点：</h4>
      {{#for location in customer.company.available_locations}}
        <p>{{location.name}}</p>
      {{/for}}
    {{/if}}
  </div>
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/company)

### company_location

客户下单时使用的公司地点。

**主要属性:**
- `current` (boolean) - 如果当前选择了该地点，则返回true
- `id` (string) - 地点ID
- `metafields` (array) - 适用于公司地点的元字段
- `name` (string) - 地点名称
- `shipping_address` (address) - 地点的收货地址
- `tax_registration_id` (number) - 地点的税号
- `url_to_set_as_current` (string) - 将地点设置为客户当前地点的URL

**示例:**
```html
{{#for location in company.available_locations}}
  <div class="location {{#if location.current}}current{{/if}}">
    <h4>{{location.name}}</h4>
    <p>税号：{{location.tax_registration_id}}</p>
    {{#if !location.current}}
      <a href="{{location.url_to_set_as_current}}">设为当前地点</a>
    {{/if}}
  </div>
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/company-location)

### policy

商店政策，例如隐私政策或退货政策。

**主要属性:**
- `id` (string) - 政策的ID
- `body` (string) - 政策的内容
- `title` (string) - 政策页的标题
- `url` (string) - 政策页的路径

**示例:**
```html
<footer>
  {{#for policy in shop.policy}}
    <a href="{{policy.url}}">{{policy.title}}</a>
  {{/for}}
</footer>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/policy)

### powered_by_link

根据商店的地区设置，创建一个HTML链接元素，链接到shopline.com的本地化版本。

**示例:**
```html
<footer>
  {{{powered_by_link}}}
</footer>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/powered-by-link)

---

## 工具和助手

### content_for_additional_checkout_buttons

返回任何启用的具有离站结账功能的支付提供商的结账按钮。

**描述:** 使用 `additional_checkout_buttons` 来检查是否存在这些支付提供商，通过使用 `content_for_additional_checkout_buttons` 来显示这些支付提供商关联的结账按钮。

**示例:**
```html
{{#if additional_checkout_buttons}}
    {{{content_for_additional_checkout_buttons}}}
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/content-for-additional-checkout-buttons)

### settings

您可以根据 `theme.config.json` 文件访问主题的全局设置。

**示例:**
```html
{{#if settings.cart_add_type == "drawer"}}
打开抽屉式购物车。
{{#else}}
跳转到购物车页面。
{{/if}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/settings)

### color

颜色对象，可以用于为网站的不同组件设置不同的颜色样式。

**主要属性:**
- `alpha` (number) - 颜色的alpha组件，取值范围为0.0到1.0之间的十进制数
- `blue` (number) - 颜色的蓝色分量，取值范围为0到255之间的数值
- `green` (number) - 颜色的绿色分量，取值范围为0到255之间的数值
- `hue` (number) - 颜色的色相组件
- `red` (number) - 颜色的红色分量，取值范围为0到255之间的数值
- `rgb` (string) - RGB格式的颜色值
- `rgba` (string) - RGBA格式的颜色值
- `saturation` (number) - 颜色的饱和度组件

**示例:**
```css
.header {
  background-color: {{settings.header_color.rgb}};
  border-color: {{settings.accent_color.rgba}};
}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/color)

### font

字体选择器设置中的字体。

**主要属性:**
- `fallback_families` (string) - 字体的备用系列
- `family` (string) - 字体的名称
- `style` (string) - 字体的样式
- `system` (boolean) - 如果字体是系统字体，则返回true
- `weight` (string) - 字体的粗细

**示例:**
```css
--sort-title-font-weight: {{settings.sort_title_font.weight}};
--sort-title-font-style: {{settings.sort_title_font.style}};
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/font)

### location

到店取货地点信息。

**主要属性:**
- `id` (string) - 地点的ID
- `name` (string) - 地点的名称
- `address` (address) - 详细地址信息

**示例:**
```html
<div class="pickup-location">
  <h3>{{location.name}}</h3>
  <address>{{location.address.summary}}</address>
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/location)

### part

导航中的分页部分，可以用于构造导航元素。

**主要属性:**
- `is_link` (boolean) - 如果该部件是链接，则返回true
- `title` (string) - 与该部分关联的页码
- `url` (string) - 该部分的URL

**示例:**
```html
{{#var paginate = all_products | get_product_pagination(10) /}}
{{#for part in paginate.parts}}
  {{#if part.is_link }}
    {{#link_to part.url}}
      {{part.title}}
    {{/link_to}}
  {{#else}}
    <span>{{part.title}}</span>
  {{/if}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/part)

### linklists

商店中的所有导航菜单。

**描述:** 你可以通过使用菜单的handle仌linklists对象中访问特定的菜单。

**示例:**
```html
{{#for link in linklists.main-menu.links}}
  {{#link_to link.url}}
    {{link.title}}
  {{/link_to}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/linklists)

### linklist

菜单导航的链接。

**主要属性:**
- `handle` (string) - 菜单的handle
- `id` (string) - 菜单ID
- `levels` (number) - 菜单层级数
- `links` (array) - 菜单链接
- `title` (string) - 菜单标题

**示例:**
```html
<nav>
  <h2>{{linklist.title}}</h2>
  {{#for link in linklist.links}}
    {{#link_to link.url}}
      {{link.title}}
    {{/link_to}}
  {{/for}}
</nav>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/object/linklist)

---

## 总结

本文档已完整收录了Sline模板引擎中所有可用的对象，实现了100%覆盖：

- **objects.json中的对象**: 64个
- **object.md中的对象**: 70个（包含6个额外对象）
- **覆盖率**: 100%（所有objects.json中的对象都已包含）

### 额外包含的对象

以下6个对象虽然不在objects.json中，但是Sline模板引擎的重要组成部分：
- `form` - 表单对象
- `localization` - 本地化信息
- `media` - 媒体对象
- `menu` - 导航菜单信息
- `metafield` - 元字段信息
- `page` - 页面信息（重复条目）

### 文档特色

每个对象都包含：
- 中文描述
- 主要属性说明
- 实际使用示例
- 官方文档链接

### 功能分类

所有对象已按照功能进行合理分类，包含18个主要分类：
1. 基础对象
2. 商店和页面
3. 商品相关
4. 客户和账户
5. 订单和支付
6. 购物车
7. 博客和文章
8. 表单和输入
9. 地址和位置
10. 媒体和资源
11. 本地化和语言
12. 模板和结构
13. 搜索和过滤
14. 分页和导航
15. 折扣和促销
16. B2B功能
17. 工具和助手
18. 集合和列表

希望这份文档能帮助开发者更好地使用Sline模板引擎的对象功能。

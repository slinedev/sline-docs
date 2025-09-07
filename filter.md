# Sline Filter API 参考文档

本文档提供了Sline模板引擎中所有可用过滤器(Filter)的详细说明。

## 目录

- [支付相关](#支付相关)
- [字符串操作](#字符串操作)
- [数字操作](#数字操作)
- [数组操作](#数组操作)
- [日期时间](#日期时间)
- [URL和资源](#url和资源)
- [图片和媒体](#图片和媒体)
- [多语言和本地化](#多语言和本地化)
- [数据获取](#数据获取)
- [分页](#分页)
- [元字段](#元字段)
- [样式和CSS](#样式和css)
- [字体](#字体)
- [其他工具](#其他工具)

---

## 支付相关

### payment_type_img_url

返回给定支付类型的SVG图片的URL。

**语法:**
```html
{{ "affrim" | payment_type_img_url() }}
```

**参数:**
- `type` (string, 必填) - 付款类型

**返回值:** string

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/payment-type-img-url)

---

## 字符串操作

### append

将一个字符串追加到另一个字符串的末尾，返回合并后的新字符串。

**语法:**
```html
str | append(suffix)
```

**参数:**
- `str` (string) - 原始字符串
- `suffix` (string) - 要追加到原始字符串末尾的字符串

**返回值:** string

**示例:**
```html
{{ "Fake Two-" | append("piece Cardigan") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/append)

### prepend

在字符串开头插入指定内容。

**语法:**
```html
string | prepend(prefix)
```

**参数:**
- `string` (string) - 原始字符串
- `prefix` (string) - 要插入到开头的字符串

**返回值:** string

**示例:**
```html
{{ "world" | prepend("hello ") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/prepend)

### starts_with

判断字符串是否包含了指定的前缀子串。

**语法:**
```html
str | starts_with(prefix)
```

**参数:**
- `str` (string) - 原始字符串
- `prefix` (string) - 指定的前缀子串

**返回值:** boolean

**示例:**
```html
{{ "Fake Two-piece Cardigan" | starts_with("Fake") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/starts-with)

### ends_with

判断字符串是否包含了指定的后缀子串。

**语法:**
```html
str | ends_with(suffix)
```

**参数:**
- `str` (string) - 原始字符串
- `suffix` (string) - 指定的后缀子串

**返回值:** boolean

**示例:**
```html
{{ "Fake Two-piece Cardigan" | ends_with("Cardigan") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/ends-with)

### upcase

将字符串中的所有字符转换为大写。

**语法:**
```html
str | upcase()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
{{ "Vest and Ribbon Tie Dress" | upcase() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/upcase)

### downcase

将字符串中的所有字符转换为小写。

**语法:**
```html
string | downcase()
```

**参数:**
- `string` (string) - 被转换为小写的值

**返回值:** string

**示例:**
```html
{{ product.title | downcase() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/downcase)

### capitalize

将字符串中的第一个单词首字母大写。

**语法:**
```html
string | capitalize()
```

**参数:**
- `string` (string) - 被转换的值

**返回值:** string

**示例:**
```html
{{ product.brand | capitalize() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/capitalize)

### camelize

将字符串转换为驼峰式命名。

**语法:**
```html
string | camelize()
```

**参数:**
- `string` (string) - 被转换的值

**返回值:** string

**示例:**
```html
{{ "camelize_value" | camelize() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/camelize)

### handleize

将字符串转换为合法的handle。

**语法:**
```html
string | handleize()
```

**参数:**
- `string` (string) - 需要转换为handle的变量

**返回值:** string

**转换规则:**
- 将字符串中的所有字母字符转换为小写
- 将所有匹配的非单词字符替换为空格
- 去除字符串首尾的空白字符
- 将字符串内部的连续空白字符（空格、制表符等）替换为单个连字符 `-`

**示例:**
```html
{{ "100% M & Ms" | handleize() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/handleize)

### truncate_words

根据指定的单词数量截断字符串内容，如果指定的单词数量小于字符串中的单词数量，则会截断的字符串后附加上省略号后缀(...)。

**语法:**
```html
str | truncate_words(limit, suffix=suffix)
```

**参数:**
- `str` (string) - 原始字符串
- `limit` (number) - 保留单词的数量

**可选参数:**
- `suffix` (string) - 保留字符串的自定义后缀

**返回值:** string

**描述:** 也可以通过提供 `suffix` 参数来指定自定义后缀。如果不想要附加后缀，则可以提供一个空字符串。

**示例:**
```html
{{ "SHOPLINE will help more merchants sell their products." | truncate_words(5)}}
{{ "SHOPLINE will help more merchants sell their products." | truncate_words(5, suffix="~") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/truncate-words)

### trim_right

去除字符串右侧的空白字符（包括空格、换行符和制表符），返回处理后的文本。

**语法:**
```html
str | trim_right()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
before: <div>{{ "\tFestive Cheer Gift Box\n" }}</div>
after: <div>{{ "\t Festive Cheer Gift Box \n" | trim_right() }}</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/trim-right)

### trim_left

去除字符串左侧的空白字符（包括空格、换行符和制表符），返回处理后的文本。

**语法:**
```html
str | trim_left()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
before: <div>{{ "\tFestive Cheer Gift Box\n" }}</div>
after: <div>{{ "\t Festive Cheer Gift Box \n" | trim_left() }}</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/trim-left)

### trim

去除字符串两端的空白字符（包括空格、换行符和制表符），返回处理后的文本。

**语法:**
```html
str | trim()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
before: <div>{{ "\tFestive Cheer Gift Box\n" }}</div>
after: <div>{{ "\t Festive Cheer Gift Box \n" | trim() }}</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/trim)

### truncate

根据指定的单词数量截断字符串内容，并在截断后追加可选的后缀（默认是 "..."）。

**语法:**
```html
str | truncate(limit, suffix=suffix)
```

**参数:**
- `str` (string) - 原始字符串
- `limit` (number) - 需要保留字符串的长度

**可选参数:**
- `suffix` (string) - 保留字符串的自定义后缀

**返回值:** string

**示例:**
```html
{{ "Vest and Ribbon Tie Dress" | truncate(10) }}
{{ "Vest and Ribbon Tie Dress" | truncate(10, suffix="~") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/truncate)

### strip_newlines

去除字符串中所有的换行符，返回一个不含换行的字符串。

**语法:**
```html
str | strip_newlines()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
{{ "First Line;\nSecond Line;\nThird Line;" | strip_newlines() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/strip-newlines)

### strip_html

去除字符串中所有的HTML标签，返回一个纯文本字符串。

**语法:**
```html
str | strip_html()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
{{ "<h1>title</h1>\n<div>description</div>" | strip_html() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/strip-html)

### split

使用指定的分隔符对字符串进行分割，返回一个字符串数组。

**语法:**
```html
str | split(separator)
```

**参数:**
- `str` (string) - 原始字符串
- `separator` (string) - 分割符

**返回值:** array

**示例:**
```html
{{#var words = "Festive Cheer Gift Box" | split(" ") /}}
{{#for word in words}}
    word: {{ word }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/split)

### slice

从指定索引位置开始截取子字符串或子数组。

**语法:**
```html
list | slice(start, len=len)
```

**参数:**
- `list` (string|array) - 原始字符串或数组
- `start` (number) - 截取起始索引位置

**可选参数:**
- `len` (number) - 截取长度

**返回值:** string|array

**描述:** 默认情况下，只会截取一个字符或数组项。不过，也可以通过提供 `len` 参数来指定截取子字符串或子数组的长度。

**示例:**
```html
{{ product.title }}
{{ product.title | slice(1, len=9) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/slice)

### replace

替换字符串中的所有匹配子串。

**语法:**
```html
string | replace(old, new)
```

**参数:**
- `string` (string) - 原始字符串
- `old` (string) - 需要被替换的子串
- `new` (string) - 替换后的新子串

**返回值:** string

**示例:**
```html
{{ "a,b,c" | replace(",", "-") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/replace)

### replace_first

替换字符串中第一个匹配的子串。

**语法:**
```html
string | replace_first(old, new)
```

**参数:**
- `string` (string) - 原始字符串
- `old` (string) - 需要被替换的子串
- `new` (string) - 替换后的新子串

**返回值:** string

**示例:**
```html
{{ "a,b,c" | replace_first(",", "-") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/replace-first)

### remove

移除字符串中所有匹配的子串。

**语法:**
```html
string | remove(substr)
```

**参数:**
- `string` (string) - 原始字符串
- `substr` (string) - 需要移除的子串

**返回值:** string

**示例:**
```html
{{ "a-b-c" | remove("-") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/remove)

### remove_first

移除字符串中第一次出现的指定子串。

**语法:**
```html
string | remove_first(substr)
```

**参数:**
- `string` (string) - 原始字符串
- `substr` (string) - 要移除的子串

**返回值:** string

**示例:**
```html
{{ "hello hello world" | remove_first("hello ") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/remove-first)

### contains

判断字符串包含子串或数组包含子元素。

**语法:**
```html
variable | contains(value)
```

**参数:**
- `variable` (string|array) - 检查的变量
- `value` (string|boolean|number) - 检查的值

**返回值:** boolean

**示例:**
```html
{{#var str = "hello word!" /}}
{{ str | contains("hello") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/contains)

### escape

将HTML中的特殊字符（例如 `&`、`<>` 等）转换为相应的转义序列。字符串中没有对应转义序列的字符将保持不变。

**语法:**
```html
string | escape()
```

**参数:**
- `string` (string) - 需要被替换的字符串

**返回值:** string

**示例:**
```html
{{{ product.description | escape() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/escape)

### newline_to_br

将字符串中的换行符（\n）替换为HTML换行标签（\<br>）。

**语法:**
```html
string | newline_to_br()
```

**参数:**
- `string` (string) - 需要替换换行符的变量

**返回值:** string

**注意:** 返回的html标签，需要使用 `{{{ }}}` 渲染，避免br标签被转义。

**示例:**
```html
{{{ product.description | newline_to_br() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/newline-to-br)

---

## 数字操作

### money

根据商店的不包含货币code格式的设置，形成一个给定的价格。

**语法:**
```html
{{ "pour price" | money()}}
```

**参数:**
- `price` (number, 必填) - 金额
- `code` (string, 可选) - 币种，非必填，默认值为市场币种

**返回值:** string

**示例:**
```html
{{ 10000 | money()}}
{{ 10000 | money(code="USD")}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/money)

### money_with_currency

根据商店的包含货币code格式的设置，形成一个给定的价格。返回格式化后的金额。

**语法:**
```html
{{"your price" | money_with_currency()}}
```

**参数:**
- `price` (number) - 金额，必填
- `code` (string) - 币种，非必填，默认值为市场币种

**返回值:** string

**示例:**
```html
{{10000 | money_with_currency()}}
{{10000 | money_with_currency(code="USD")}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/money-with-currency)

### money_without_currency

根据商店的不包含货币code格式的设置，形成一个给定的价格，没有货币符号。返回格式化后的金额。

**语法:**
```html
{{"your price" | money_without_currency()}}
```

**参数:**
- `price` (number) - 金额, 必填
- `code` (string) - 币种，非必填，默认值为市场币种

**返回值:** string

**示例:**
```html
{{10000 | money_without_currency()}}
{{10000 | money_without_currency(code="USD")}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/money-without-currency)

### plus

数字加法运算。

**语法:**
```html
number | plus(addend)
```

**参数:**
- `number` (number) - 被加数
- `addend` (number) - 加数

**返回值:** number

**示例:**
```html
{{ 1 | plus(1) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/plus)

### minus

数字减法运算。

**语法:**
```html
number | minus(subtrahend)
```

**参数:**
- `number` (number) - 被减数
- `subtrahend` (number) - 减数

**返回值:** number

**示例:**
```html
{{ 5 | minus(3) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/minus)

### times

数字乘法运算。

**语法:**
```html
number | times(multiplier)
```

**参数:**
- `number` (number) - 被乘数
- `multiplier` (number) - 乘数

**返回值:** number

**示例:**
```html
{{ 2 | times(5) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/times)

### divided_by

数字除法运算。

**语法:**
```html
number | divided_by(divisor, integer=integer)
```

**参数:**
- `number` (number) - 被除数
- `divisor` (number) - 除数（不可为零）

**可选参数:**
- `integer` (boolean) - 强制返回整数结果

**返回值:** number

**描述:** 当两数均为整数时，默认返回向下取整的整数；若任一数为浮点数，则返回浮点数结果。可通过 `integer` 参数强制指定返回类型。

**示例:**
```html
{{ 10 | divided_by(4) }}
{{ 10 | divided_by(4, integer=false) }}
{{ 10 | divided_by(3.1) }}
{{ 10 | divided_by(3.1, integer=true) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/divided-by)

### modulo

计算两数相除的余数。

**语法:**
```html
number | modulo(divisor)
```

**参数:**
- `number` (number) - 被除数
- `divisor` (number) - 除数（非零数字）

**返回值:** number

**示例:**
```html
{{ 10 | modulo(3) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/modulo)

### abs

计算数字的绝对值。

**语法:**
```html
number | abs()
```

**参数:**
- `number` (number) - 要计算绝对值的数字

**返回值:** number

**示例:**
```html
{{ -1 | abs() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/abs)

### ceil

将数字向上取整到最接近的整数。

**语法:**
```html
number | ceil()
```

**参数:**
- `number` (number) - 要处理的数字

**返回值:** number

**示例:**
```html
{{ 4.3 | ceil() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/ceil)

### floor

将数字向下取整到最接近的整数。

**语法:**
```html
number | floor()
```

**参数:**
- `number` (number) - 要处理的数字

**返回值:** number

**示例:**
```html
{{ 4.3 | floor() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/floor)

### round

将数字四舍五入到指定小数位。

**语法:**
```html
number | round(fixed=fixed)
```

**参数:**
- `number` (number) - 要处理的数字

**可选参数:**
- `fixed` (number) - 保留的小数位数，默认为0

**返回值:** number

**示例:**
```html
{{ 1.35 | round() }}
{{ 1.35 | round(fixed=1) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/round)

### at_least

确保数字不小于指定的最小值。

**语法:**
```html
number | at_least(min)
```

**参数:**
- `number` (number) - 要限制的数字
- `min` (number) - 允许的最小值

**返回值:** number

**描述:** 若输入数字大于等于最小值，返回原数字；否则返回最小值。

**示例:**
```html
{{ 3 | at_least(4) }}
{{ 5 | at_least(4) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/at-least)

### at_most

限制数字不超过指定的最大值。

**语法:**
```html
number | at_most(max)
```

**参数:**
- `number` (number) - 要限制的数字
- `max` (number) - 允许的最大值

**返回值:** number

**描述:** 若输入数字小于等于最大值，返回原数字；否则返回最大值。

**示例:**
```html
{{ 3 | at_most(4) }}
{{ 5 | at_most(4) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/at-most)

---

## 数组操作

### first

返回数组中的第一个元素。

**语法:**
```html
array | first()
```

**参数:**
- `array` (array) - 目标数组

**返回值:** any

**示例:**
```html
{{#var arr = "one,two,three" | split(",") /}}
{{ arr | first() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/first)

### last

返回一个数组中的最后一个项目。

**语法:**
```html
array | last()
```

**参数:**
- `array` (array) - 目标数组

**返回值:** any

**示例:**
```html
{{#var arr = "one,two,three" | split(",") /}}
{{ arr | last() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/last)

### size

返回字符串或数组的大小。

**语法:**
```html
variable | size()
```

**参数:**
- `variable` (array|string) - 获取长度的变量

**返回值:** number

**描述:** 字符串的大小是字符串包含的字符数。数组的大小是数组中的项数。

**示例:**
```html
{{#var arr = "one,two,three" | split(",") /}}
{{ arr | size() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/size)

### concat

合并两个数组，返回一个新数组。

**语法:**
```html
array1 | concat(array2)
```

**参数:**
- `array1` (array) - 合并的目标数组
- `array2` (array) - 被合并的数组

**返回值:** array

**示例:**
```html
{{#var arr1 = "one,two,three" | split(",") /}}
{{#var arr2 = "four,five" | split(",") /}}
{{ arr1 | concat(arr2) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/concat)

### join

将一个数组中的所有元素使用指定分隔符合并成一个字符串。

**语法:**
```html
array | join(separator)
```

**参数:**
- `array` (array) - 被转换的数组
- `separator` (string) - 每个元素之间连接的字符串

**返回值:** string

**示例:**
```html
{{#var arr = "one,two,three" | split(",") /}}
{{ arr | join("__") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/join)

### map

根据数组中项目的特定属性创建值数组。

**语法:**
```html
array | map(key)
```

**参数:**
- `array` (array) - 被提取的数组
- `key` (string) - 数组中对象的属性

**返回值:** array

**示例:**
```html
{{ product.images | map("src") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/map)

### where

基于对象属性值对数组进行筛选，返回符合条件的新数组。支持精确匹配或真值检测两种模式。

**语法:**
```html
array | where(key, equals=value)
```

**参数:**
- `array` (array) - 原数组，数组元素应为对象
- `key` (string) - 需要检测的对象属性键名

**可选参数:**
- `equals` (any) - 启用精确匹配模式时作为比对基准的值，未提供时自动切换至真值检测模式

**返回值:** array

**示例:**
1. 精确匹配模式:
```html
{{#var filterProducts = paginate.list|where("vendor", equals="Brand 3") /}}
```
2. 真值检测模式:
```html
{{#var filterProducts = paginate.list|where("vendor") /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/where)

### sort

对数组进行排序。

**语法:**
```html
array | sort(by=key)
```

**参数:**
- `array` (array) - 原数组

**可选参数:**
- `by` (string) - 对象数组排序时使用的属性键名

**返回值:** array

**示例:**
1. 字符串数组排序:
```html
{{#var arr = "c,a,b" | split(",") /}}
{{ arr | sort() | json() }}
```
2. 对象数组排序:
```html
{{#var sortedProducts = paginate.list | sort(by="price") /}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/sort)

### reverse

反转数组中元素的顺序，返回新数组。

**语法:**
```html
array | reverse()
```

**参数:**
- `array` (array) - 原数组

**返回值:** array

**示例:**
```html
{{#var arr = "a,b,c" | split(",") /}}
{{ arr | reverse() | json() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/reverse)

### uniq

去除数组中的重复元素，返回唯一值组成的新数组。

**语法:**
```html
array | uniq()
```

**参数:**
- `array` (array) - 原数组

**返回值:** array

**示例:**
```html
{{#var arr = "a,b,a,c" | split(",") /}}
{{ arr | uniq() | json() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/uniq)

---

## 日期时间

### date

将日期字符串格式化为指定格式。

**语法:**
```html
date_string | date(format=format)
```

**参数:**
- `date_string` (string) - ISO8601格式的日期字符串

**可选参数:**
- `format` (string) - 输出格式（支持内置类型或自定义占位符）

**内置日期格式化类型:**
- default
- abbreviated_date
- basic
- date
- date_at_time
- on_date

**返回值:** string

**描述:** 可使用占位符自定义日期输出的格式，可参考：https://www.strfti.me/

**示例:**
```html
{{ "2022-04-14 16:56:02 -0400" | date() }}
{{ "2022-04-14 16:56:02 -0400" | date(format="basic") }}
{{ "2022-04-14 16:56:02 -0400" | date(format="%B %d, %Y")  }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/date)

---

## URL和资源

### asset_url

返回主题静态资源的文件CDN地址，支持绝对路径和相对路径。

**语法:**
```html
filepath | asset_url()
```

**参数:**
- `filepath` (string) - 文件路径

**返回值:** string

**示例:**
- 绝对路径：需要引用的资源路径 `/public/a.js`
  ```html
  {{ "a.js" | asset_url() }}
  ```
- 相对路径：表达式所在的文件路径为 `sections/test/two/two.html`，需要引用的资源路径 `sections/test/one/test.js`
  ```html
  {{ "../one/test.js"| asset_url() }}
  ```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/asset-url)

### file_img_url

从Shopline后台的文件页面返回图像的CDN URL。

**语法:**
```html
filename | file_img_url(size=size)
```

**参数:**
- `filename` (string) - 文件名

**可选参数:**
- `size` (string) - 尺寸, 格式为: 100x、210x

**返回值:** string

**示例:**
```html
{{{ "1691570437909.jpg" | file_img_url() }}}
{{{ "1691570437909.jpg" | file_img_url(size="100x") }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/file-img-url)

### file_url

从Shopline后台的文件库返回文件的CDN URL。

**语法:**
```html
filename | file_url()
```

**参数:**
- `filename` (string) - 文件名

**返回值:** string

**示例:**
```html
{{{ "1691570437909.jpg" | file_url() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/file-url)

### url_for_type

生成一个商品集合页面的网址，该页面展示指定产品类型的所有商品。

**语法:**
```html
{{ "type" | url_for_type() }}
```

**参数:**
- `type` (string) - 产品类型

**返回值:** string

**示例:**
```html
{{ "type" | url_for_type() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/url-for-type)

### url_for_vendor

生成一个商品集合页面的网址，该页面展示指定产品品牌的所有商品。

**语法:**
```html
{{ "vendor" | url_for_vendor() }}
```

**参数:**
- `vendor` (string) - 产品品牌

**返回值:** string

**示例:**
```html
{{ "vendor" | url_for_vendor() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/url-for-vendor)

### url_param_escape

对字符串中URL参数不安全的字符进行转义处理。

**语法:**
```html
str | url_param_escape()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
{{{ "<p>Love & Peace</p>" | url_param_escape() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/url-param-escape)

### url_decode

将字符串中的%字符转换为URL字符。

**语法:**
```html
str | url_decode()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
{{ "vicky%40qq.com" | url_decode() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/url-decode)

### url_encode

将字符串中的任何URL不安全的字符转换为带有%编码的字符。

**语法:**
```html
str | url_encode()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**注意:** 字符串中的空格会被转成 `+` 号，而不是带%编码的字符。

**示例:**
```html
{{{ "vicky@qq.com" | url_encode() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/url-encode)

### url_escape

对字符串中URL不安全的字符进行转义处理。

**语法:**
```html
str | url_escape()
```

**参数:**
- `str` (string) - 原始字符串

**返回值:** string

**示例:**
```html
{{{ "<p>Love & Peace</p>" | url_escape() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/url-escape)

---

## 图片和媒体

### image_url

返回图片的远程CDN链接。

**语法:**
```html
variable | image_url(width=number, height=number, quality=number)
```

**参数:**
- `variable` (object) - 数据对象

**可选参数:**
- `width` (number) - 图片宽度
- `height` (number) - 图片高度
- `quality` (number) - 图片压缩比

**返回值:** string

**描述:** 你可以通过 `image_url` filter 获取以下数据对象的图片链接：image、article、line_item、variant、product、collection、video对象。

**示例:**
1. 设置图片宽度：
```html
{{ product | image_url(width=100) }}
```
2. 设置图片高度：
```html
{{ product | image_url(height=100) }}
```
3. 设置图片压缩比：
```html
{{ product | image_url(quality=90) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/image-url)

### external_video_url

返回指定外部视频的链接。

**语法:**
```html
media | external_video_url(attribute=any)
```

**参数:**
- `media` (object) - 媒体对象

**可选参数:**
- `autoplay` (boolean) - 是否自动播放。默认为 `false`
- `controls` (boolean) - 是否显示播放器控件。默认为 `true`
- `loop` (boolean) - 是否循环播放。默认为 `false`

**返回值:** string

**描述:** 你可以为视频链接添加指定参数。参数名称及相关可选值需与 [YouTuBe API](https://developers.google.com/youtube/player_parameters#Parameters) 相同。

**示例:**
```html
{{#for media in product.media}}
    {{#switch media.media_type}}
        {{#case "external_video" /}}
            {{#if media.host == "youtube"}}
                {{#external_video_tag media | external_video_url(autoplay=false, loop=true) /}}
            {{/if}}
    {{/switch}}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/external-video-url)

---

## 多语言和本地化

### t

从多语言文件中返回给定翻译键的已翻译文本字符串。

**语法:**
```html
key | t()
```

**参数:**
- `key` (string) - 多语言文件中的翻译键

**可选参数:**
- `...props` (any) - 用于替换多语言文本中的动态占位符

**返回值:** string

**示例:**
```html
{{ "products.general.sold_out" | t() }}
{{ "products.product_details.inventory_low_stock_show_count" | t(quantity=10) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/t)

---

## 数据获取

### get

通过某种类型资源的id或handle获取单个资源对象。

**语法:**
```html
obj | get(idOrHandle)
```

**参数:**
- `obj` (any) - 某种类型的全部资源对象，目前仅支持上述列举出来的Object类型
- `idOrHandle` (string) - 资源id或handle

**返回值:** any

**描述:** 适用于跟以下Object结合使用：all_products、all_collections、all_articles、all_blogs、all_pages

**示例:**
```html
{{#var myProduct = all_products | get("winter-wonderland-gift-box") /}}
{{ myProduct.title }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get)

### get_product

获取指定的单个商品对象。

**语法:**
```html
obj | get_product()
```

**参数:**
- `obj` (any) - 含有商品ID的Object对象，目前仅支持上述列举出来的Object类型

**返回值:** product

**描述:** 适用于跟line_item、gift_card结合使用

**示例:**
```html
{{#var myProduct = gift_card | get_product() /}}
{{ myProduct.title }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-product)

### get_collections

获取某个商品所关联的所有分类对象。

**语法:**
```html
product | get_collections()
```

**参数:**
- `product` (any) - 指定商品Object

**返回值:** array

**描述:** 适用于跟product结合使用

**示例:**
```html
{{#var myCollections = product | get_collections() /}}
{{#for collection in myCollections}}
  {{ collection.title }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-collections)

### get_variants

获取某个商品下的所有变体对象。

**语法:**
```html
product | get_variants()
```

**参数:**
- `product` (any) - 指定商品Object

**返回值:** array

**描述:** 适用于跟product结合使用

**示例:**
```html
{{#var myVariants = product | get_variants() /}}
{{#for variant in myVariants}}
  {{ variant.title }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-variants)

---

## 分页

### get_pagination

通过分页获取指定类型的资源对象。

**语法:**
```html
obj | get_pagination(pageSize)
```

**参数:**
- `obj` (any) - 指定类型的全部资源对象
- `pageSize` (number) - 每页数量

**返回值:** paginate

**描述:** 适用于跟all_collections、all_pages结合使用

**示例:**
```html
{{#var paginate = all_collections | get_pagination(10) /}}
{{#for collection in paginate.list}}
    {{forloop.index}}: {{ collection.title }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-pagination)

### get_product_pagination

通过分页获取商品对象。

**语法:**
```html
collection | get_product_pagination(pageSize)
```

**参数:**
- `collection` (collection) - 商品分类Object对象
- `pageSize` (number) - 每页数量

**返回值:** paginate

**描述:** 适用于跟collection结合使用

**示例:**
```html
{{#var paginate = collection | get_product_pagination(10) /}}
{{#for item in paginate.list}}
  {{forloop.index}}: {{ item.title }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-product-pagination)

### get_comment_pagination

通过分页获取评论对象。

**语法:**
```html
article | get_comment_pagination(pageSize)
```

**参数:**
- `article` (any) - 博客文章Object对象
- `pageSize` (number) - 每页数量

**返回值:** paginate

**描述:** 适用于跟article结合使用

**示例:**
```html
{{#var paginate = article | get_comment_pagination(10) /}}
{{#for item in paginate.list}}
    {{forloop.index}}: {{ item.content }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-comment-pagination)

### get_article_pagination

通过分页获取文章对象。

**语法:**
```html
blog | get_article_pagination(pageSize)
```

**参数:**
- `blog` (any) - 博客Object对象
- `pageSize` (number) - 每页数量

**返回值:** paginate

**描述:** 适用于跟blog结合使用

**示例:**
```html
{{#var paginate = blog | get_article_pagination(10) /}}
{{#for item in paginate.list}}
    {{forloop.index}}: {{ item.title }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-article-pagination)

### get_order_pagination

通过分页获取订单对象。

**语法:**
```html
customer | get_order_pagination(pageSize)
```

**参数:**
- `customer` (any) - 客户Object对象
- `pageSize` (number) - 每页数量

**返回值:** paginate

**描述:** 适用于跟customer结合使用

**示例:**
```html
{{#var paginate = customer | get_order_pagination(10) /}}
{{#for item in paginate.list}}
  {{forloop.index}}: {{ item.id }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-order-pagination)

### get_search_pagination

通过分页获取搜索出来的结果对象。

**语法:**
```html
search | get_search_pagination(pageSize)
```

**参数:**
- `search` (any) - 搜索结果对象
- `pageSize` (number) - 每页数量

**返回值:** paginate

**描述:** 适用于跟search结合使用

**示例:**
```html
{{#var paginate = search | get_search_pagination(10) /}}
{{#for item in paginate.list}}
  {{forloop.index}}: {{ item.title }}
{{/for}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-search-pagination)

---

## 元字段

### get_metafields

获取某个资源对应的元字段对象。

**语法:**
```html
obj | get_metafields(namespace)
```

**参数:**
- `obj` (any) - 指定的资源对象
- `namespace` (string) - 元字段的命名空间

**返回值:** metafields

**描述:** 适用于跟product、collection、blog、article、page、order、customer、variant、shop、company结合使用

**示例:**
```html
{{#var mf = product | get_metafields("seo") /}}
{{ mf.seo_key.value }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/get-metafields)

### metafield_text

生成元字段文本数据。

**语法:**
```html
metafield | metafield_text()
```

**参数:**
- `metafield` (object) - metafield数据

**返回值:** string

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
{{ metafield_ns.my_key | metafield_text() }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/metafield-text)

---

## 样式和CSS

### class_list

与style相关控件配合使用，输出对应的类名列表。

**语法:**
```html
setting | class_list()
```

**参数:**
- `setting` (any) - style相关控件的值

**返回值:** string

**描述:** 支持传入单个style控件配置或整个settings对象：
- 单个style配置：返回当前style控件对应的样式列表
- settings对象：返回settings中所有style控件的样式列表

**示例:**
```html
<div class="product-detail__info {{block.settings.layout | class_list()}}">
  ...
</div>

<div class="product-card {{block.settings | class_list()}}">
  ...
</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/class-list)

### css_var

与style picker配合使用，输出配置对应的css变量名。

**语法:**
```html
style_setting | css_var(key_name)
```

**参数:**
- `style_setting` (any) - style picker动态配置值
- `key_name` (string) - 对应css配置的属性名

**返回值:** string

**示例:**
```html
<div style="--info-row-gap: {{section.settings.layout | css_var(`row-gap`)}};">content</div>
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/css-var)

---

## 字体

### font_url

返回传入字体对象指定格式（`woff2`或`woff`）的CDN地址。

**语法:**
```html
font | font_url(format=format)
```

**参数:**
- `font` (font) - font对象

**可选参数:**
- `format` (string) - 字体文件格式（`woff2`或`woff`），默认`woff2`

**返回值:** string

**示例:**
```html
{{ settings.sort_title_font | font_url() }}
{{ settings.sort_title_font | font_url(format="woff") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/font-url)

### font_modify

修改字体对象的指定属性，并返回新的字体对象。

**语法:**
```html
font | font_modify(key, value)
```

**参数:**
- `font` (font) - font对象
- `key` (string) - 要修改的属性
- `value` (string) - 新的属性值

**返回值:** string

**支持的属性和值:**

| 属性 | 有效值 | 说明 |
|---------|-----------|----------|
| `style` | `"normal"` | 将字体转换为常规（非斜体）变体 |
|  | `"italic"` | 将字体转换为斜体变体（如果可用） |
|  | `"oblique"` | 将字体转换为倾斜体变体 |
| `weight` | `100`–`900`（以100为间隔） | 调整字重至指定值（如`400`为常规，`700`为加粗） |
|  | `"normal"` | `weight: 400`的简写 |
|  | `"bold"` | `weight: 700`的简写 |
|  | `"+/-N"`（如`"+200"`） | 在当前字重上增加/减少`N`（如`400`→`600`） |
|  | `"lighter"` | 根据CSS规则降低字重（如`700`→`400`） |
|  | `"bolder"` | 根据CSS规则提高字重（如`400`→`700`） |

**示例:**
```html
Original weight: {{ settings.sort_title_font.weight }}
{{#var lighterFont = settings.sort_title_font | font_modify("weight", "lighter") /}}
h2 {
  font-weight: {{ lighterFont.weight }};
}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/font-modify)

### font_face

为传入的字体对象生成CSS `@font-face`声明。

**语法:**
```html
font | font_face()
```

**参数:**
- `font` (font) - font对象

**返回值:** string

**示例:**
```html
{{{ settings.sort_title_font | font_face() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/font-face)

---

## 其他工具

### json

将值转换为符合JSON格式的字符串。

**语法:**
```html
value | json()
```

**参数:**
- `value` (any) - 需要序列化的值

**返回值:** string

**注意:** `{{ ... }}`会对输出结果进行html转义，如需原样输出可使用`{{{ ... }}}`。

**示例:**
```html
{{{ product.tags | json() }}}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/json)

### default

为`nil`、`false`或`空字符串`提供默认值。

**语法:**
```html
value | default(default, allow_empty_str=bool, allow_false=bool)
```

**参数:**
- `default` (any) - 默认值（当value为空时返回）
- `value` (any) - 要检查的值

**可选参数:**
- `allow_empty_str` (boolean) - 是否视空字符串`""`为有效值（默认为`false`）
- `allow_false` (boolean) - 是否视`false`为有效值（默认为`false`）

**返回值:** any

**示例:**
```html
1. {{ "" | default("Tom") }}
2. {{ "" | default("Tom", allow_empty_str=true) }}
3. {{ false | default(true) }}
4. {{ false | default(true, allow_false=true) }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/default)

### pluralize

根据给定的数字，输出字符串的单数形式或复数形式。

**语法:**
```html
number | pluralize(singular, plural)
```

**参数:**
- `number` (number) - 决定使用单数还是复数的数字
- `singular` (string) - 单数形式的字符串
- `plural` (string) - 复数形式的字符串

**返回值:** string

**示例:**
```html
{{ 1 | pluralize("singular", "plural") }}
{{ 2 | pluralize("singular", "plural") }}
```

**链接:** [详细文档](https://developer.shopline.com/docs/sline/filter/pluralize)

---

## 总结

本文档已完整收录了Sline模板引擎中所有可用的过滤器，按功能分类整理并提供了详细的使用说明和示例。每个过滤器都包含：

- 中文描述
- 标准语法格式  
- 详细参数说明
- 返回值类型
- 实际使用示例
- 官方文档链接

希望这份文档能帮助开发者更好地使用Sline模板引擎的过滤器功能。

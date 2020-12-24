# 12/18(五)購物車-model欄位說明
###### tags: `龍哥`

#### Order
* username
* tel
* address
* user:belongs_to

#### OrderItem
* product:belongs_to
* quantity:integer
* order:belongs_to
* sell_price

#### Coupon
* 序號
* 有效日期
* 折扣


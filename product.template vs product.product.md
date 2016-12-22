之前直接忽视了`product.template`和`product.product`的区别，认为`product.product`仅仅在`product.template`的基础上添加些字段而已。现在要把自己写的代码中关联的`product.template`改为`product.template`，实为痛苦。故记之。

下文先翻译下官方的文档：[Using product variants ](https://www.odoo.com/documentation/user/10.0//inventory/settings/products/variants.html)

文档中的`产品变型`即`product.product`

> 产品变型（`Product variants`）用来管理有不同变量的产品, 例如尺寸, 颜色等等。它可以让我们在产品模板层面对产品进行管理(所有的变量), 也可以在变型层面管理(特定的属性`attributes`)。
>
> 例如, 一个销售T恤的公司可能有以下产品 :
>
> - B&C T-shirt
>   - Sizes: S, M, L, XL, XXL
>   - Colors: Blue, Red, White, Black
>
> 在该示例中, `B&C T-shirt` 是产品模板`product template`, `B&C T-Shirt, S, Blue` 是一个产品变型, 尺寸和颜色是其属性`attributes` 。
>
> 以上示例总共有20个不同的产品(5中尺寸x4种颜色)。每一个产品都会有自己的库存、销售信息、 等等。
>
> ## 我们应该使用产品变型吗
>
> ### 变型的作用
>
> - 条形码`Barcode`：编码和条形码是和产品变型绑定在一起的，而不是和产品模板绑定在一起。每个产品变型都有自己的条形码和最小库存单位。
> - 价格`Price`：每个产品变型都有自己的标价，这个标价是根据产品模型计算出来的。比如，产品模型的标价为20美元，红色的产品变型需要加价3美元，这样产品变型的标价就是23美元。当然，我们也可以自己定义产品模板或者产品变型的价格规则。
> - 库存`Inventory`：产品的库存是通过产品变型来管理的。你不拥有`B&C T-shirt`，你仅仅拥有`B&C T-Shirt, S, Red`或者`B&C T-Shirt, M, Blue`。事实上，我们在产品模板的`form`视图上看到的库存是各个产品变型库存的总合。
> - 照片`Picture`：产品照片是和产品变型绑定在一起的，每隔产品变型都有自己的照片。
> - 其他字段：大部分其他字段都属于产品模板。如果我们更新了这些字段，比如收益账户`Income Account`或者税率`Taxes`，产品变型中的相关字段也自动更新。
>
> ### 什么时候使用产品变型
>
> - 电子商务`eCommerce`:
> - 生产`Manufacturing：`
> - 价格`Price`：
>
> ### 什么时候应该避免使用产品变形
>
> ## 配置
>
> 激活产品变型
>
> 创建带有型号的产品
>
> 管理组合的可能性
>
> 根据型号设置价格

## 开发中使用`product.product`还是`product.template`?

- 添加公有字段继承`product.template`添加

  这样同一个产品模板的产品变型中新增的字段值就一样了。如果需要值不一样，那就应该考虑增加新的产品变型。

- 关联产品时，应关联到`product.product`而不是`product.template`

  这样咱们自己写的代码才能对产品变型起作用
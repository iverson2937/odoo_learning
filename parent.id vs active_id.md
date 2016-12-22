在`form`视图中怎么表示当前记录呢？

>同级字段用`active_id`，
>
>`Many2many``One2many`嵌套`tree`视图中的字段用`parent.id`

```Xml
<page string="预设食材清单行">
  <div>
    <button string="⇒ 重置预设食材清单" class="oe_link oe_right" help="根据门店历史订单数据智能预测待购买食材" name="calculate_preset_product_line_ids" type="object"/>
    <field name="preset_product_line_ids">
      <tree editable="bottom">
        <field name="product_id" context="{'from_shop': True, 'shop_id': parent.id}" options="{'no_create_edit': True}"/>
        <field name="name"/>
        <field name="oder_type_id" domain="[('shop_id', '=', parent.id)]" context="{'default_shop_id': parent.id}"/>
      </tree>
    </field>
  </div>
</page>

<page string="订货类型">
  <field name="product_order_type_ids" domain="[('shop_id', '=', active_id)]" context="{'default_shop_id': active_id}">
    <tree editable="bottom">
      <field name="name"/>
      <field name="cycle" string="周期"/>
    </tree>
  </field>
</page>
```

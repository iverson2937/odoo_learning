从销售订单得到启发：
- 定义`ir.sequence`记录
- 重写`create`方法

```
<?xml version="1.0" encoding="utf-8"?>
<odoo>
    <data noupdate="1">

        <!-- Sequences for sale.order -->
        <record id="seq_sale_order" model="ir.sequence">
            <field name="name">Sales Order</field>
            <field name="code">sale.order</field>
            <field name="prefix">SO</field>
            <field name="padding">3</field>
            <field name="company_id" eval="False"/>
        </record>

    </data>
</odoo>

```


```
@api.model
def create(self, vals):
    if vals.get('name', 'New') == 'New':
        vals['name'] = self.env['ir.sequence'].next_by_code('sale.order') or 'New'

    result = super(SaleOrder, self).create(vals)
    return result
```

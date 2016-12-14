reference:

- http://odoo-development.readthedocs.io/en/latest/odoo/models/ir.cron.html

这篇文章介绍得很不错，谢谢该作者。现使用Odoo 10新api重新写/翻译下该文章。

----

## ir.cron

在Odoo 10中创建自动化动作

自动化动作，可以在一段时间后自行启动，从而帮助我们做好多事情，比如，自动化操作数据库而不需我们手动更改。自动化动作在Ooo中实现很简单，只要在表`ir.cron`中插入一个记录，Odoo就会按我们定义的去执行它。

#### 1.创建一个模块和模块方法以供练习
```
class ModelName(models.Model):
  _name = "model.name"

  # todo
  # fields definition

  def method_name(self)：
    # metod_body
```

#### 2.创建自动化动作

自动化动作的一个很重要的点就是`noupdate`需置为`1`，因为我们不行更新模块是自动化操作改变

```
<openerp>
  <data noupdate="1">
    <record id="cron_name" model="ir.cron">
    <field name="name">Name </field>
      <field name="active" eval="True" />
      <field name="user_id" ref="base.user_root" />
      <field name="interval_number">1</field>
      <field name="interval_type">days</field>
      <field name="numbercall">-1</field>
      <field name="doal">1</field>
      <field name="nextcall" >2016-12-31 23:59:59</field>
      <field name="model" eval="model.name" />
      <field name="function" eval="method_name" />
      <field name="args" eval="" />
      <field name="priority" eval="5" />
    </record>
  </data>
</openerp>
```

待续

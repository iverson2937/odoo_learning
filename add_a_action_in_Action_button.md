references

- https://www.odoo.com/forum/help-1/question/why-can-t-i-make-a-button-in-tree-7468

- https://stackoverflow.com/questions/40571580/how-to-create-server-actions-in-odoo-10

```
<!--  Action button -->
    <record id="server_action_id" model="ir.actions.server">
            <field name="name">server_action_name</field>
            <field name="type">ir.actions.server</field>
            <field name="model_id" ref="model_model_name"/>
            <field name="state">code</field>
            <field name="code">env['model_name'].browse(context.get('active_ids')).some_method()</field>
      </record>

      <record id="id_of_the_action_value" model="ir.values">
          <field name="name">action_name</field>
          <field name="action_id" ref="server_action_id"/>
          <field name="value" eval="'ir.actions.server,' + str(ref('server_action_id'))"/>
          <field name="key">action</field>
          <field name="model_id" ref="model_model_name"/>
          <field name="model">model_name</field>
          <field name="key2">client_action_multi</field>
      </record>
```

# Rules

Firefly III contains a powerful rule engine that can automatically update your transactions. It can do this when transactions are created or when they are changed. It works by combining "triggers" with "actions".

This is especially useful when you're importing data and you wish all transactions to be updated at once. Or perhaps, you are too lazy to set the correct budget and category all the time so you make a rule to do this for you.

Rule groups
-----------

Rules are divided over rule groups. Each rule group has rules in a specific order.

Rules can be set to be "strict" or not. If a rule is set to be strict, ALL triggers must match for the rule to fire. If a rule is not scrict, ANY trigger is enough.

Triggers
--------

A rule must spring into action at the right time! This is decided by triggers that you can set yourself. Here are some notable rule triggers that people use often:

* When a transaction is created
* When the description is something specific
* When the amount is above *X*.
* When the budget is *X*.

Rules can be set to be "strict" or not. If a rule is set to be strict, ALL triggers must match for the rule to fire. If a rule is not scrict, ANY trigger is enough.

Actions
-------

When the triggers are hit (either ALL or ANY, see the "strict" option), Firefly III will execute the associated rule actions. There are many actions available. Notable ones are:

* Change the budget, category, tag(s), description, amount
* Set a new description
* Change the source or destination account

Combined, this gives you a lot of power over your financial data.

You cannot fire other rules from a rule.

Stop processing
~~~~~~~~~~~~~~~

When you create a new rule, you can set an option called "stop processing". If you set it, and the rule is triggered, other rules in the group will NOT be processed any more.

For any trigger, you can also set the "stop processing" option. If you do, and the trigger is hit, it will stop processing other triggers in the rule. Whether or not the actions get executed depends on how many triggers were fired so far. If you hit 2 out of 2 when "stop processing" was hit, the actions will fire.

For each action, you can set "stop processing" as well. When you do, any actions after the current one will not fire.


Converting to another transaction type
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

If you set an action to convert your transaction to a deposit, a transfer or a withdrawal, make sure that you configure the rule action correctly. If you don't do this right the rule action wil *silently* fail and nothing will happen. Here you can read what will happen to your transaction. This is dependent on the original type and the future type of the transaction.

These conversions will *not* be applied to split transactions.


From a deposit to a withdrawal
    The money will be transferred away from the asset account instead of deposited into it. The "action value" you must provide must be the name of a valid expense account. If it does not exist, it will be created.

    If you leave the action value blank, the new expense account will be named after the revenue account. So, a deposit from "Your Boss" becomes a withdrawal at "Your Boss".

From a transfer to a withdrawal
	Firefly III will replace the "destination" asset account with an expense account. So, a transfer from your Checking Account to your Savings Account will be converted into a withdrawal from your Checkings Account to Account X, where X is an expense account. The "action value" you must provide must be the name of a valid expense account. If it does not exist, it will be created.

	If you leave the action value blank, the new expense account will be named after the original destination asset account.

From a withdrawal to a deposit
    The money will be deposited into the asset account instead of withdrawn from it. The "action value" you must provide must be the name of a valid revenue account. If it does not exist, it will be created.

    If you leave the action value blank, the new revenue account will be named after the original expense account. So, a withdrawal from "Walmart" becomes a deposit from "Walmart".

From a transfer to a deposit.
    Firefly III will replace the "source" asset account with an revenue account. So, a transfer from your Savings Account to your Checking Account will be converted into a deposit into your Checkings Account from Account X, where X is a revenue account. The "action value" you must provide must be the name of a valid revenue account. If it does not exist, it will be created.

    If you leave the action value blank, the new revenue account will be named after the original source asset account.

From a withdrawal to a transfer
    The money will be moved away from the original asset account, into another asset account. The "action value" you must provide must be the name of a valid destination asset account. If it does not exist, the action will fail.

    If you leave the action value empty, the action will fail.

From a deposit to a transfer
    The money will be moved into from the original asset account, from another asset account. The "action value" you must provide must be the name of a valid asset account. If it does not exist, the action will fail.

    If you leave the action value empty, the action will fail.

Apply rules
-----------

You can apply your rules to existing transactions. On the rule-overview (page ``/rules``), either use the "on/off"-icon or the ellipsis menu in a rule group to apply entire rule groups or individual rules to your transactions. See for some screenshots below.


Screenshots
-----------


.. figure:: https://firefly-iii.org/static/docs/4.7.0/rules-meta.png
   :alt: Meta data of a rule

   A new rule can be given some basic information.

.. figure:: https://firefly-iii.org/static/docs/4.7.0/rules-triggers.png
   :alt: Set the triggers

   First you would set up the triggers for the new rule.

.. figure:: https://firefly-iii.org/static/docs/4.7.0/rules-actions.png
   :alt: Set the actions

   Then decide on the actions to take.

.. figure:: https://firefly-iii.org/static/docs/4.7.6.2/apply-rule.png
   :alt: Option to run a rule on transactions.

   Option to run a rule on transactions.

.. figure:: https://firefly-iii.org/static/docs/4.7.6.2/apply-rule-group.png
   :alt: Option to run a rule group on transactions.

   Option to run a rule group on transactions.


浏览工单
==================

如果你正在寻找工单来处理, 可以在在 **概览** 菜单中查看.

.. figure:: /images/basics/find-ticket/browse.jpg
   :alt: 概览视图例子
   :align: center

   在主菜单中点击 **概览** 即可浏览工单.

.. hint:: 📥 把概览想象成是有不同过滤规则的 **收件箱**, 特定的规则显示指定条件的工单.

这里有 **七条内置的概览**
(Zammad 的管理员可以通过 `创建更多`_ 自定义条件的规则):

* **指派给我的工单My assigned tickets** (*open/pending* only)
* **处理中未指派的工单Unassigned & Open**
* **我的挂起到达提醒的工单My pending reached tickets** (previously marked *pending* and currently due)
* **我订阅的工单My Subscribed Tickets** ()
* **处理中的工单Open** (system-wide)
* **挂起到达提醒的工单Pending reached** (system-wide, previously marked *pending* and currently due)
* **升级的工单** (system-wide, failing to meet a `服务水平协议`_)

.. _创建更多: https://admin-docs.zammad.org/en/latest/manage/overviews.html
.. _服务水平协议:
   https://admin-docs.zammad.org/en/latest/manage/slas/index.html

.. tip:: **🖱️ 小技巧**

   * Click on column headings to change the display order.
   * Click-and-drag column dividers to adjust their width.
   * :doc:`Ticket states </basics/service-ticket/settings/state>` are
     **color-coded:**

     .. include:: /snippets/ticket-state-type-circles.rst
   * :doc:`Ticket priorities </basics/service-ticket/settings/priority>` are
     **color-coded:**

     .. figure:: /images/basics/service-ticket/settings/priority-colors.png
        :alt: Overview showing 3 tickets with different priorities
        :align: center

        Zammad's 3 default priorities allow you to see the importance of
        your tickets better.

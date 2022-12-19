浏览工单
========

如果你正在寻找工单来处理, 可以在在 **概览** 菜单中查看.

.. figure:: /images/basics/find-ticket/browse.jpg
   :alt: 概览视图例子
   :align: center

   在主菜单中点击 **概览** 即可浏览工单.

.. hint:: 📥 把概览想象成是有不同过滤规则的 **收件箱**, 特定的规则显示指定条件的工单.

这里有 **七条内置的概览**
(Zammad 的管理员可以通过 `创建更多`_ 自定义条件的规则):

* **指派给我的工单** (仅 *处理中/挂起* 状态的工单)
* **处理中未指派的工单** (所有处理中还没有指派所有者的工单)
* **我的挂起到达提醒的工单** (分配给我, 且标记为挂起并已到达提醒时间的工单)
* **我订阅的工单** (主动点订阅按钮或被其他人通过 @@ 订阅的工单会出现在这里)
* **处理中的工单** (系统所有正在处理中的工单)
* **挂起到达提醒的工单** (系统所有标记为挂起并已到达提醒时间的工单)
* **升级的工单** (系统所有 `服务水平协议`_ 超时的工单)

.. _创建更多: https://admin-docs.zammad.org/en/latest/manage/overviews.html
.. _服务水平协议:
   https://admin-docs.zammad.org/en/latest/manage/slas/index.html

.. tip:: **🖱️ 小技巧**

   * 点击标题列可更改显示顺序.
   * 点击并拖动列分隔符可调整字段的宽度.
   * Zammad 使用不同的 **颜色编码** 以区分不同的 :doc:`工单状态 </basics/service-ticket/settings/state>` :

     .. include:: /snippets/ticket-state-type-circles.rst
   * Zammad 使用不同的 **颜色编码** 以区分不同的 :doc:`工单优先级 </basics/service-ticket/settings/priority>` :

     .. figure:: /images/basics/service-ticket/settings/priority-colors.png
        :alt: 概览中显示3笔工单在不同的优先级
        :align: center

        Zammad 默认的三种优先级设置可以让你更好地看出你的工单的重要性. 

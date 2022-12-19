工单是什么?
===========

在 Zammad 中, **工单** 是用来跟踪客户服务请求的. 当客户第一次给你 (或公司) 发
邮件询问某事时, Zammad 会创建一个新的工单. 在你和客户之间发送的每条消息都会添加到
该工单中, 直到问题解决, 客户满意为止, 最终 **关闭** 工单.

所以, 基本上, **工单就是你和客户之间有关某个问题的消息会话**.


.. figure:: /images/basics/what-is-a-ticket.png
   :alt: 工单会话视图
   :align: center

   工单是客户和服务人员之间的消息会话.

.. hint:: 你知道你在做一件很棒的事! 当你

   1) 快速响应工单

   2) 并及时关闭.

   👀 你可以通过关注 :doc:`信息中心 </extras/dashboard>`
   了解自己的表现.

.. _ticket_settings:

工单设置
--------

Tickets also have metadata attached to them to make them easier to manage.
For instance, tickets have a customer and (optionally) an agent;
they can be open or closed (or even be scheduled for later);
they can be organized into groups;
and they can even be flagged for high or low priority.

For the sake of simplicity,
we’ll refer to this metadata as the **settings** of a ticket.
All of these settings can be changed at any time.
Each setting is explained in detail :doc:`here </basics/service-ticket/settings>`,
but for the time being, let’s go over the two most important ones:

Owner *(optional)*
   The **agent currently assigned to** (*i.e.,* responsible for) the ticket.

State
   Is the customer still waiting on an answer (**open**), or has the ticket
   been resolved (**closed**)?

.. include:: /snippets/ticket-settings-link-list.rst

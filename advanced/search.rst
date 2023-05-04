高级搜索
========

使用 Zammad, 您可以将搜索限制在特定信息上. 这样, 您就可以查找具有特定关键字和状态的工单. 
下面的信息将帮助您提高搜索结果.

例如, 您可以使用 ``customer.attribute`` 搜索特定客户::

   customer.firstname: 三

或::

   customer.lastname: 张


你可以使用带有 ``()`` 和 ``AND`` / ``OR`` 组合更复杂的条件进行搜索, 例如::

   state.name: open AND (article.from:me OR article.from:somebody)

.. hint::
   
   上面的 ``open`` 不能使中文的 **处理中**, 同样搜索 **已关闭** 的工单是使用 ``closed``.

例如::

   state.name: closed AND (article.from:me OR article.from:somebody)

.. note:: **🤓 Zammad 在 4.0 中对搜索语法作了重大变动**

   在 Zammad 3.6 以前的版本, 仅能搜索以下的关键词: 

      * group
      * priority
      * state
      * organization

   在 Zammad 4.0 之后, 关键词需要具体到某个对象. 这意味着需要在关键词后面
   添加 ``.name`` (例如 ``group.name`` 或 ``priority.name``) 
   来缩小搜索的范围.


可用的搜索关键词
--------------------

.. hint:: 

   如果需要所有的搜索关键词, 请参考 
   `Zammad 系统管理员手册 
   <https://docs.zammad.org/en/latest/install/elasticsearch/indexed-attributes.html>`_ 


.. |br| raw:: html

   <br />

.. csv-table:: 属性及其用法
   :header: "关键词", "值", "例子", "描述"
   :widths: 10, 10, 10, 20

   "工单号", "1118566", "number:1118566 |br|\ number:11185*", "直接搜索工单号, 支持通配符."
   "主题", "some title", "title:""some title"" |br|\ title:Printer |br|\ title: ""some ti*""", "如果搜索关键词中间含用空格字符, 请使用双引号, 这样 Zammad 会把引号内的内容视作一个关建词进行搜索. 单一关键词是不需要引号的."
   "工单创建时间", "2018-11-18", "created_at:2023-03-14 |br|\ created_at:[2023-03-14 TO 2023-10-24] |br|\ created_at:>now-1h", "你可以使用简单的日期, 日期范围或者 >now-xh。请注意, 日期格式应为 YYYY-MM-DD ."
   "工单状态", "new |br|\ open |br|\ closed", "state.name: new |br|\ state.name:new OR open", "你可以为特定的工单状态进行过滤 (甚至可以使用 OR 进行组合过滤). 请注意, 非在你的实例中定义了自定义工单状态, 否则需要使用英文命名的状态进行过滤."
   "消息数量", "5 |br|\ [5 TO 10] |br|\ [5 TO \*] |br|\ [\* TO 5]", "article_count:5 |br|\ article_count: [5 TO 10] |br|\ article_count:[5 TO \*] |br|\ article_count:[\* TO 5]", "你可以搜索具有特定数量文章的工单 (甚至可以搜索所有文章数量大于 5 的工单或者文章数量不超过 5 的工单, 如果需要的话)."
   "消息来自", "\*bob\*", "article.from:\*bob\*", "显示所有工单消息来源包含有""Bob""的内容."
   "消息正文", "heat |br|\ heat~ |br|\ /joh?n(ath[oa]n)/", "article.body:heat |br|\ article.body:heat~ |br|\ articlebody:/joh?n(ath[oa]n)/", "第一个例子展示了包含单词 ""heat"" 的所有工单 - 你还可以使用模糊操作符 ""~"" 来搜索类似的单词, 例如 ""head"". Zammad 还允许你在允许使用属性的地方使用正则表达式, 例如 ""/joh?n(ath[oa]n)/"" 匹配字符串中包含 ""john"" 或 ""johnathan"" 的内容, ""(ath[oa]n)"" 表示 ""athan"" 或 ""athon"", 其中 [] 表示匹配中括号内的任意一个字符."
   
.. hint:: **复杂的搜索组合**

  你可以使用 ``AND``, ``OR`` 和 ``TO`` 组合搜索关键词组合进一步缩小返回的结果,
  如果需要, 还可以用括号 ``()`` 将复杂搜索的关键词分开. 这样你就可以使用更多的 (AND/OR)
  实现更多的搜索条件. 如果你想排序某些搜索结果, 你可以使用否定 ``!``.
  下面提供一些搜索组合范例:
  
  .. csv-table:: 复杂的搜索组合示例
   :header: "搜索组合", "描述"
   :widths: 10, 20
   
   "state.name:(closed OR open) AND (priority.name:""2 normal"" OR tags:反馈)", "显示所有状态为 closed 或 open, 并且优先为 ""2 normal"" 或标记为 ""反馈"" 的工单."
   "state.name:(closed OR open) AND (priority.name:""2 normal"" OR tags:反馈) AND !(*Zammad*)", "这个结果与上面有些相似, 但从结果中排序了带有 ""Zammad"" 单词的工单."
   "owner.email:bob@example.net AND state.name:(open OR new)", "显示所以来自于 bob@example.net , 并且状态为处理中 open 或新建 new 的工单."
   "state.name:pending* AND article_count:[1 TO 5]", "显示所有任何挂起 pending 状态且消息数为1到5的所有内容."

工单属性及数据类型
-------------------------------------

下面是一些与工单或是消息有关的重要属性.

与工单有关的关键词
^^^^^^^^^^^^^^^^^^

   * number: 字符串
   * title: 字符串
   * group: 对象 (group.name, ...)
   * priority: 对象 (priority.name, ...)
   * state: 对象 (state.name, ...)
   * organization: 对象 (organization.name, ...)
   * owner: 对象 (owner.firstname, owner.lastname, owner.email, ...)
   * customer: 对象 
     (customer.firstname, customer.lastname, customer.email, ...)
   * first_response_at: 时间戳
   * first_response_in_min: 分钟 (工作时间内首次响应的时间)
   * close_at: 时间戳
   * close_in_min: 整数 (工作时间内多少分钟之前关闭的工单)
   * last_contact_at: 时间戳 (客户或服务人员最后一次联系的时间)
   * last_contact_agent_at: 时间戳 (服务人员最后一次联系的时间)
   * last_contact_customer_at: 时间戳 (客户最后一次联系的时间)
   * create_article_type: 字符串 (email|phone|web|...)
   * create_article_sender: 字符串 (Customer|Agent|System)
   * article_count: 整数
   * escalation_at: 时间戳
   * pending_time: 时间戳

与消息有关的关键词
^^^^^^^^^^^^^^^^^^

   * article.from: 字符串
   * article.to: 字符串
   * article.cc: 字符串
   * article.subject: 字符串
   * article.body: 字符串
   * article.attachment.title: 字符串 (附件的文件名)
   * article.attachment.content: 字符串 (附件内容)
   * article.attachment.content_type: 字符串 (文件类型, 例如 PDF)

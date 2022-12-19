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

.. csv-table:: Attributes and their usuage
   :header: "关键词", "值", "例子", "描述"
   :widths: 10, 10, 10, 20

   "工单号", "1118566", "number:1118566 |br|\ number:11185*", "直接搜索工单号, 支持通配符."
   "主题", "some title", "title:""some title"" |br|\ title:Printer |br|\ title: ""some ti*""", "If you need to use spacings in the search phrase, use quotes. Zammad will do a AND-Search over the given words. You can also use a single keyword without quotation."
   "工单创建时间", "2018-11-18", "created_at:2018-11-18 |br|\ created_at:[2018-11-15 TO 2018-11-18] |br|\ created_at:>now-1h", "You can either use a simple date, a date-range or >now-xh. Please note that the date format needs to be YYYY-MM-DD"
   "工单状态", "new |br|\ open |br|\ closed", "state.name: new |br|\ state.name:new OR open", "You can filter for specific ticket states (and even combine them with an OR). Please note that you need to use the english namings for states, unless you have custom ticket states defined in your instance."
   "消息数量", "5 |br|\ [5 TO 10] |br|\ [5 TO \*] |br|\ [\* TO 5]", "article_count:5 |br|\ article_count: [5 TO 10] |br|\ article_count:[5 TO \*] |br|\ article_count:[\* TO 5]", "You can search for Tickets with a specific number of articles (you can even search for everything with 5 or more articles or even up to 5 articles, if needed)."
   "消息来自", "\*bob\*", "article.from:\*bob\*", "Show all tickets that contain articles from ""Bob"""
   "消息正文", "heat |br|\ heat~ |br|\ /joh?n(ath[oa]n)/", "article.body:heat |br|\ article.body:heat~ |br|\ articlebody:/joh?n(ath[oa]n)/", "First example shows every ticket containing the word ""heat"" - you can also use the fuzzy operator ""~"" to search for similar words like e.g. like ""head"". Zammad will also allow you to use regular expressions, where ever the attributes allows it."
   
.. hint:: **复杂的搜索组合**

  You can combine search phrases by using ``AND``, ``OR`` and ``TO``, 
  depending on the situation and phrases you use. If needed, you can parts of 
  your search phrase for complex searches with ``()``. This allows you to 
  combine several phrases with different dependencies (AND/OR). In case you 
  receive search results that you want to exclude, you can use negation ``!``. 
  Below are some examples that you could use with this:
  
  .. csv-table:: Examples for search phrase combinations
   :header: "搜索组合", "描述"
   :widths: 10, 20
   
   "state.name:(closed OR open) AND (priority.name:""2 normal"" OR tags:feedback)", "Show every ticket that state is either closed or open and has priority normal or the tag feedback."
   "state.name:(closed OR open) AND (priority.name:""2 normal"" OR tags:feedback) AND !(*Zammad*)", "This gets the same result as above, expect that we don't want the ticket to contain anything matching to ""Zammad"""
   "owner.email:bob@example.net AND state.name:(open OR new)", "Show Tickets from bob@example.net that are either open or new"
   "state.name:pending* AND article_count:[1 TO 5]", "Show everything with any pending state and an article count of 1 to 5."

Some Ticket attributes and their type
-------------------------------------

Below you can find the most important attributes sorted by ticket and article.

与工单有关的关键词
^^^^^^^^^^^^^^^^^^

   * number: string
   * title: string
   * group: object (group.name, ...)
   * priority: object (priority.name, ...)
   * state: object (state.name, ...)
   * organization: object (organization.name, ...)
   * owner: object (owner.firstname, owner.lastname, owner.email, ...)
   * customer: object 
     (customer.firstname, customer.lastname, customer.email, ...)
   * first_response_at: timestamp
   * first_response_in_min: integer (business min till first response)
   * close_at: timestamp
   * close_in_min: integer (business min till close)
   * last_contact_at: timestamp (last contact by customer or agent)
   * last_contact_agent_at: timestamp (last contact by agent)
   * last_contact_customer_at: timestamp (last contact by customer)
   * create_article_type: string (email|phone|web|...)
   * create_article_sender: string (Customer|Agent|System)
   * article_count: integer
   * escalation_at: timestamp
   * pending_time: timestamp

与消息有关的关键词
^^^^^^^^^^^^^^^^^^

   * article.from: string
   * article.to: string
   * article.cc: string
   * article.subject: string
   * article.body: string
   * article.attachment.title: string (filename of attachment)
   * article.attachment.content: string (content of attachment)
   * article.attachment.content_type: string (File type e.g. PDF)

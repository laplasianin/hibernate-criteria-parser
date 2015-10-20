Hibernate allows you opportunity to create aliases when set the query.

But it can be pain to build significant query with a lot of joins if you receive somthing like following from cient:
<code>'document.creator.user.username' like 'Ivan' and 'document.creator.agent.fund.id' is null.</code>

You need to parse values like 'document.creator.user.username' automatically and also don't forget that if you create several different aliases to one path hibernate translates it to several different joins to one path (join creator as c1 join creator as c2...), so your query could became incorrect.

This simple lib provide you simple API to parse path (divider is dot symbol) and return string value represents end point of query you can use in restrictions. (it returns internall alias mapping name so you don't need to know full collections of aliases and worry about duplicates)

<b>Usage:</b>

1) Create new criteria builder in any way:<br>
<code>Criteria criteria = getSession().createCriteria(getEntityClass());</code>

2) Then create alias builder and feed it with criteria and query path:<br>

<code>CriteriaAliasBuilder aliasBuilder = new CriteriaAliasBuilder();</code>

<code>String queryPath = "document.creator.user.username";</code>

<code>String aliasToUserName = aliasBuilder.build(criteria, queryPath);</code>


3) And then you can use any restrictions:<br>

<code>Restrictions.eq(aliasToUserName, 'Ivan')</code>


it uses hibernate-annotations lib so you can add any implementations

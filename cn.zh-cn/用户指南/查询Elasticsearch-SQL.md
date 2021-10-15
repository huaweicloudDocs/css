# 查询Elasticsearch SQL<a name="css_01_0061"></a>

在6.5.4及之后版本中我们提供Open Distro for Elasticsearch SQL插件允许您使用SQL而不是Elasticsearch查询域特定语言（DSL）编写查询。

如果您已经熟悉SQL并且不想学习DSL查询，那么此功能是一个很好的选择。

## 基本操作<a name="section59231342303"></a>

要使用该功能，需要将请求发送到\_opendistro/\_sqlURI。您可以使用请求参数或请求正文（推荐）。

```
GET https://<host>:<port>/_opendistro/_sql?sql=select * from my-index limit 50
```

```
POST https://<host>:<port>/_opendistro/_sql
{
  "query": "SELECT * FROM my-index LIMIT 50"
}
```

您还可以使用curl命令：

```
curl -XPOST https://localhost:9200/_opendistro/_sql -u username:password -k -d '{"query": "SELECT * FROM kibana_sample_data_flights LIMIT 10"}' -H 'Content-Type: application/json'
```

默认情况下，查询返回JSON，但您也可以选择CSV格式返回数据，需要对format参数进行设置：

```
POST _opendistro/_sql?format=csv
{
  "query": "SELECT * FROM my-index LIMIT 50"
}
```

CSV格式返回数据时，每行对应一个文档，每列对应一个字段。

## 支持操作<a name="section17251759164012"></a>

我们支持的SQL操作包括声明、条件、聚合函数、Include和Exclude、常用函数、连接join和展示等操作。

-   声明statements

    **表 1**  声明statements

    <a name="table136696188464"></a>
    <table><thead align="left"><tr id="row18670121812462"><th class="cellrowborder" valign="top" width="12.58%" id="mcps1.2.3.1.1"><p id="p201811141478"><a name="p201811141478"></a><a name="p201811141478"></a>Statement</p>
    </th>
    <th class="cellrowborder" valign="top" width="87.42%" id="mcps1.2.3.1.2"><p id="p71821541475"><a name="p71821541475"></a><a name="p71821541475"></a>Example</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1667091864614"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p418244144714"><a name="p418244144714"></a><a name="p418244144714"></a>Select</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p31827484717"><a name="p31827484717"></a><a name="p31827484717"></a>SELECT * FROM my-index</p>
    </td>
    </tr>
    <tr id="row126709180463"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p1618213484716"><a name="p1618213484716"></a><a name="p1618213484716"></a>Delete</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p41821145479"><a name="p41821145479"></a><a name="p41821145479"></a>DELETE FROM my-index WHERE _id=1</p>
    </td>
    </tr>
    <tr id="row16701185462"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p6182340475"><a name="p6182340475"></a><a name="p6182340475"></a>Where</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p618220416477"><a name="p618220416477"></a><a name="p618220416477"></a>SELECT * FROM my-index WHERE ['field']='value'</p>
    </td>
    </tr>
    <tr id="row1367010187461"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p618213418474"><a name="p618213418474"></a><a name="p618213418474"></a>Order by</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p1918215484720"><a name="p1918215484720"></a><a name="p1918215484720"></a>SELECT * FROM my-index ORDER BY _id asc</p>
    </td>
    </tr>
    <tr id="row1767141804619"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p151820410478"><a name="p151820410478"></a><a name="p151820410478"></a>Group by</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p918244104712"><a name="p918244104712"></a><a name="p918244104712"></a>SELECT * FROM my-index GROUP BY range(age, 20,30,39)</p>
    </td>
    </tr>
    <tr id="row9671818144613"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p17182443475"><a name="p17182443475"></a><a name="p17182443475"></a>Limit</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p61821494717"><a name="p61821494717"></a><a name="p61821494717"></a>SELECT * FROM my-index LIMIT 50 (default is 200)</p>
    </td>
    </tr>
    <tr id="row1867115188466"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p51827419472"><a name="p51827419472"></a><a name="p51827419472"></a>Union</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p1818224194715"><a name="p1818224194715"></a><a name="p1818224194715"></a>SELECT * FROM my-index1 UNION SELECT * FROM my-index2</p>
    </td>
    </tr>
    <tr id="row196711618144617"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p51824494716"><a name="p51824494716"></a><a name="p51824494716"></a>Minus</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p1618212474720"><a name="p1618212474720"></a><a name="p1618212474720"></a>SELECT * FROM my-index1 MINUS SELECT * FROM my-index2</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >与任何复杂查询一样，大型UNION和MINUS语句可能会使集群资源紧张甚至崩溃。


-   条件Conditions

    **表 2**  条件Conditions

    <a name="table1788703814504"></a>
    <table><thead align="left"><tr id="row1888418383503"><th class="cellrowborder" valign="top" width="12.58%" id="mcps1.2.3.1.1"><p id="p1188413815017"><a name="p1188413815017"></a><a name="p1188413815017"></a>Condition</p>
    </th>
    <th class="cellrowborder" valign="top" width="87.42%" id="mcps1.2.3.1.2"><p id="p68842038185014"><a name="p68842038185014"></a><a name="p68842038185014"></a>Example</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row9884123845010"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p198841382502"><a name="p198841382502"></a><a name="p198841382502"></a>Like</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p8884638195015"><a name="p8884638195015"></a><a name="p8884638195015"></a>SELECT * FROM my-index WHERE name LIKE 'j%'</p>
    </td>
    </tr>
    <tr id="row20884123818507"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p3884163814505"><a name="p3884163814505"></a><a name="p3884163814505"></a>And</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p788463810505"><a name="p788463810505"></a><a name="p788463810505"></a>SELECT * FROM my-index WHERE name LIKE 'j%' AND age &gt; 21</p>
    </td>
    </tr>
    <tr id="row168841338185010"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p16884103818509"><a name="p16884103818509"></a><a name="p16884103818509"></a>Or</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p8884838175015"><a name="p8884838175015"></a><a name="p8884838175015"></a>SELECT * FROM my-index WHERE name LIKE 'j%' OR age &gt; 21</p>
    </td>
    </tr>
    <tr id="row8885138195017"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p16885638155011"><a name="p16885638155011"></a><a name="p16885638155011"></a>Count distinct</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p78851538115013"><a name="p78851538115013"></a><a name="p78851538115013"></a>SELECT count(distinct age) FROM my-index</p>
    </td>
    </tr>
    <tr id="row5885838195014"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p88851138145011"><a name="p88851138145011"></a><a name="p88851138145011"></a>In</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p9885123805012"><a name="p9885123805012"></a><a name="p9885123805012"></a>SELECT * FROM my-index WHERE name IN ('alejandro', 'carolina')</p>
    </td>
    </tr>
    <tr id="row38858384509"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p988512381506"><a name="p988512381506"></a><a name="p988512381506"></a>Not</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p888510387505"><a name="p888510387505"></a><a name="p888510387505"></a>SELECT * FROM my-index WHERE name NOT IN ('jane')</p>
    </td>
    </tr>
    <tr id="row88852382506"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p138855386507"><a name="p138855386507"></a><a name="p138855386507"></a>Between</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p1988583845011"><a name="p1988583845011"></a><a name="p1988583845011"></a>SELECT * FROM my-index WHERE age BETWEEN 20 AND 30</p>
    </td>
    </tr>
    <tr id="row188543810506"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p7885173875016"><a name="p7885173875016"></a><a name="p7885173875016"></a>Aliases</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p988523815501"><a name="p988523815501"></a><a name="p988523815501"></a>SELECT avg(age) AS Average_Age FROM my-index</p>
    </td>
    </tr>
    <tr id="row1388719382509"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p18887153820500"><a name="p18887153820500"></a><a name="p18887153820500"></a>Date</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p128870384504"><a name="p128870384504"></a><a name="p128870384504"></a>SELECT * FROM my-index WHERE birthday='1990-11-15'</p>
    </td>
    </tr>
    <tr id="row148871638175019"><td class="cellrowborder" valign="top" width="12.58%" headers="mcps1.2.3.1.1 "><p id="p888773815011"><a name="p888773815011"></a><a name="p888773815011"></a>Null</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.42%" headers="mcps1.2.3.1.2 "><p id="p20887203819506"><a name="p20887203819506"></a><a name="p20887203819506"></a>SELECT * FROM my-index WHERE name IS NULL</p>
    </td>
    </tr>
    </tbody>
    </table>

-   聚合函数Aggregation

    **表 3**  聚合函数Aggregation

    <a name="table14777194527"></a>
    <table><thead align="left"><tr id="row117783965212"><th class="cellrowborder" valign="top" width="12.04%" id="mcps1.2.3.1.1"><p id="p1822862318528"><a name="p1822862318528"></a><a name="p1822862318528"></a>Aggregation</p>
    </th>
    <th class="cellrowborder" valign="top" width="87.96000000000001%" id="mcps1.2.3.1.2"><p id="p11228723105220"><a name="p11228723105220"></a><a name="p11228723105220"></a>Example</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row677812985214"><td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.3.1.1 "><p id="p11228423145212"><a name="p11228423145212"></a><a name="p11228423145212"></a>avg()</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.96000000000001%" headers="mcps1.2.3.1.2 "><p id="p4228122315210"><a name="p4228122315210"></a><a name="p4228122315210"></a>SELECT avg(age) FROM my-index</p>
    </td>
    </tr>
    <tr id="row1577812914522"><td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.3.1.1 "><p id="p6228192385212"><a name="p6228192385212"></a><a name="p6228192385212"></a>count()</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.96000000000001%" headers="mcps1.2.3.1.2 "><p id="p5228323165217"><a name="p5228323165217"></a><a name="p5228323165217"></a>SELECT count(age) FROM my-index</p>
    </td>
    </tr>
    <tr id="row19778893529"><td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.3.1.1 "><p id="p722852325220"><a name="p722852325220"></a><a name="p722852325220"></a>max()</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.96000000000001%" headers="mcps1.2.3.1.2 "><p id="p1122802318526"><a name="p1122802318526"></a><a name="p1122802318526"></a>SELECT max(age) AS Highest_Age FROM my-index</p>
    </td>
    </tr>
    <tr id="row0778139175216"><td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.3.1.1 "><p id="p22281623175215"><a name="p22281623175215"></a><a name="p22281623175215"></a>min()</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.96000000000001%" headers="mcps1.2.3.1.2 "><p id="p222862345220"><a name="p222862345220"></a><a name="p222862345220"></a>SELECT min(age) AS Lowest_Age FROM my-index</p>
    </td>
    </tr>
    <tr id="row11778159125210"><td class="cellrowborder" valign="top" width="12.04%" headers="mcps1.2.3.1.1 "><p id="p11228923185219"><a name="p11228923185219"></a><a name="p11228923185219"></a>sum()</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.96000000000001%" headers="mcps1.2.3.1.2 "><p id="p15228323125218"><a name="p15228323125218"></a><a name="p15228323125218"></a>SELECT sum(age) AS Age_Sum FROM my-index</p>
    </td>
    </tr>
    </tbody>
    </table>


-   Include和Exclude字段

    **表 4**  Include和Exclude

    <a name="table54279212535"></a>
    <table><thead align="left"><tr id="row2428132125318"><th class="cellrowborder" valign="top" width="11.5%" id="mcps1.2.3.1.1"><p id="p1945132611535"><a name="p1945132611535"></a><a name="p1945132611535"></a>Pattern</p>
    </th>
    <th class="cellrowborder" valign="top" width="88.5%" id="mcps1.2.3.1.2"><p id="p29451226205312"><a name="p29451226205312"></a><a name="p29451226205312"></a>Example</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row742816295318"><td class="cellrowborder" valign="top" width="11.5%" headers="mcps1.2.3.1.1 "><p id="p18945726115312"><a name="p18945726115312"></a><a name="p18945726115312"></a>include()</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.5%" headers="mcps1.2.3.1.2 "><p id="p29451265533"><a name="p29451265533"></a><a name="p29451265533"></a>SELECT include('a*'), exclude('age') FROM my-index</p>
    </td>
    </tr>
    <tr id="row24288215316"><td class="cellrowborder" valign="top" width="11.5%" headers="mcps1.2.3.1.1 "><p id="p11945726105314"><a name="p11945726105314"></a><a name="p11945726105314"></a>exclude()</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.5%" headers="mcps1.2.3.1.2 "><p id="p18945142685318"><a name="p18945142685318"></a><a name="p18945142685318"></a>SELECT exclude('*name') FROM my-index</p>
    </td>
    </tr>
    </tbody>
    </table>


-   函数Functions

    **表 5**  函数Functions

    <a name="table1388491105413"></a>
    <table><thead align="left"><tr id="row28841411135411"><th class="cellrowborder" valign="top" width="11.41%" id="mcps1.2.3.1.1"><p id="p77251736135419"><a name="p77251736135419"></a><a name="p77251736135419"></a>Function</p>
    </th>
    <th class="cellrowborder" valign="top" width="88.59%" id="mcps1.2.3.1.2"><p id="p872593605420"><a name="p872593605420"></a><a name="p872593605420"></a>Example</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row5885811125411"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p372663615414"><a name="p372663615414"></a><a name="p372663615414"></a>floor</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p572653645411"><a name="p572653645411"></a><a name="p572653645411"></a>SELECT floor(number) AS Rounded_Down FROM my-index</p>
    </td>
    </tr>
    <tr id="row1088571116543"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p2726436155413"><a name="p2726436155413"></a><a name="p2726436155413"></a>trim</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p1272619363547"><a name="p1272619363547"></a><a name="p1272619363547"></a>SELECT trim(name) FROM my-index</p>
    </td>
    </tr>
    <tr id="row18885111115546"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p187261936165417"><a name="p187261936165417"></a><a name="p187261936165417"></a>log</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p13726236135416"><a name="p13726236135416"></a><a name="p13726236135416"></a>SELECT log(number) FROM my-index</p>
    </td>
    </tr>
    <tr id="row38852011195416"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p13726163675416"><a name="p13726163675416"></a><a name="p13726163675416"></a>log10</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p197263366547"><a name="p197263366547"></a><a name="p197263366547"></a>SELECT log10(number) FROM my-index</p>
    </td>
    </tr>
    <tr id="row19885181195414"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p11726193618544"><a name="p11726193618544"></a><a name="p11726193618544"></a>substring</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p57262367545"><a name="p57262367545"></a><a name="p57262367545"></a>SELECT substring(name, 2,5) FROM my-index</p>
    </td>
    </tr>
    <tr id="row58851811115410"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p172633665411"><a name="p172633665411"></a><a name="p172633665411"></a>round</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p87261836155412"><a name="p87261836155412"></a><a name="p87261836155412"></a>SELECT round(number) FROM my-index</p>
    </td>
    </tr>
    <tr id="row14885511155413"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p472653618540"><a name="p472653618540"></a><a name="p472653618540"></a>sqrt</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p19726336145413"><a name="p19726336145413"></a><a name="p19726336145413"></a>SELECT sqrt(number) FROM my-index</p>
    </td>
    </tr>
    <tr id="row14885101175420"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p14726236105419"><a name="p14726236105419"></a><a name="p14726236105419"></a>concat_ws</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p1972611368548"><a name="p1972611368548"></a><a name="p1972611368548"></a>SELECT concat_ws(' ', age, height) AS combined FROM my-index</p>
    </td>
    </tr>
    <tr id="row16885191105414"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p18726936165410"><a name="p18726936165410"></a><a name="p18726936165410"></a>/</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p372618366547"><a name="p372618366547"></a><a name="p372618366547"></a>SELECT number / 100 FROM my-index</p>
    </td>
    </tr>
    <tr id="row14885011105410"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p1272713616543"><a name="p1272713616543"></a><a name="p1272713616543"></a>%</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p19727153655417"><a name="p19727153655417"></a><a name="p19727153655417"></a>SELECT number % 100 FROM my-index</p>
    </td>
    </tr>
    <tr id="row11885511135416"><td class="cellrowborder" valign="top" width="11.41%" headers="mcps1.2.3.1.1 "><p id="p972713685413"><a name="p972713685413"></a><a name="p972713685413"></a>date_format</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.59%" headers="mcps1.2.3.1.2 "><p id="p3727436145418"><a name="p3727436145418"></a><a name="p3727436145418"></a>SELECT date_format(date, 'Y') FROM my-index</p>
    </td>
    </tr>
    </tbody>
    </table>

    >![](public_sys-resources/icon-note.gif) **说明：** 
    >必须在文档映射中启用fielddata才能使大多数字符串函数正常工作。


-   连接操作Joins

    **表 6**  连接操作Joins

    <a name="table2631133710555"></a>
    <table><thead align="left"><tr id="row36321937105512"><th class="cellrowborder" valign="top" width="11.59%" id="mcps1.2.3.1.1"><p id="p171605492551"><a name="p171605492551"></a><a name="p171605492551"></a>Join</p>
    </th>
    <th class="cellrowborder" valign="top" width="88.41%" id="mcps1.2.3.1.2"><p id="p1416024945513"><a name="p1416024945513"></a><a name="p1416024945513"></a>Example</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row13632937105516"><td class="cellrowborder" valign="top" width="11.59%" headers="mcps1.2.3.1.1 "><p id="p616054985515"><a name="p616054985515"></a><a name="p616054985515"></a>Inner join</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.41%" headers="mcps1.2.3.1.2 "><p id="p5160849115513"><a name="p5160849115513"></a><a name="p5160849115513"></a>SELECT p.firstname, p.lastname, p.gender, dogs.name FROM people p JOIN dogs d ON d.holdersName = p.firstname WHERE p.age &gt; 12 AND d.age &gt; 1</p>
    </td>
    </tr>
    <tr id="row18632153725514"><td class="cellrowborder" valign="top" width="11.59%" headers="mcps1.2.3.1.1 "><p id="p19160124955518"><a name="p19160124955518"></a><a name="p19160124955518"></a>Left outer join</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.41%" headers="mcps1.2.3.1.2 "><p id="p1516064917557"><a name="p1516064917557"></a><a name="p1516064917557"></a>SELECT p.firstname, p.lastname, p.gender, dogs.name FROM people p LEFT JOIN dogs d ON d.holdersName = p.firstname</p>
    </td>
    </tr>
    <tr id="row6632203785510"><td class="cellrowborder" valign="top" width="11.59%" headers="mcps1.2.3.1.1 "><p id="p131615491559"><a name="p131615491559"></a><a name="p131615491559"></a>Cross join</p>
    </td>
    <td class="cellrowborder" valign="top" width="88.41%" headers="mcps1.2.3.1.2 "><p id="p20161144995515"><a name="p20161144995515"></a><a name="p20161144995515"></a>SELECT p.firstname, p.lastname, p.gender, dogs.name FROM people p CROSS JOIN dogs d</p>
    </td>
    </tr>
    </tbody>
    </table>

    相关约束和限制，参考“连接操作Joins”。


-   展示Show

    展示show操作与索引模式匹配的索引和映射。您可以使用\*或%使用通配符。

    **表 7**  展示show

    <a name="table1919121475815"></a>
    <table><thead align="left"><tr id="row692041455817"><th class="cellrowborder" valign="top" width="12.22%" id="mcps1.2.3.1.1"><p id="p19984153416582"><a name="p19984153416582"></a><a name="p19984153416582"></a>Show</p>
    </th>
    <th class="cellrowborder" valign="top" width="87.78%" id="mcps1.2.3.1.2"><p id="p2098418342580"><a name="p2098418342580"></a><a name="p2098418342580"></a>Example</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row16920131416588"><td class="cellrowborder" valign="top" width="12.22%" headers="mcps1.2.3.1.1 "><p id="p10985133485814"><a name="p10985133485814"></a><a name="p10985133485814"></a>Show tables like</p>
    </td>
    <td class="cellrowborder" valign="top" width="87.78%" headers="mcps1.2.3.1.2 "><p id="p8985133410588"><a name="p8985133410588"></a><a name="p8985133410588"></a>SHOW TABLES LIKE logs-*</p>
    </td>
    </tr>
    </tbody>
    </table>


## 连接操作Joins<a name="section89917481618"></a>

Open Distro for Elasticsearch SQL支持inner joins, left outer joins,和cross joins。Join操作有许多约束：

-   您只能加入两个参数。

-   您必须为索引使用别名（例如people p）。

-   在ON子句中，您只能使用AND条件。

-   在WHERE语句中，不要将包含多个索引的树组合在一起。例如，以下语句有效：

    ```
    WHERE (a.type1 > 3 OR a.type1 < 0) AND (b.type2 > 4 OR b.type2 < -1)
    ```

    以下声明无效：

    ```
    WHERE (a.type1 > 3 OR b.type2 < 0) AND (a.type1 > 4 OR b.type2 < -1)
    ```


-   您不能使用GROUP BY或ORDER BY来获得结果。

-   LIMIT和OFFSET不支持一起使用（例如LIMIT 25 OFFSET 25）。

## JDBC驱动<a name="section153416302213"></a>

Java数据库连接（JDBC）驱动程序允许您将Open Distro for Elasticsearch与您的商业智能（BI）应用程序集成。

有关下载和使用JAR文件的信息，请参阅[GitHub仓库](https://github.com/opendistro-for-elasticsearch/sql-jdbc)。


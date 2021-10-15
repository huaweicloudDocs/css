# API概览<a name="css_03_0057"></a>

CSS提供的接口为符合RESTful API设计规范的自研接口。通过CSS的自研接口，您可以使用CSS的如[表1](#zh-cn_topic_0171174227_zh-cn_topic_0111426203_table6550431105030)所示的功能。

**表 1**  接口功能

<a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_table6550431105030"></a>
<table><thead align="left"><tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row1547110105030"><th class="cellrowborder" valign="top" width="23.646464646464647%" id="mcps1.2.4.1.1"><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p54101492105030"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p54101492105030"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p54101492105030"></a>接口</p>
</th>
<th class="cellrowborder" valign="top" width="25.393939393939398%" id="mcps1.2.4.1.2"><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p20144750105030"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p20144750105030"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p20144750105030"></a>功能</p>
</th>
<th class="cellrowborder" valign="top" width="50.95959595959596%" id="mcps1.2.4.1.3"><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p21112044105030"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p21112044105030"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p21112044105030"></a>API URI</p>
</th>
</tr>
</thead>
<tbody><tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row55790672105030"><td class="cellrowborder" rowspan="8" valign="top" width="23.646464646464647%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p19630156303"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p19630156303"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p19630156303"></a>集群管理接口</p>
<p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p726519334222"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p726519334222"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p726519334222"></a></p>
<p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p92651433102210"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p92651433102210"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p92651433102210"></a></p>
<p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p8265733172210"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p8265733172210"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p8265733172210"></a></p>
<p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p705174586"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p705174586"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p705174586"></a></p>
<p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p65859208585"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p65859208585"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p65859208585"></a></p>
</td>
<td class="cellrowborder" valign="top" width="25.393939393939398%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p30859977105030"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p30859977105030"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p30859977105030"></a><a href="创建集群.md">创建集群</a></p>
</td>
<td class="cellrowborder" valign="top" width="50.95959595959596%" headers="mcps1.2.4.1.3 "><pre class="screen" id="zh-cn_topic_0171174227_screen1712184173715"><a name="zh-cn_topic_0171174227_screen1712184173715"></a><a name="zh-cn_topic_0171174227_screen1712184173715"></a>POST /v1.0/{project_id}/clusters</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row15453874105030"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p58483711105030"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p58483711105030"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p58483711105030"></a><a href="查询集群列表.md">查询集群列表</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen1389320295471"><a name="zh-cn_topic_0171174227_screen1389320295471"></a><a name="zh-cn_topic_0171174227_screen1389320295471"></a>GET /v1.0/{project_id}/clusters</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row10170161211814"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p191413507285"><a name="p191413507285"></a><a name="p191413507285"></a><a href="查询集群详情.md">查询集群详情</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen15206531255"><a name="zh-cn_topic_0171174227_screen15206531255"></a><a name="zh-cn_topic_0171174227_screen15206531255"></a>GET /v1.0/{project_id}/clusters/{cluster_id}</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row125219148184"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p852121401818"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p852121401818"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p852121401818"></a><a href="删除集群.md">删除集群</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen1695846201113"><a name="zh-cn_topic_0171174227_screen1695846201113"></a><a name="zh-cn_topic_0171174227_screen1695846201113"></a>DELETE /v1.0/{project_id}/clusters/{cluster_id}</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row130151718589"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p9091714582"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p9091714582"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p9091714582"></a><a href="重启集群.md">重启集群</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen2401124204013"><a name="zh-cn_topic_0171174227_screen2401124204013"></a><a name="zh-cn_topic_0171174227_screen2401124204013"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/restart</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row13422317205811"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p17422131718586"><a name="zh-cn_topic_0171174227_p17422131718586"></a><a name="zh-cn_topic_0171174227_p17422131718586"></a><a href="扩容集群.md">扩容集群</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen129859211914"><a name="zh-cn_topic_0171174227_screen129859211914"></a><a name="zh-cn_topic_0171174227_screen129859211914"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/extend </pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row5331171415816"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p14332141475815"><a name="zh-cn_topic_0171174227_p14332141475815"></a><a name="zh-cn_topic_0171174227_p14332141475815"></a><a href="扩容实例的数量和存储容量.md">扩容实例的数量和存储容量</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen110063710489"><a name="zh-cn_topic_0171174227_screen110063710489"></a><a name="zh-cn_topic_0171174227_screen110063710489"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/role_extend</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row143916515910"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p12261113763114"><a name="p12261113763114"></a><a name="p12261113763114"></a><a href="获取实例规格列表.md">获取实例规格列表</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen961365211405"><a name="zh-cn_topic_0171174227_screen961365211405"></a><a name="zh-cn_topic_0171174227_screen961365211405"></a>GET /v1.0/{project_id}/es-flavors</pre>
</td>
</tr>
<tr id="row193661351732"><td class="cellrowborder" rowspan="5" valign="top" width="23.646464646464647%" headers="mcps1.2.4.1.1 "><p id="p836718511835"><a name="p836718511835"></a><a name="p836718511835"></a>集群管理接口</p>
<p id="p849561241"><a name="p849561241"></a><a name="p849561241"></a></p>
<p id="p14913015309"><a name="p14913015309"></a><a name="p14913015309"></a></p>
</td>
<td class="cellrowborder" valign="top" width="25.393939393939398%" headers="mcps1.2.4.1.2 "><p id="p336812511439"><a name="p336812511439"></a><a name="p336812511439"></a><a href="查询指定集群的标签.md">查询指定集群的标签</a></p>
</td>
<td class="cellrowborder" valign="top" width="50.95959595959596%" headers="mcps1.2.4.1.3 "><pre class="screen" id="screen1033055019575"><a name="screen1033055019575"></a><a name="screen1033055019575"></a>GET /v1.0/{project_id}/css-cluster/{cluster_id}/tags</pre>
</td>
</tr>
<tr id="row549261949"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p15491861341"><a name="p15491861341"></a><a name="p15491861341"></a><a href="查询所有标签.md">查询所有标签</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="screen110063710489"><a name="screen110063710489"></a><a name="screen110063710489"></a>GET /v1.0/{project_id}/css-cluster/tags</pre>
</td>
</tr>
<tr id="row1724731612510"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1624871618257"><a name="p1624871618257"></a><a name="p1624871618257"></a><a href="添加集群标签.md">添加集群标签</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="screen157372512456"><a name="screen157372512456"></a><a name="screen157372512456"></a>POST /v1.0/{project_id}/css-cluster/{cluster_id}/tags</pre>
</td>
</tr>
<tr id="row465021910256"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p865031910250"><a name="p865031910250"></a><a name="p865031910250"></a><a href="批量添加或删除集群标签.md">批量添加或删除集群标签</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="screen040172164815"><a name="screen040172164815"></a><a name="screen040172164815"></a>POST /v1.0/{project_id}/css-cluster/{cluster_id}/tags/action</pre>
</td>
</tr>
<tr id="row1236212432519"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p636213241251"><a name="p636213241251"></a><a name="p636213241251"></a><a href="删除集群指定标签.md">删除集群指定标签</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="screen13361126174613"><a name="screen13361126174613"></a><a name="screen13361126174613"></a>DELETE /v1.0/{project_id}/css-cluster/{cluster_id}/tags/{key}</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row7746927402"><td class="cellrowborder" rowspan="3" valign="top" width="23.646464646464647%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p81010371807"><a name="zh-cn_topic_0171174227_p81010371807"></a><a name="zh-cn_topic_0171174227_p81010371807"></a>词库管理接口（IK分词）</p>
</td>
<td class="cellrowborder" valign="top" width="25.393939393939398%" headers="mcps1.2.4.1.2 "><p id="p141802973320"><a name="p141802973320"></a><a name="p141802973320"></a><a href="加载自定义词库.md">加载自定义词库</a></p>
</td>
<td class="cellrowborder" valign="top" width="50.95959595959596%" headers="mcps1.2.4.1.3 "><pre class="screen" id="zh-cn_topic_0171174227_screen9271122910118"><a name="zh-cn_topic_0171174227_screen9271122910118"></a><a name="zh-cn_topic_0171174227_screen9271122910118"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/thesaurus</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row177472271011"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p6747227807"><a name="zh-cn_topic_0171174227_p6747227807"></a><a name="zh-cn_topic_0171174227_p6747227807"></a><a href="查询自定义词库状态.md">查询自定义词库状态</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen1459413411112"><a name="zh-cn_topic_0171174227_screen1459413411112"></a><a name="zh-cn_topic_0171174227_screen1459413411112"></a>GET /v1.0/{project_id}/clusters/{cluster_id}/thesaurus</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row1774715273011"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p177478271014"><a name="zh-cn_topic_0171174227_p177478271014"></a><a name="zh-cn_topic_0171174227_p177478271014"></a><a href="删除自定义词库.md">删除自定义词库</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen490125316112"><a name="zh-cn_topic_0171174227_screen490125316112"></a><a name="zh-cn_topic_0171174227_screen490125316112"></a>DELETE /v1.0/{project_id}/clusters/{cluster_id}/thesaurus</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row1878113271184"><td class="cellrowborder" rowspan="9" valign="top" width="23.646464646464647%" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p67811027161812"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p67811027161812"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p67811027161812"></a>快照管理接口</p>
</td>
<td class="cellrowborder" valign="top" width="25.393939393939398%" headers="mcps1.2.4.1.2 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p1878102721819"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p1878102721819"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p1878102721819"></a><a href="自动设置集群快照的基础配置（不推荐使用）.md">自动设置集群快照的基础配置（不推荐使用）</a></p>
</td>
<td class="cellrowborder" valign="top" width="50.95959595959596%" headers="mcps1.2.4.1.3 "><pre class="screen" id="zh-cn_topic_0171174227_screen168121631216"><a name="zh-cn_topic_0171174227_screen168121631216"></a><a name="zh-cn_topic_0171174227_screen168121631216"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/index_snapshot/auto_setting</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row394773371812"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p79471433141818"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p79471433141818"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p79471433141818"></a><a href="修改集群快照的基础配置.md">修改集群快照的基础配置</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="screen19252343816"><a name="screen19252343816"></a><a name="screen19252343816"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/index_snapshot/setting</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row1216861610572"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="p1267102983513"><a name="p1267102983513"></a><a name="p1267102983513"></a><a href="设置自动创建快照策略.md">设置自动创建快照策略</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen16814165091216"><a name="zh-cn_topic_0171174227_screen16814165091216"></a><a name="zh-cn_topic_0171174227_screen16814165091216"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/index_snapshot/policy</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_row2078413188578"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p1178419186579"><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p1178419186579"></a><a name="zh-cn_topic_0171174227_zh-cn_topic_0111426203_p1178419186579"></a><a href="查询集群的自动创建快照策略.md">查询集群的自动创建快照策略</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen2627181112137"><a name="zh-cn_topic_0171174227_screen2627181112137"></a><a name="zh-cn_topic_0171174227_screen2627181112137"></a>GET /v1.0/{project_id}/clusters/{cluster_id}/index_snapshot/policy</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row1998216200318"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p798211201732"><a name="zh-cn_topic_0171174227_p798211201732"></a><a name="zh-cn_topic_0171174227_p798211201732"></a><a href="手动创建快照.md">手动创建快照</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen103422026151316"><a name="zh-cn_topic_0171174227_screen103422026151316"></a><a name="zh-cn_topic_0171174227_screen103422026151316"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/index_snapshot</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row8366112712316"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p1436614271539"><a name="zh-cn_topic_0171174227_p1436614271539"></a><a name="zh-cn_topic_0171174227_p1436614271539"></a><a href="查询快照列表.md">查询快照列表</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen194613390135"><a name="zh-cn_topic_0171174227_screen194613390135"></a><a name="zh-cn_topic_0171174227_screen194613390135"></a>GET /v1.0/{project_id}/clusters/{cluster_id}/index_snapshots</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row1155918433317"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p17559643739"><a name="zh-cn_topic_0171174227_p17559643739"></a><a name="zh-cn_topic_0171174227_p17559643739"></a><a href="恢复快照.md">恢复快照</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="screen15657191319478"><a name="screen15657191319478"></a><a name="screen15657191319478"></a>POST /v1.0/{project_id}/clusters/{cluster_id}/index_snapshot/{snapshot_id}/restore</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row122881552634"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p528915521336"><a name="zh-cn_topic_0171174227_p528915521336"></a><a name="zh-cn_topic_0171174227_p528915521336"></a><a href="删除快照.md">删除快照</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="zh-cn_topic_0171174227_screen62433191415"><a name="zh-cn_topic_0171174227_screen62433191415"></a><a name="zh-cn_topic_0171174227_screen62433191415"></a>DELETE /v1.0/{project_id}/clusters/{cluster_id}/index_snapshot/{snapshot_id}</pre>
</td>
</tr>
<tr id="zh-cn_topic_0171174227_row1865610391236"><td class="cellrowborder" valign="top" headers="mcps1.2.4.1.1 "><p id="zh-cn_topic_0171174227_p265615391433"><a name="zh-cn_topic_0171174227_p265615391433"></a><a name="zh-cn_topic_0171174227_p265615391433"></a><a href="停用快照功能.md">停用快照功能</a></p>
</td>
<td class="cellrowborder" valign="top" headers="mcps1.2.4.1.2 "><pre class="screen" id="screen715056164610"><a name="screen715056164610"></a><a name="screen715056164610"></a>DELETE /v1.0/{project_id}/clusters/{cluster_id}/index_snapshots</pre>
</td>
</tr>
</tbody>
</table>


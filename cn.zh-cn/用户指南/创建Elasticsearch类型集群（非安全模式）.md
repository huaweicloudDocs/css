# 创建Elasticsearch类型集群（非安全模式）<a name="css_01_0094"></a>

在开始使用云搜索服务时，您必须创建一个集群。

## 背景信息<a name="section32701230131812"></a>

-   如果您要以折扣套餐计费方式使用集群，则需要提前购买折扣套餐，再创建与折扣套餐中区域、节点规格或者节点存储相同的集群。购买折扣套餐的具体操作步骤，请参见《价格说明》中的[折扣套餐](折扣套餐.md)章节。
-   如果您要以按需计费方式使用集群，则直接创建集群。

## 操作步骤<a name="section781857123412"></a>

1.  登录云搜索服务[管理控制台](https://console.huaweicloud.com/elasticsearch/?locale=zh-cn)。
2.  在“总览“或者“集群管理“页面，单击“创建集群“，进入“创建集群”页面。
3.  选择“当前区域“和“可用区“。

    **表 1**  区域和可用区参数说明

    <a name="table123919163912"></a>
    <table><thead align="left"><tr id="row6240191618912"><th class="cellrowborder" valign="top" width="35.28%" id="mcps1.2.3.1.1"><p id="p6240101619913"><a name="p6240101619913"></a><a name="p6240101619913"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="64.72%" id="mcps1.2.3.1.2"><p id="p1324019161897"><a name="p1324019161897"></a><a name="p1324019161897"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1324031620914"><td class="cellrowborder" valign="top" width="35.28%" headers="mcps1.2.3.1.1 "><p id="p82406161916"><a name="p82406161916"></a><a name="p82406161916"></a>当前<span id="text1094710917615"><a name="text1094710917615"></a><a name="text1094710917615"></a>区域</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="64.72%" headers="mcps1.2.3.1.2 "><p id="p1371716288100"><a name="p1371716288100"></a><a name="p1371716288100"></a>集群工作区域在右侧下拉框中选择。</p>
    </td>
    </tr>
    <tr id="row112401161695"><td class="cellrowborder" valign="top" width="35.28%" headers="mcps1.2.3.1.1 "><p id="p142401416791"><a name="p142401416791"></a><a name="p142401416791"></a>可用区</p>
    </td>
    <td class="cellrowborder" valign="top" width="64.72%" headers="mcps1.2.3.1.2 "><p id="p132401616890"><a name="p132401616890"></a><a name="p132401616890"></a>选择集群工作区域下关联的可用区。详细描述可参考<a href="https://support.huaweicloud.com/css_faq/css_02_0034.html" target="_blank" rel="noopener noreferrer">什么是区域和可用区</a>。</p>
    <p id="p869080899"><a name="p869080899"></a><a name="p869080899"></a>云搜索服务支持配置多个“可用区”，详细请参考<a href="https://support.huaweicloud.com/productdesc-css/css_04_0023.html" target="_blank" rel="noopener noreferrer">跨AZ高可用性介绍</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

4.  指定集群基本信息，选择“集群版本“，并输入“集群名称“。

    **表 2**  基本参数说明

    <a name="table1514341616111"></a>
    <table><thead align="left"><tr id="row10143191614119"><th class="cellrowborder" valign="top" width="23.48%" id="mcps1.2.3.1.1"><p id="p181437168110"><a name="p181437168110"></a><a name="p181437168110"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="76.52%" id="mcps1.2.3.1.2"><p id="p171431816161119"><a name="p171431816161119"></a><a name="p171431816161119"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row714311614114"><td class="cellrowborder" valign="top" width="23.48%" headers="mcps1.2.3.1.1 "><p id="p181127310148"><a name="p181127310148"></a><a name="p181127310148"></a>集群版本</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.52%" headers="mcps1.2.3.1.2 "><p id="p101431316141111"><a name="p101431316141111"></a><a name="p101431316141111"></a>当前支持5.5.1、6.2.3、6.5.4、7.1.1、7.6.2、7.9.3。</p>
    </td>
    </tr>
    <tr id="row31431616181112"><td class="cellrowborder" valign="top" width="23.48%" headers="mcps1.2.3.1.1 "><p id="p13143516151111"><a name="p13143516151111"></a><a name="p13143516151111"></a>集群名称</p>
    </td>
    <td class="cellrowborder" valign="top" width="76.52%" headers="mcps1.2.3.1.2 "><p id="p914318165115"><a name="p914318165115"></a><a name="p914318165115"></a>自定义的集群名称，可输入的字符范围为4～32个字符，只能包含数字、字母、中划线和下划线，且必须以字母开头。</p>
    <div class="note" id="note1364615174019"><a name="note1364615174019"></a><a name="note1364615174019"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p146469104015"><a name="p146469104015"></a><a name="p146469104015"></a>当集群创建成功后，您可以根据需求修改集群名称。单击需要修改的集群名称，进入集群基本信息页面，单击<span class="parmname" id="parmname101547139715"><a name="parmname101547139715"></a><a name="parmname101547139715"></a>“集群名称”</span>后面的<a name="image886165273813"></a><a name="image886165273813"></a><span><img id="image886165273813" src="figures/icon-edit-css-0.png"></span>，修改完成后，单击<a name="image112791138430"></a><a name="image112791138430"></a><span><img id="image112791138430" src="figures/icon-save-css.png"></span>，进行保存。如果需要取消修改，可单击<a name="image16489729134314"></a><a name="image16489729134314"></a><span><img id="image16489729134314" src="figures/icon-cancels-css.png"></span>进行取消。</p>
    </div></div>
    </td>
    </tr>
    </tbody>
    </table>

    **图 1**  基本信息配置<a name="fig94622525108"></a>  
    ![](figures/基本信息配置-1.png "基本信息配置-1")

5.  指定集群的主机规格相关参数。

    **表 3**  参数说明

    <a name="table950951922414"></a>
    <table><thead align="left"><tr id="css_01_0011_row14509181918241"><th class="cellrowborder" valign="top" width="25%" id="mcps1.2.3.1.1"><p id="css_01_0011_p150917199243"><a name="css_01_0011_p150917199243"></a><a name="css_01_0011_p150917199243"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="75%" id="mcps1.2.3.1.2"><p id="css_01_0011_p1350941916247"><a name="css_01_0011_p1350941916247"></a><a name="css_01_0011_p1350941916247"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="css_01_0011_row15509111982410"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p1350910198248"><a name="css_01_0011_p1350910198248"></a><a name="css_01_0011_p1350910198248"></a>节点数量</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p2050931982412"><a name="css_01_0011_p2050931982412"></a><a name="css_01_0011_p2050931982412"></a>集群中的节点个数。</p>
    <a name="css_01_0011_ul55091419152414"></a><a name="css_01_0011_ul55091419152414"></a><ul id="css_01_0011_ul55091419152414"><li>如果未启用Master节点和Client节点时，此参数指定的节点将被作为Master节点和Client节点，同时具备集群管理、存储数据、提供接入集群和分析数据的服务。此时，为保证集群中数据的稳定性，建议设置节点数量大于等于3个。</li><li>如果启用Master节点，且未启用Client节点，此参数指定的节点将用于存储数据并提供Client节点功能。</li><li>如果已启用Master节点和Client节点，此参数指定的节点将仅用于存储数据。</li><li>如果启用Client节点，且未启用Master节点，此参数指定的节点将用于存储数据并提供Master节点功能。</li></ul>
    </td>
    </tr>
    <tr id="css_01_0011_row65090196243"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p1250951902416"><a name="css_01_0011_p1250951902416"></a><a name="css_01_0011_p1250951902416"></a>节点规格</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p82922442343"><a name="css_01_0011_p82922442343"></a><a name="css_01_0011_p82922442343"></a>集群中的节点规格。</p>
    <p id="css_01_0011_p228785316512"><a name="css_01_0011_p228785316512"></a><a name="css_01_0011_p228785316512"></a>您可以选择任一系列，然后从对应系列中根据需要选择一个规格。每个集群只能选择一个规格，规格的详细说明可参考<a href="https://support.huaweicloud.com/productdesc-ecs/zh-cn_topic_0035470096.html" target="_blank" rel="noopener noreferrer">弹性云服务器的实例类型与规格</a>。您不能选择已售罄的CPU和内存资源。</p>
    </td>
    </tr>
    <tr id="css_01_0011_row175091919122413"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p650921919248"><a name="css_01_0011_p650921919248"></a><a name="css_01_0011_p650921919248"></a>节点存储</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p650911918249"><a name="css_01_0011_p650911918249"></a><a name="css_01_0011_p650911918249"></a>当前支持三种存储类型，普通I/O、高I/O、超高I/O。</p>
    </td>
    </tr>
    <tr id="css_01_0011_row250912197249"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p1950921962418"><a name="css_01_0011_p1950921962418"></a><a name="css_01_0011_p1950921962418"></a>节点存储<span id="css_01_0011_text194165916512"><a name="css_01_0011_text194165916512"></a><a name="css_01_0011_text194165916512"></a>容量</span></p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p16509181952416"><a name="css_01_0011_p16509181952416"></a><a name="css_01_0011_p16509181952416"></a>存储空间大小，其取值范围与节点规格关联，不同的规格允许的取值范围不同。</p>
    </td>
    </tr>
    <tr id="css_01_0011_row116591846144114"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p1366016468418"><a name="css_01_0011_p1366016468418"></a><a name="css_01_0011_p1366016468418"></a>按需套餐包</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p76603462416"><a name="css_01_0011_p76603462416"></a><a name="css_01_0011_p76603462416"></a>在购买集群时，可以根据需求，购买套餐包。对于长期使用者，推荐该方式。详细可参考<a href="https://support.huaweicloud.com/usermanual-css/css_06_0012.html" target="_blank" rel="noopener noreferrer">折扣套餐</a>。</p>
    </td>
    </tr>
    <tr id="css_01_0011_row155091119132418"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p125096195242"><a name="css_01_0011_p125096195242"></a><a name="css_01_0011_p125096195242"></a>启用Master节点</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p10509719182412"><a name="css_01_0011_p10509719182412"></a><a name="css_01_0011_p10509719182412"></a>Master节点用于管理集群中的所有节点。当需要存储和分析的数据量大，所需节点数量大于20个节点时，建议启用Master节点，保证集群的稳定性。反之，建议购买节点同时作为Master和Client节点即可，即仅设置集群的<span class="parmname" id="css_01_0011_parmname35095196246"><a name="css_01_0011_parmname35095196246"></a><a name="css_01_0011_parmname35095196246"></a>“节点数量”</span>参数。</p>
    <p id="css_01_0011_p1750971913243"><a name="css_01_0011_p1750971913243"></a><a name="css_01_0011_p1750971913243"></a>启用Master节点后，在下方选择对应的<span class="parmname" id="css_01_0011_parmname1050910191242"><a name="css_01_0011_parmname1050910191242"></a><a name="css_01_0011_parmname1050910191242"></a>“节点规格”</span>、<span class="parmname" id="css_01_0011_parmname185091219172411"><a name="css_01_0011_parmname185091219172411"></a><a name="css_01_0011_parmname185091219172411"></a>“节点数量”</span>和<span class="parmname" id="css_01_0011_parmname747011523515"><a name="css_01_0011_parmname747011523515"></a><a name="css_01_0011_parmname747011523515"></a>“节点存储”</span>。<span class="parmname" id="css_01_0011_parmname950918195249"><a name="css_01_0011_parmname950918195249"></a><a name="css_01_0011_parmname950918195249"></a>“节点数量”</span>必须是大于3的奇数，最多设置9个节点。其中<span class="parmname" id="css_01_0011_parmname18509191932411"><a name="css_01_0011_parmname18509191932411"></a><a name="css_01_0011_parmname18509191932411"></a>“节点存储”</span>的存储容量为固定值，存储类型可以根据实际情况选择，默认为存储容量为40GB的高I/O磁盘。</p>
    <div class="note" id="css_01_0011_note69581136111"><a name="css_01_0011_note69581136111"></a><a name="css_01_0011_note69581136111"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="css_01_0011_p1395920365115"><a name="css_01_0011_p1395920365115"></a><a name="css_01_0011_p1395920365115"></a>只有开通大集群权限的用户才能配置<span class="parmname" id="css_01_0011_parmname72147841318"><a name="css_01_0011_parmname72147841318"></a><a name="css_01_0011_parmname72147841318"></a>“启用Master节点”</span>和<span class="parmname" id="css_01_0011_parmname68430139139"><a name="css_01_0011_parmname68430139139"></a><a name="css_01_0011_parmname68430139139"></a>“启用Client节点”</span>参数。</p>
    </div></div>
    </td>
    </tr>
    <tr id="css_01_0011_row18509171911243"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p1450911198249"><a name="css_01_0011_p1450911198249"></a><a name="css_01_0011_p1450911198249"></a>启用Client节点</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p1550911198241"><a name="css_01_0011_p1550911198241"></a><a name="css_01_0011_p1550911198241"></a>Client节点用于提供客户端接入集群和分析数据的服务。当需要存储和分析的数据量大，所需节点数量大于20个节点时，建议启用Client节点，保证集群的稳定性。反之，建议购买节点同时作为Master和Client节点即可，即仅设置集群的<span class="parmname" id="css_01_0011_parmname15096192243"><a name="css_01_0011_parmname15096192243"></a><a name="css_01_0011_parmname15096192243"></a>“节点数量”</span>参数。</p>
    <p id="css_01_0011_p6509121992415"><a name="css_01_0011_p6509121992415"></a><a name="css_01_0011_p6509121992415"></a>启用Client节点后，在下方选择对应的<span class="parmname" id="css_01_0011_parmname16509181952411"><a name="css_01_0011_parmname16509181952411"></a><a name="css_01_0011_parmname16509181952411"></a>“节点规格”</span>、<span class="parmname" id="css_01_0011_parmname165096197248"><a name="css_01_0011_parmname165096197248"></a><a name="css_01_0011_parmname165096197248"></a>“节点数量”</span>和<span class="parmname" id="css_01_0011_parmname1585081873719"><a name="css_01_0011_parmname1585081873719"></a><a name="css_01_0011_parmname1585081873719"></a>“节点存储”</span>。<span class="parmname" id="css_01_0011_parmname7509171917247"><a name="css_01_0011_parmname7509171917247"></a><a name="css_01_0011_parmname7509171917247"></a>“节点数量”</span>可设置为1~32任意数值。其中<span class="parmname" id="css_01_0011_parmname254011417363"><a name="css_01_0011_parmname254011417363"></a><a name="css_01_0011_parmname254011417363"></a>“节点存储”</span>的存储容量为固定值，存储类型可以根据实际情况选择，默认为存储容量为40GB的高I/O磁盘。</p>
    </td>
    </tr>
    <tr id="css_01_0011_row12889131219416"><td class="cellrowborder" valign="top" width="25%" headers="mcps1.2.3.1.1 "><p id="css_01_0011_p1389081294118"><a name="css_01_0011_p1389081294118"></a><a name="css_01_0011_p1389081294118"></a>启用冷数据节点</p>
    </td>
    <td class="cellrowborder" valign="top" width="75%" headers="mcps1.2.3.1.2 "><p id="css_01_0011_p18902012184113"><a name="css_01_0011_p18902012184113"></a><a name="css_01_0011_p18902012184113"></a>冷数据节点用于存放对于历史数据要求分钟级别的返回。当用户对历史数据返回时间要求不是很高的话，可以将这部分数据存储在冷数据节点上，从而降低成本。</p>
    <p id="css_01_0011_p57631824383"><a name="css_01_0011_p57631824383"></a><a name="css_01_0011_p57631824383"></a>冷数据节点为可选节点，支持的节点个数为1-32个。</p>
    <p id="css_01_0011_p1024710511283"><a name="css_01_0011_p1024710511283"></a><a name="css_01_0011_p1024710511283"></a>开启冷数据节点之后，云搜索服务将会自动的给相关节点打上冷热标签，相关的集群参数，配置详情请参见<a href="https://www.elastic.co/guide/en/elasticsearch/reference/master/allocation-awareness.html" target="_blank" rel="noopener noreferrer">https://www.elastic.co/guide/en/elasticsearch/reference/master/allocation-awareness.html</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

    **图 2**  设置主机规格<a name="fig57951699305"></a>  
    ![](figures/设置主机规格-2.png "设置主机规格-2")

6.  指定集群的网络规格相关参数。

    **表 4**  参数说明

    <a name="table29572519253"></a>
    <table><thead align="left"><tr id="row159579512517"><th class="cellrowborder" valign="top" width="24.47%" id="mcps1.2.3.1.1"><p id="p2095710562511"><a name="p2095710562511"></a><a name="p2095710562511"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="75.53%" id="mcps1.2.3.1.2"><p id="p149578519252"><a name="p149578519252"></a><a name="p149578519252"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row1895720513251"><td class="cellrowborder" valign="top" width="24.47%" headers="mcps1.2.3.1.1 "><p id="p1195718522512"><a name="p1195718522512"></a><a name="p1195718522512"></a>虚拟私有云</p>
    </td>
    <td class="cellrowborder" valign="top" width="75.53%" headers="mcps1.2.3.1.2 "><p id="p264085512814"><a name="p264085512814"></a><a name="p264085512814"></a>VPC即虚拟私有云，是通过逻辑方式进行网络隔离，提供安全、隔离的网络环境。</p>
    <p id="p41161851162810"><a name="p41161851162810"></a><a name="p41161851162810"></a>选择创建集群需要的VPC，单击<span class="parmname" id="parmname2011675115289"><a name="parmname2011675115289"></a><a name="parmname2011675115289"></a>“查看虚拟私有云”</span>进入VPC服务查看已创建的VPC名称和ID。如果没有VPC，需要创建一个新的VPC。</p>
    <div class="note" id="note114411478188"><a name="note114411478188"></a><a name="note114411478188"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p1344127131818"><a name="p1344127131818"></a><a name="p1344127131818"></a>此处您选择的VPC必须包含网段（CIDR），否则集群将无法创建成功。新建的VPC默认包含网段（CIDR）。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row595765162514"><td class="cellrowborder" valign="top" width="24.47%" headers="mcps1.2.3.1.1 "><p id="p4957358252"><a name="p4957358252"></a><a name="p4957358252"></a>子网</p>
    </td>
    <td class="cellrowborder" valign="top" width="75.53%" headers="mcps1.2.3.1.2 "><p id="p18101747131315"><a name="p18101747131315"></a><a name="p18101747131315"></a>通过子网提供与其他网络隔离的、可以独享的网络资源，以提高网络安全。</p>
    <p id="p269214423135"><a name="p269214423135"></a><a name="p269214423135"></a>选择创建集群需要的子网，可进入VPC服务查看VPC下已创建的子网名称和ID。</p>
    </td>
    </tr>
    <tr id="row295715514257"><td class="cellrowborder" valign="top" width="24.47%" headers="mcps1.2.3.1.1 "><p id="p19571653255"><a name="p19571653255"></a><a name="p19571653255"></a>安全组</p>
    </td>
    <td class="cellrowborder" valign="top" width="75.53%" headers="mcps1.2.3.1.2 "><p id="p12957856252"><a name="p12957856252"></a><a name="p12957856252"></a>安全组是一个逻辑上的分组，为同一个VPC内具有相同安全保护需求并相互信任的弹性云服务器提供访问策略。单击<span class="parmname" id="parmname144113710185"><a name="parmname144113710185"></a><a name="parmname144113710185"></a>“查看安全组”</span>可了解安全组详情。</p>
    <div class="note" id="note1744217181810"><a name="note1744217181810"></a><a name="note1744217181810"></a><span class="notetitle"> 说明： </span><div class="notebody"><p id="p174421275180"><a name="p174421275180"></a><a name="p174421275180"></a>请确保安全组的<span class="parmname" id="parmname4442275183"><a name="parmname4442275183"></a><a name="parmname4442275183"></a>“端口范围/ICMP类型”</span>为<span class="parmvalue" id="parmvalue174429711817"><a name="parmvalue174429711817"></a><a name="parmvalue174429711817"></a>“Any”</span>或者包含端口9200的端口范围。</p>
    </div></div>
    </td>
    </tr>
    <tr id="row1095719532518"><td class="cellrowborder" valign="top" width="24.47%" headers="mcps1.2.3.1.1 "><p id="p119571151254"><a name="p119571151254"></a><a name="p119571151254"></a>安全模式</p>
    </td>
    <td class="cellrowborder" valign="top" width="75.53%" headers="mcps1.2.3.1.2 "><p id="p19743821141412"><a name="p19743821141412"></a><a name="p19743821141412"></a>关闭安全模式。</p>
    </td>
    </tr>
    <tr id="row119571856258"><td class="cellrowborder" valign="top" width="24.47%" headers="mcps1.2.3.1.1 "><p id="p1495775102513"><a name="p1495775102513"></a><a name="p1495775102513"></a>企业项目</p>
    </td>
    <td class="cellrowborder" valign="top" width="75.53%" headers="mcps1.2.3.1.2 "><p id="p1213911541512"><a name="p1213911541512"></a><a name="p1213911541512"></a>如果您开通了企业项目，在创建云搜索服务集群时，您可以给集群绑定一个企业项目。您可以在右侧下拉框中选择当前用户下已创建的企业项目，也可以通过单击<span class="uicontrol" id="uicontrol230020193714"><a name="uicontrol230020193714"></a><a name="uicontrol230020193714"></a>“查看项目管理”</span>按钮，前往<span class="parmname" id="parmname116821641182610"><a name="parmname116821641182610"></a><a name="parmname116821641182610"></a>“企业项目管理”</span>管理控制台，新建企业项目和查看已有的企业项目。</p>
    </td>
    </tr>
    <tr id="row158401727210"><td class="cellrowborder" valign="top" width="24.47%" headers="mcps1.2.3.1.1 "><p id="p1610483814506"><a name="p1610483814506"></a><a name="p1610483814506"></a>集群快照开关</p>
    </td>
    <td class="cellrowborder" valign="top" width="75.53%" headers="mcps1.2.3.1.2 "><a name="ul1097111005710"></a><a name="ul1097111005710"></a><ul id="ul1097111005710"><li>基础配置<a name="ul720218881214"></a><a name="ul720218881214"></a><ul id="ul720218881214"><li>OBS桶：快照存储的OBS桶的名称。</li><li>备份路径：快照在OBS桶中的存放路径。</li><li>IAM委托：指当前账户授权<span id="text18960152712494"><a name="text18960152712494"></a><a name="text18960152712494"></a>云搜索服务</span>访问或维护存储在OBS中数据。</li></ul>
    <p id="p1887414335131"><a name="p1887414335131"></a><a name="p1887414335131"></a>具体详细信息，请参考<a href="https://support.huaweicloud.com/usermanual-css/css_01_0033.html#section1" target="_blank" rel="noopener noreferrer">管理自动创建快照</a>。</p>
    </li><li>自动创建快照<p id="p1841849325"><a name="p1841849325"></a><a name="p1841849325"></a>默认情况下，系统打开了<span class="parmname" id="parmname1141817911217"><a name="parmname1141817911217"></a><a name="parmname1141817911217"></a>“自动快照创建”</span>开关，您可以根据自己的需求设置<span class="parmname" id="parmname84181597218"><a name="parmname84181597218"></a><a name="parmname84181597218"></a>“快照名称前缀”</span>、<span class="parmname" id="parmname34191595216"><a name="parmname34191595216"></a><a name="parmname34191595216"></a>“备份开始时间”</span>和<span class="parmname" id="parmname0419179925"><a name="parmname0419179925"></a><a name="parmname0419179925"></a>“保留时间（天）”</span>。如果您不需要启用自动快照，可以在<span class="parmname" id="parmname1841912918214"><a name="parmname1841912918214"></a><a name="parmname1841912918214"></a>“自动快照创建”</span>右侧，单击开关关闭自动创建快照功能。</p>
    <a name="ul164197913210"></a><a name="ul164197913210"></a><ul id="ul164197913210"><li><span class="parmname" id="parmname34199919217"><a name="parmname34199919217"></a><a name="parmname34199919217"></a>“快照名称前缀”</span>：快照名称由快照名称前缀加上时间戳组成，例如自动生成的快照名称snapshot-1566921603720。快照名称前缀的长度为1～32个字符，只能包含小写字母、数字、中划线和下划线，且必须以小写字母开头。</li><li><span class="parmname" id="parmname1341910910214"><a name="parmname1341910910214"></a><a name="parmname1341910910214"></a>“备份开始时间”</span>：指每天自动开始备份的时间，只能指定整点时间，如00:00、01:00，取值范围为00:00～23:00。请在下拉框中选择备份时间。</li><li><span class="parmname" id="parmname18419191521"><a name="parmname18419191521"></a><a name="parmname18419191521"></a>“保留时间（天）”</span>：指备份的快照在OBS的保留时间，以天为单位，取值范围为1～90，您可以根据自己的需求进行设置。系统在半点时刻会自动删除超过保留时间的快照。</li></ul>
    <p id="p154191691322"><a name="p154191691322"></a><a name="p154191691322"></a>例如：自动快照创建的策略设置如<a href="#fig438122816367">图4</a>所示，则系统会在35天后的00:30自动删除35天前00:00自动开始备份的快照。</p>
    </li></ul>
    </td>
    </tr>
    </tbody>
    </table>

    **图 3**  设置网络规格<a name="fig187844173412"></a>  
    ![](figures/设置网络规格-3.png "设置网络规格-3")

    **图 4**  设置自动快照创建的相关参数<a name="fig438122816367"></a>  
    ![](figures/设置自动快照创建的相关参数-4.png "设置自动快照创建的相关参数-4")

7.  配置集群高级配置功能。

    “高级配置“：选择“默认配置“，则默认关闭“终端节点服务“和“标签“功能。如果需要配置“终端节点服务“、“标签“功能，选择“自定义“。

    **表 5**  高级配置参数

    <a name="table2687931145214"></a>
    <table><thead align="left"><tr id="row66871131125211"><th class="cellrowborder" valign="top" width="28.470000000000002%" id="mcps1.2.3.1.1"><p id="p668893116529"><a name="p668893116529"></a><a name="p668893116529"></a>参数</p>
    </th>
    <th class="cellrowborder" valign="top" width="71.53%" id="mcps1.2.3.1.2"><p id="p268873119525"><a name="p268873119525"></a><a name="p268873119525"></a>说明</p>
    </th>
    </tr>
    </thead>
    <tbody><tr id="row18688153185211"><td class="cellrowborder" valign="top" width="28.470000000000002%" headers="mcps1.2.3.1.1 "><p id="p868833111527"><a name="p868833111527"></a><a name="p868833111527"></a>终端节点服务</p>
    </td>
    <td class="cellrowborder" valign="top" width="71.53%" headers="mcps1.2.3.1.2 "><p id="p463119361535"><a name="p463119361535"></a><a name="p463119361535"></a>开启终端节点服务后，用户可以获得一个内网访问的域名，通过这个域名，可以在同一个vpc内访问该集群。详细配置请参考<a href="终端节点服务.md">终端节点服务</a>。</p>
    </td>
    </tr>
    <tr id="row7688143119529"><td class="cellrowborder" valign="top" width="28.470000000000002%" headers="mcps1.2.3.1.1 "><p id="p968843165210"><a name="p968843165210"></a><a name="p968843165210"></a>标签</p>
    </td>
    <td class="cellrowborder" valign="top" width="71.53%" headers="mcps1.2.3.1.2 "><p id="p765315035317"><a name="p765315035317"></a><a name="p765315035317"></a>为集群添加标签，可以方便用户识别和管理拥有的集群资源。此处您可以选择<span class="parmname" id="parmname290571616233"><a name="parmname290571616233"></a><a name="parmname290571616233"></a>“标签管理服务”</span>中已定义好的<span class="parmname" id="parmname4601719162316"><a name="parmname4601719162316"></a><a name="parmname4601719162316"></a>“预定义标签”</span>，也可以自己定义标签。详细标签使用请参考<a href="标签管理.md">标签管理</a>。</p>
    </td>
    </tr>
    </tbody>
    </table>

8.  单击“立即申请“，进入规格确认界面。
9.  规格确认完成后，单击“提交申请“开始创建集群。
10. 单击“返回集群列表“，系统将跳转到“集群管理“页面。您创建的集群将展现在集群列表中，且集群状态为“创建中“，创建成功后集群状态会变为“可用“。

    如果集群创建失败，请根据界面提示，重新创建集群。



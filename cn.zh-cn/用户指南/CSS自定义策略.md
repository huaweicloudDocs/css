# CSS自定义策略<a name="css_01_0086"></a>

如果系统预置的CSS权限，不满足您的授权要求，可以创建自定义策略。自定义策略中可以添加的授权项（Action）请参考[权限策略和授权项](https://support.huaweicloud.com/api-css/css_03_0065.html)。

目前华为云支持以下两种方式创建自定义策略：

-   可视化视图创建自定义策略：无需了解策略语法，按可视化视图导航栏选择云服务、操作、资源、条件等策略内容，可自动生成策略。
-   JSON视图创建自定义策略：可以在选择策略模板后，根据具体需求编辑策略内容；也可以直接在编辑框内编写JSON格式的策略内容。
-   具体创建步骤请参见：[创建自定义策略](https://support.huaweicloud.com/usermanual-iam/iam_01_0605.html)。本章为您介绍常用的CSS自定义策略样例。

## CSS系统策略样例<a name="section19521230141915"></a>

示例1：授权用户CSS FullAccess权限，即给用户配置CSS的所有权限。

开启CSS FullAccess权限，需要依赖OBS和IAM权限，除了配CSS FullAccess还要加上IAM ReadOnlyAccess和OBS的所有权限。如果用户需要查看集群监控信息，则需要依赖CES的只读权限。如果用户需要使用终端节服务，除了配置VPCEndpoint Administrator权限，还需要同时配置VPC Administrator、Server Administrator以及DNS Administrator权限。如果用户需要使用标签功能，需要配置TMS Administrator权限。

>![](public_sys-resources/icon-note.gif) **说明：** 
>如果是子账户，需要同时设置GetBucketStoragePolicy、GetBucketLocation、ListBucket权限，才能看到OBS桶。

1.  授权用户CSS FullAccess权限。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Action": [
                    "css:*:*",
                    "vpc:securityGroups:get",
                    "vpc:securityGroups:create",
                    "vpc:securityGroups:delete",
                    "vpc:securityGroupRules:get",
                    "vpc:securityGroupRules:create",
                    "vpc:securityGroupRules:delete",
                    "vpc:vpcs:list",
                    "vpc:privateIps:list",
                    "vpc:ports:get",
                    "vpc:ports:create",
                    "vpc:ports:update",
                    "vpc:ports:delete",
                    "vpc:quotas:list",
                    "vpc:subnets:get",
                    "ecs:cloudServerFlavors:get",
                    "ecs:serverInterfaces:use",
                    "ecs:cloudServers:addNics",
                    "ecs:quotas:get",
                    "evs:types:get",
                    "evs:quotas:get"                
                ],
                "Effect": "Allow"
            }
        ]
    }
    ```

2.  授权用户IAM ReadOnlyAccess自定义策略。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Action": [
                    "iam:*:get*",
                    "iam:*:list*",
                    "iam:*:check*"
                ],
                "Effect": "Allow"
            }
        ]
    }
    ```

3.  授权用户OBS的所有权限。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Action": [
                    "OBS:*:*"
                ],
                "Effect": "Allow"
            }
        ]
    }
    ```

4.  （可选）授权用户查看集群监控信息权限。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Action": [
                    "ces:*:get*",
                    "ces:*:list*"
                ],
                "Effect": "Allow"
            }
        ]
    }
    ```

5.  （可选）授权用户VPCEndpoint Administrator权限。

    ```
    {
        "Version": "1.0",
        "Statement": [
            {
                "Action": [
                    "VPCEP:endpoint_services:*"
                ],
                "Effect": "Allow"
            }
        ],
        "Depends": [
            {
                "catalog": "BASE",
                "display_name": "Server Administrator"
            },
            {
                "catalog": "VPC",
                "display_name": "VPC Administrator"
            },
            {
                "catalog": "DNS",
                "display_name": "DNS Administrator"
            }
        ]
    }
    ```

6.  （可选）授权VPC Administrator权限。

    ```
    {
        "Version": "1.0",
        "Statement": [
            {
                "Action": [
                    "vpc:vpcs:*",
                    "vpc:routers:*",
                    "vpc:networks:*",
                    "vpc:subnets:*",
                    "vpc:ports:*",
                    "vpc:privateIps:*",
                    "vpc:peerings:*",
                    "vpc:routes:*",
                    "vpc:lbaas:*",
                    "vpc:vpns:*",
                    "ecs:*:get",
                    "ecs:*:list",
                    "elb:*:get",
                    "elb:*:list"
                ],
                "Effect": "Allow"
            }
        ]
    }
    ```

7.  （可选）授权Server Administrator权限。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Action": [
                    "ecs:*:*",
                    "evs:*:get",
                    "evs:*:list",
                    "evs:volumes:create",
                    "evs:volumes:delete",
                    "evs:volumes:attach",
                    "evs:volumes:detach",
                    "evs:volumes:manage",
                    "evs:volumes:update",
                    "evs:volumes:uploadImage",
                    "evs:snapshots:create",
                    "vpc:*:get",
                    "vpc:*:list",
                    "vpc:networks:create",
                    "vpc:networks:update",
                    "vpc:subnets:update",
                    "vpc:subnets:create",
                    "vpc:routers:get",
                    "vpc:routers:update",
                    "vpc:ports:*",
                    "vpc:privateIps:*",
                    "vpc:securityGroups:*",
                    "vpc:securityGroupRules:*",
                    "vpc:floatingIps:*",
                    "vpc:publicIps:*",
                    "vpc:bandwidths:*",
                    "vpc:firewalls:*",
                    "ims:images:create",
                    "ims:images:delete",
                    "ims:images:get",
                    "ims:images:list",
                    "ims:images:update",
                    "ims:images:upload"
                ],
                "Effect": "Allow"
            }
        ],
        "Depends": [
            {
                "catalog": "BASE",
                "display_name": "Tenant Guest"
            },
            {
                "catalog": "BASE",
                "display_name": "BSS Administrator"
            },
            {
                "catalog": "BASE",
                "display_name": "VPC Administrator"
            },
            {
                "catalog": "BASE",
                "display_name": "IMS Administrator"
            }
        ]
    }
    ```

8.  （可选）授权DNS Administrator权限。

    ```
    {
        "Version": "1.0",
        "Statement": [
            {
                "Action": [
                    "DNS:Zone:*",
                    "DNS:RecordSet:*",
                    "DNS:PTRRecord:*"
                ],
                "Effect": "Allow"
            }
        ],
        "Depends": [
            {
                "catalog": "BASE",
                "display_name": "Tenant Guest"
            },
            {
                "catalog": "VPC",
                "display_name": "VPC Administrator"
            }
        ]
    }
    ```


1.  （可选）授权TMS Administrator权限。

    ```
    {
        "Version": "1.0",
        "Statement": [
            {
                "Action": [
                    "TMS:predefine_tag:*",
                    "TMS:resource_tag:*"
                ],
                "Effect": "Allow"
            }
        ],
        "Depends": [
            {
                "catalog": "BASE",
                "display_name": "Tenant Guest"
            },
            {
                "catalog": "BASE",
                "display_name": "Server Administrator"
            },
            {
                "catalog": "IMS",
                "display_name": "IMS Administrator"
            },
            {
                "catalog": "Auto Scaling",
                "display_name": "AutoScaling Administrator"
            },
            {
                "catalog": "VPC",
                "display_name": "VPC Administrator"
            },
            {
                "catalog": "VBS",
                "display_name": "VBS Administrator"
            },
            {
                "catalog": "OBS",
                "display_name": "Tenant Administrator"
            },
            {
                "catalog": "OBS",
                "display_name": "Tenant Guest"
            }
        ]
    }
    ```


>![](public_sys-resources/icon-note.gif) **说明：** 
>如果用户账号开通了企业项目：
>-   当该账号配置CSS FullAccess权限时，即使给单个企业项目只配了CSS ReadOnlyAccess权限，但所有企业项目都拥有CSS FullAccess权限。
>-   如果给单个企业项目开通了CSS FullAccess权限，则该企业项目下的所有子用户都可以拥有该权限。如：企业项目default配了CSS FullAccess权限，那么子用户可以读到default企业项目下的集群，且进行读写操作。

示例2：授权用户CSS ReadOnlyAccess权限，即给用户配置CSS的只读权限。如果用户需要查看集群监控信息，则需要依赖CES的只读权限。

1.  授权用户CSS ReadOnlyAccess权限。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Action": [
                    "css:*:get*",
                    "css:*:list*",
                    "vpc:securityGroups:get",
                    "vpc:securityGroupRules:get",
                    "vpc:vpcs:list",
                    "vpc:privateIps:list",
                    "vpc:ports:get",
                    "vpc:quotas:list",
                    "vpc:subnets:get",
                    "ecs:cloudServerFlavors:get",
                    "ecs:quotas:get",
                    "evs:types:get",
                    "evs:quotas:get"              
                ],
                "Effect": "Allow"
            }
        ]
    }
    ```


1.  （可选）授权用户查看集群监控信息权限。

    ```
    {
        "Version": "1.1",
        "Statement": [
            {
                "Action": [
                    "ces:*:get*",
                    "ces:*:list*"
                ],
                "Effect": "Allow"
            }
        ]
    }
    ```


>![](public_sys-resources/icon-note.gif) **说明：** 
>如果用户账号开通了企业项目：
>-   在统一认证服务中给该账号开通了CSS ReadOnlyAccess权限，但是给某个企业项目配置了CSS FullAccess权限，那么子用户可以读到所有企业项目下的集群，但是只对开通CSS FullAccess权限下的集群进行写操作。例如，给企业项目default配置了CSS FullAccess权限，那么子用户可以读到所有企业项目下的集群，但是只对default下的集群进行写操作。
>-   在统一认证服务中给该账号开通了CSS ReadOnlyAccess权限，但是没有给单个企业项目授权，则子账户只能读取该项目下的集群，不能进行写操作。例如，给企业项目default配了CSS ReadOnlyAccess，那么子用户可以读到default企业项目下的集群，不可进行写操作。

## CSS自定义策略样例<a name="section11742221141718"></a>

示例1：授权用户创建集群。

```
{
    "Version": "1.1",
    "Statement": [
        {
            "Action": [
                "css:cluster:create",
                "vpc:securityGroups:get",
                "vpc:securityGroups:create",
                "vpc:securityGroups:delete",
                "vpc:securityGroupRules:get",
                "vpc:securityGroupRules:create",
                "vpc:securityGroupRules:delete",
                "vpc:vpcs:list",
                "vpc:privateIps:list",
                "vpc:ports:get",
                "vpc:ports:create",
                "vpc:ports:update",
                "vpc:ports:delete",
                "vpc:quotas:list",
                "vpc:subnets:get",
                "ecs:cloudServerFlavors:get",
                "ecs:serverInterfaces:use",
                "ecs:cloudServers:addNics",
                "ecs:quotas:get",
                "evs:types:get",
                "evs:quotas:get"
            ],
            "Effect": "Allow"
        }
    ]
}
```

示例2：拒绝用户删除集群。

拒绝策略需要同时配合其他策略使用，否则没有实际作用。用户被授予的策略中，一个授权项的作用如果同时存在Allow和Deny，则遵循**Deny优先原则**。

如果您给用户授予CSS Admin的系统策略，但不希望用户拥有CSS admin中定义的删除云服务器权限，您可以创建一条拒绝删除云服务的自定义策略，然后同时将CSS Admin和拒绝策略授予用户，根据Deny优先原则，则用户可以对CSS执行除了删除集群外的所有操作。拒绝策略示例如下：

```
{ 
      "Version": "1.1", 
      "Statement": [ 
            { 
		  "Effect": "Deny", 
                  "Action": [ 
                        "css:cluster:delete"
                  ] 
            } 
      ] 
}

```

示例3：多个授权项策略。

一个自定义策略中可以包含多个授权项，且除了可以包含本服务的授权项外，还可以包含其他服务的授权项，可以包含的其他服务必须跟本服务同属性，即都是项目级服务或都是全局级服务。多个授权语句策略描述如下：

```
{
    "Version": "1.1",
    "Statement": [
        {
            "Action": [
                "ecs:cloudServers:resize",
                "ecs:cloudServers:delete",
                "ecs:cloudServers:delete",
                "css:cluster:restart",
                "css:*:get*",
                "css:*:list*"
            ],
            "Effect": "Allow"
        }
    ]
}
```


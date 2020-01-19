# RBAC策略语法<a name="css_01_0073"></a>

## 策略语法<a name="section513575312247"></a>

给用户组选择策略时，单击策略下方的![](figures/zh-cn_image_0220433320.gif)，可以查看策略的详细内容，以CSS服务的“Elasticsearch Administrator“为例，说明RBAC策略语法。

**图 1**  RBAC策略设置<a name="fig1028117104910"></a>  
![](figures/RBAC策略设置.png "RBAC策略设置")

```
{
    "Version": "1.0",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "css:*:*"
            ]
        }
    ],
    "Depends": [
        {
            "catalog": "BASE",
            "display_name": "Server Administrator"
        },
        {
            "catalog": "BASE",
            "display_name": "Tenant Guest"
        }
    ]
}
```

## 参数说明<a name="section4815150185213"></a>

-   Version：策略的版本号，RBAC策略版本为“1.0”。
-   Statement：策略的授权语句，包含Action（授权项）和Effect（作用），Action和Effect结合构成用户具备的权限。
    -   Action（授权项）：操作权限，格式为：服务名:资源类型:操作

        "CSS:\*:\*"：表示对CSS的所有操作，其中CSS为服务名；“\*”为通配符，表示对所有的资源类型可以执行所有操作。

    -   Effect（作用）：定义Action中的操作权限是否允许执行。Allow：允许；Deny：拒绝。

-   Depends：策略的依赖关系，给用户组授予该策略时，需要同时勾选依赖的权限，否则该策略不会生效。
    -   catalog：依赖的策略的所属服务。
    -   display\_name：依赖的策略的名称。例如：Tenant Guest，Server Administrator



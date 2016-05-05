title: 关于DataTables的使用
date: 2015-12-23 20:34:36
tags: technology
---

DataTables是一个jQuery的表格插件。这是一个高度灵活的工具，依据的基础逐步增强，这将增加先进的互动控制，支持任何HTML表格。
在云迹项目中，表格都使用该插件，所以特此在这里总结记录一些常用用法。

## DataTables的默认配置
```
var oTable = $('#example').DataTable();
```

## DataTables的一些基础属性配置
```
"data":tableData,
"columnDefs": [ {
        "targets": 0,
        "data": null,
        "class": "text-center",
        "render": function ( data, type, full, meta ) {
          return '<span class="row-details row-details-close"></span>';
        }
    },
    {
        "targets": 1,
        "data": "VISIT_TIME"
    }
}],
"pageLength": 10,//设置每页显示多少条
"language": {//设置提示中文字
	"lengthMenu": " 每页 _MENU_ 条",
	"info": "当前第_PAGE_页，总共_PAGES_页",
	"zeroRecords": "未查询到数据",
	"emptyTable": "暂无数据",
	"infoEmpty":"未查询到数据"
},
"ordering": false,//设置是否启用排序
"lengthChange": false,//设置是否允许变换每页选择条数
"info": false //设置是否显示文字信息
```

## DataTables一些基本操作

**1、获取某一行绑定的所有值**
```
var tr = $(this).closest('tr');//获取这一行的tr对象
var row = oTable.row( tr );
dataObj = row.data();//dataObj为该行的数据对象
```

**2、展开一行详细**
详细示例内容参见：[官方API示例](http://www.datatables.net/examples/api/row_details.html "展开一行详细内容")

**3、关于排序**
```
"columnDefs": [ {
        "targets": 0,
        "data": "column1",
        "orderable": false //设置第0列不参与排序
    }
}],
"ordering" : true //启用排序
"order": [[ 0, "asc" ]] //设置默认排序：0代表列号；为空表示不设置默认排序
```

**4、自定义检索项目**
```
var searchValue = "test";
//检索第0列的值为"test"的方法
oTable.column(0).search(searchValue).draw();
```
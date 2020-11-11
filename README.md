# covert-json-to-excel

## Plugin setup

```
npm i covert-json-to-excel
```

## How to use?
数据如下:
```js
const data = [
  {
    name: "哈哈",
    age: 1,
    sex: "男",
    companyName: "公司1",
    companyAddress: {
      companyAddressZh:"公司地址中文1",
      companyAddressEn:"公司地址英文1"
    }
  },
  {
    name: "呵呵",
    age: 2,
    sex: "女",
    companyName: "公司2",
    companyAddress: {
      companyAddressZh:"公司地址中文2",
      companyAddressEn:"公司地址英文2"
    }
  },
  {
    name: "嘻嘻",
    age: 3,
    sex: "男",
    companyName: "公司3",
    companyAddress: {
      companyAddressZh:"公司地址中文3",
      companyAddressEn:"公司地址英文3"
    }
  },
  {
    name: "啦啦",
    age: 4,
    sex: "女",
    companyName: "公司4",
    companyAddress: {
      companyAddressZh:"公司地址中文4",
      companyAddressEn:"公司地址英文4"
    }
  }
];
```

1. json直接转化：

```js
import Json2excel from "custom-json2excel";
const json2excel = new Json2excel({ data });
json2excel.generate();
```

2. 自定义头部字段时的使用方式：

```js
import Json2excel from "custom-json2excel";
const keyMap = [{
  title:"姓名",
  key:"name",
},
{
  title:"地址",
  filter:function(row){
    return row.companyAddress.companyAddressZh
  }
}];
const json2excel = new Json2excel({ data, keyMap });
json2excel.generate();
```


3. 绑定回调函数的使用方式：

```js
const json2excel = new Json2excel({
  data,
  keyMap,
  onStart: () => {
    console.log("开始");
  },
  onSuccess: () => {
    console.log("成功");
  }
});
json2excel.generate();
```

## Props type

| _Prop_    | _Type_   | _Defaults_ | _Required_ | _Description_                                                      |
| :-------- | :------- | :--------- | :--------- | ------------------------------------------------------------------ |
| data      | Array    | []         | ✓          | 转化成表格初始 json 数据                                           |
| keyMap    | Array    | []         | ×          | keyMap 映射表，用于自定义表格头部名称                              |
| name      | String   | excel      | ×          | excel 表格名称                                                     |
| type      | String   | xls        | ×          | 生成的表格类型，可选值(xls、csv)                                   |
| onStart   | Function |            | ×          | 生成 Excel 前的回调函数                                            |
| onSuccess | Function |            | ×          | 生成 Excel 成功的回调函数                                          |

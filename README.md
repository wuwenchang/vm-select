![vm-select](https://img.shields.io/npm/v/vm-select.svg?style=flat) 

# vm-select 
基于 vue2.x 的下拉多选组件
![images](https://github.com/collins401/vm-select/master/docs/1550453663311.png)
## Installation
```
$ npm install vm-select --save
```

### use
```
<template>
 <vm-select :options="options" v-model="selected" multiple label="name" label-key="id"></vm-select>
</template>
<script>
import vmSelect from "vm-select"
export default {
 data () {
  return {
    options: [
      {id: '1', name: 'github'},
      {id: '2', name: 'gitlab'},
      {id: '3', name: 'gitbook'},
      {id: '4', name: 'gitalk'},
      {id: '5', name: 'gitchat'},
      {id: '6', name: 'npm'}
    ],
    selected: ['1', '3', '5']
  }
 },
 components: {
  vmSelect
 }
}
</script>
```
### vm-select props
|属性|说明|类型|默认值|
|:--|:--|:--|:--|
| value | v-model，单选时只接受 String 或 Number，多选时只接受 Array， String，Number 格式| Array | 必填 |
|options|	list 下拉值，e.g. `[1,2,3,4] `or `[{id: 1, name: 'github'},{id: 2, name: 'gitlab'}]`	|Array	|必填|
|multiple|	是否支持多选	|Boolean	|false|
|disabled|	是否禁用|	Boolean|	false
|search|	是否 支持搜索|	Boolean|	false
|label|	数据格式为[{}]数组对象时，label 为必填显示值，e.g.: `label="name"`|	String|	空
|labelKey|	数据格式为[{}]labelKey 为必填显示值，e.g.: `label-key="id"`|	String|	空
|customLabel|	自定义显示 label 值| Function|	空
|customDisabled| 下拉选项禁止状态| Function|	空
|strings|	文本默认值|	 Object|	空

### vm-select events
|事件名|说明|返回值|
|:--|:--|:--|
|on-change|选中的Option变化时触发，默认返回 value|当前选中项|

简单的 vue 组件，根据业务使用提取，欢迎大家 fork ([Demo][1])。
======================

## DatePicker
### Props
```js
{
    format: 'yyyy-MM-dd',
    min: '2010-01-01',
    max: '2030-01-01',
    range: false,
    weekStart: 0,
    useTools: false
}
```

#### Instructions
| Prop Name | Type | Description |
|---|---|
| format | String | 格式化日期格式字符串，支持 `yyyy-MM-dd` 或者 `yyyy/MM/dd` 等可转换为日期的格式字符串。默认 `yyyy-MM-dd` |
| min | String | 最大可选择的日期，支持可转换为日期的字符串。默认 `2010-01-01` |
| max | String | 最大可选择的日期，支持可转换为日期的字符串。默认 `2030-01-01` |
| range | Boolean | 日期选择器区间选择类型，默认为空或不传，设置为单选。可传入 `common` 或 `week` 变为普通区间选择器或周选择器 |
| weekStart | Number | 当 `range='week'` 周选择器时，可以设置周起始序号。默认为 `0`，从周日开始计算一周，比如：从周五计算一周开始，`:week-start='5'` |
| useTools | Boolean | 是否使用按钮触发选择 |

#### Return Value After Format

说明：返回值为根据 `format` 格式化后的选择值进行返回。

### Demo

```html
  <date-picker v-model="dateSingle" @input="dateSingleChange" :format="'yyyy/MM/dd'"></date-picker>
  <date-picker range="common" v-model="dateCommon" @input="dateCommonChange"></date-picker>
  <date-picker range="week" v-model="dateWeek" @input="dateWeekChange"></date-picker>
  <date-picker range="week" :week-start="5" v-model="dateWeek" @input="dateWeekChange"></date-picker>
```

```js
  // vue data bind
  data() {
    return {
        dateSingle: '2018/01/01',
        dateCommon: ['2018-01-01', '2018-01-31'],
        dateWeek: ['2018-01-01']
    }
  }
```

## DropSelector

### Props

```js
{
  data: ['北京', '上海'],
  textKeyName: 'text',
  textHolder: '请从列表中选择',
  canSearch: false,
  keywordHolder: '输入关键字搜索',
  filterKeys: 'pinyin,suoxie',
  multi: false,
  canSelectAll: true,
  defaultSelectAll: false,
  enumSelect: false
}
```

#### Instructions
| Prop Name | Type | Description |
|---|---|
| data | Array | 选择器选项列表，数组每项可以为 `String` 或 `Object` ，最终返回值为 `Object` |
| textKeyName | String | 设置选择器显示文字的 `key` 名称，默认为 `text` |
| textHolder | String | 设置默认提示文字，默认 `'请选择'` |
| canSearch | Boolean | 是否可以进行搜索 |
| keywordHolder | String | 搜索框提示文字，默认 `'输入关键字搜索'` |
| filterKeys | String | 搜索过滤 `key` 字符串，以 `,` 分割，比如：`'pinyin|suoxie'` |
| multi | String | 是否可以多选 |
| canSelectAll | Boolean | 是否包含全选项 |
| defaultSelectAll | Boolean | 是否默认全选 |
| enumSelect | Boolean | 多选时，是否枚举已选择项 |

#### Return Value Is `Object`

选择完成后会触发组件 `change` 事件，并返回选择项 `Object` 。

说明：如果 `data` 数组项目为 `String` 类型，返回值为 {text: `String`, vmIndex: `Number`}。如果数组项为 `Object` 进行原对象返回，并添加 `vmIndex` 属性。

### Demo
```html
<drop-selector :data="data" text-key-name="city" @change="singleChange"></drop-selector>
<drop-selector :data="dataSearch" text-key-name="city" @change="singleChange" can-search filter-keys="suoxie,pinyin"></drop-selector>
<drop-selector :data="dataMulti" text-key-name="city" @change="multiChange" multi default-select-all></drop-selector>
<drop-selector :data="dataMultiSearch" text-key-name="city" @change="multiChange" multi can-search enum-select></drop-selector>
```


  [1]: http://yangfan86.gitee.io/datepickerdemo/
# Table 表格

表格常用于展示同类结构下的多种数据，易于组织、对比和分析等，并可对数据进行搜索、筛选、排序等操作。一般包括表头、数据行和表尾三部分。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/table)。

> 该组件于 1.14.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-table": "tdesign-miniprogram/table/table"
}
```



## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/5A8ZsBmV8r8L)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 组件类型

#### 基础表格

```wxml
<t-table
  row-key="id"
  columns="{{columns}}"
  data="{{data}}"
  show-header="{{true}}"
  cell-empty-content="-"
  bind:row-click="handleRowClick"
  bind:cell-click="handleCellClick"
/>

```
```js
import SkylineBehavior from '@behaviors/skyline.js';

Component({
  behaviors: [SkylineBehavior],
  data: {
    columns: [
      { colKey: 'applicant', title: '标题', ellipsis: true },
      { colKey: 'status', title: '标题', ellipsis: true },
      { colKey: 'channel', title: '标题', ellipsis: true },
      { colKey: 'detail.email', title: '标题', ellipsis: true },
    ],
    data: [],
  },
  lifetimes: {
    attached() {
      const data = [];
      const total = 10;
      for (let i = 0; i < total; i += 1) {
        data.push({
          id: i + 1,
          index: i + 1,
          applicant: ['内容', '内容', '内容'][i % 3],
          status: ['内容', '内容', '内容'][i % 3],
          channel: ['内容', '内容', '内容'][i % 3],
          detail: {
            email: ['内容', '内容', '内容'][i % 3],
          },
        });
      }
      this.setData({ data });
    },
  },
  methods: {
    handleRowClick(e) {
      console.log('[row-click]', e.detail);
    },
    handleCellClick(e) {
      console.log('[cell-click]', e.detail);
    },
  },
});

```
```wxss
/* base demo 无额外样式 */

```
```json
{
  "component": true,
  "usingComponents": {
    "t-table": "tdesign-miniprogram/table/table"
  }
}

```

#### 横向平铺可滚动表格

```wxml
<t-table
  row-key="id"
  columns="{{columns}}"
  data="{{data}}"
  table-content-width="720px"
  show-header="{{true}}"
  cell-empty-content="-"
  bind:row-click="handleRowClick"
  bind:cell-click="handleCellClick"
/>

```
```js
import SkylineBehavior from '@behaviors/skyline.js';

Component({
  behaviors: [SkylineBehavior],
  data: {
    columns: [
      { colKey: 'applicant', title: '标题', width: 180 },
      { colKey: 'status', title: '标题', width: 180 },
      { colKey: 'channel', title: '标题', width: 180 },
      { colKey: 'detail.email', title: '标题', width: 180 },
    ],
    data: [],
  },
  lifetimes: {
    attached() {
      const data = [];
      const total = 5;
      for (let i = 0; i < total; i += 1) {
        data.push({
          id: i + 1,
          index: i + 1,
          applicant: ['横向平铺内容不省略', '内容', '内容'][i % 3],
          status: ['横向平铺内容不省略', '内容', '内容'][i % 3],
          channel: ['横向平铺内容不省略', '内容', '内容'][i % 3],
          detail: {
            email: ['横向平铺内容不省略', '内容', '内容'][i % 3],
          },
        });
      }
      this.setData({ data });
    },
  },
  methods: {
    handleRowClick(e) {
      console.log('[row-click]', e.detail);
    },
    handleCellClick(e) {
      console.log('[cell-click]', e.detail);
    },
  },
});

```
```wxss
/* scroll demo 无额外样式 */

```
```json
{
  "component": true,
  "usingComponents": {
    "t-table": "tdesign-miniprogram/table/table"
  }
}

```

#### 带斑马纹表格样式

```wxml
<t-table
  row-key="id"
  fixed-rows="{{[1, 2]}}"
  columns="{{columns}}"
  data="{{data}}"
  stripe="{{true}}"
  max-height="{{400}}"
  show-header="{{true}}"
  cell-empty-content="-"
  bind:row-click="handleRowClick"
  bind:cell-click="handleCellClick"
/>

```
```js
import SkylineBehavior from '@behaviors/skyline.js';

Component({
  behaviors: [SkylineBehavior],
  data: {
    columns: [
      { colKey: 'applicant', title: '标题' },
      { colKey: 'status', title: '标题' },
      { colKey: 'channel', title: '标题' },
      { colKey: 'detail.email', title: '标题', ellipsis: true },
    ],
    data: [],
  },
  lifetimes: {
    attached() {
      const data = [];
      const total = 20;
      for (let i = 0; i < total; i += 1) {
        const content = ['内容', '内容', '内容', '内容', '内容'][i % 5];
        data.push({
          id: i + 1,
          index: i + 1,
          applicant: content,
          status: content,
          channel: content,
          detail: {
            email: content,
          },
        });
      }
      this.setData({ data });
    },
  },
  methods: {
    handleRowClick(e) {
      console.log('[row-click]', e.detail);
    },
    handleCellClick(e) {
      console.log('[cell-click]', e.detail);
    },
  },
});

```
```wxss
/* stripe demo 无额外样式 */

```
```json
{
  "component": true,
  "usingComponents": {
    "t-table": "tdesign-miniprogram/table/table"
  }
}

```

#### 带边框表格样式

```wxml
<t-table
  row-key="id"
  columns="{{columns}}"
  data="{{data}}"
  bordered="{{true}}"
  show-header="{{true}}"
  cell-empty-content="-"
  bind:row-click="handleRowClick"
  bind:cell-click="handleCellClick"
/>

```
```js
import SkylineBehavior from '@behaviors/skyline.js';

Component({
  behaviors: [SkylineBehavior],
  data: {
    columns: [
      { colKey: 'applicant', title: '标题', ellipsis: true },
      { colKey: 'status', title: '标题', ellipsis: true },
      { colKey: 'channel', title: '标题', ellipsis: true },
      { colKey: 'detail.email', title: '标题', ellipsis: true },
    ],
    data: [],
  },
  lifetimes: {
    attached() {
      const data = [];
      const total = 10;
      for (let i = 0; i < total; i += 1) {
        data.push({
          id: i + 1,
          index: i + 1,
          applicant: ['内容', '内容', '内容'][i % 3],
          status: ['内容', '内容', '内容'][i % 3],
          channel: ['内容', '内容', '内容'][i % 3],
          detail: {
            email: ['内容', '内容', '内容内容内容'][i % 3],
          },
        });
      }
      this.setData({ data });
    },
  },
  methods: {
    handleRowClick(e) {
      console.log('[row-click]', e.detail);
    },
    handleCellClick(e) {
      console.log('[cell-click]', e.detail);
    },
  },
});

```
```wxss
/* bordered demo 无额外样式 */

```
```json
{
  "component": true,
  "usingComponents": {
    "t-table": "tdesign-miniprogram/table/table"
  }
}

```

#### 带合并单元格的表格

```wxml
<t-table
  row-key="id"
  columns="{{columns}}"
  data="{{data}}"
  bordered="{{true}}"
  rowspan-and-colspan="{{rowspanAndColspan}}"
  cell-empty-content="-"
/>

```
```js
import SkylineBehavior from '@behaviors/skyline.js';

Component({
  behaviors: [SkylineBehavior],
  data: {
    columns: [
      { colKey: 'index', title: '序号', width: 60 },
      { colKey: 'name', title: '姓名' },
      { colKey: 'department', title: '部门' },
      { colKey: 'status', title: '状态' },
    ],
    data: [
      { id: 1, index: 1, name: '张三', department: '研发部', status: '在职' },
      { id: 2, index: 2, name: '李四', department: '研发部', status: '在职' },
      { id: 3, index: 3, name: '王五', department: '设计部', status: '离职' },
      { id: 4, index: 4, name: '赵六', department: '产品部', status: '在职' },
    ],
    // 注意：小程序中 rowspanAndColspan 需要通过函数传递
    // 合并规则：
    // 1. 第1-2行的"部门"列合并（rowspan）
    // 2. 第3行的"姓名"和"部门"列合并（colspan）
    rowspanAndColspan: null,
  },
  lifetimes: {
    attached() {
      this.setData({
        rowspanAndColspan: ({ rowIndex, colIndex }) => {
          // 第1行第2列（部门）：向下合并2行
          if (rowIndex === 0 && colIndex === 2) {
            return { rowspan: 2, colspan: 1 };
          }
          // 第2行第2列（部门）：被上面合并，不渲染
          if (rowIndex === 1 && colIndex === 2) {
            return { rowspan: 0, colspan: 0 };
          }
          // 第3行第1列（姓名）：向右合并2列
          if (rowIndex === 2 && colIndex === 1) {
            return { rowspan: 1, colspan: 2 };
          }
          // 第3行第2列（部门）：被左边合并，不渲染
          if (rowIndex === 2 && colIndex === 2) {
            return { rowspan: 0, colspan: 0 };
          }
          return {};
        },
      });
    },
  },
});

```
```wxss
/* rowspan-colspan demo 无额外样式 */

```
```json
{
  "component": true,
  "usingComponents": {
    "t-table": "tdesign-miniprogram/table/table"
  }
}

```


## API

### BaseTable Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
bordered | Boolean | false | 是否显示表格边框 | N
cell-empty-content | String | - | 单元格数据为空时呈现的内容 | N
columns | Array | [] | 列配置，泛型 T 指表格数据类型。TS 类型：`Array<BaseTableCol<T>>` | N
data | Array | [] | 数据源，泛型 T 指表格数据类型。TS 类型：`Array<T>` | N
empty | String | '' | 空表格呈现样式，支持全局配置 `GlobalConfigProvider` | N
fixed-rows | Array | - | 固定行（冻结行），示例：[M, N]，表示冻结表头 M 行和表尾 N 行。M 和 N 值为 0 时，表示不冻结行。TS 类型：`Array<number>` | N
footer-summary | String | - | 表尾总结行 | N
height | String / Number | - | 表格高度，超出后会出现滚动条。示例：100,  '30%',  '300'。值为数字类型，会自动加上单位 px。如果不是绝对固定表格高度，建议使用 `maxHeight` | N
loading | Boolean | undefined | 加载中状态。值为 `true` 会显示默认加载中样式，可以通过 Function 和 插槽 自定义加载状态呈现内容和样式。值为 `false` 则会取消加载状态 | N
loading-props | Object | - | 透传加载组件全部属性。TS 类型：`Partial<LoadingProps>`，[Loading API Documents](loading.md#api)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/table/type.ts) | N
max-height | String / Number | - | 表格最大高度，超出后会出现滚动条。示例：100, '30%', '300'。值为数字类型，会自动加上单位 px | N
row-key | String | 'id' | 必需。唯一标识一行数据的字段名，来源于 `data` 中的字段。如果是字段嵌套多层，可以设置形如 `item.a.id` 的方法 | Y
rowspan-and-colspan | Function | - | 用于自定义合并单元格，泛型 T 指表格数据类型。示例：`({ row, col, rowIndex, colIndex }) => { rowspan: 2, colspan: 3 }`。TS 类型：`TableRowspanAndColspanFunc<T>` `type TableRowspanAndColspanFunc<T extends TableRowData = TableRowData> = (params: BaseTableCellParams<T>) => RowspanColspan` `interface RowspanColspan { colspan?: number; rowspan?: number }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/table/type.ts) | N
show-header | Boolean | true | 是否显示表头 | N
stripe | Boolean | false | 是否显示斑马纹 | N
table-content-width | String | - | 表格内容的总宽度，注意不是表格可见宽度。主要应用于 `table-layout: auto` 模式下的固定列显示。`tableContentWidth` 内容宽度的值必须大于表格可见宽度 | N
table-layout | String | fixed | 表格布局方式。可选项：auto/fixed | N
vertical-align | String | middle | 行内容上下方向对齐。可选项：top/middle/bottom | N

### BaseTable Events

名称 | 参数 | 描述
-- | -- | --
cell-click | `(detail: BaseTableCellEventContext<T>)` | 单元格点击时触发。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/table/type.ts)。<br/>`interface BaseTableCellEventContext<T extends TableRowData = TableRowData> { row: T; col: BaseTableCol<T>; rowIndex: number; colIndex: number;}`<br/>
row-click | `(detail: RowEventContext<T>)` | 行点击时触发，泛型 T 指表格数据类型。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/table/type.ts)。<br/>`interface RowEventContext<T extends TableRowData = TableRowData> { row: T; index: number;}`<br/>

### BaseTable Slots

名称 | 描述
-- | --
cell-empty-content | 自定义 `cell-empty-content` 显示内容
empty | 自定义 `empty` 显示内容
footer-summary | 自定义 `footer-summary` 显示内容
loading | 自定义 `loading` 显示内容

### BaseTable External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-footer | 表尾总结行样式类
t-class-header | 表头行样式类

### BaseTableCol

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
align | String | left | 列横向对齐方式。可选项：left/right/center | N
cell | String / Function | - | 自定义单元格渲染。默认使用 `colKey` 的值作为自定义当前列的插槽名称。<br/>如果 `cell` 值类型为 Function 表示以函数形式渲染单元格。优先级高于 `render`。泛型 T 指表格数据类型。TS 类型：`string \| ((params: BaseTableCellParams<T>) => string)` `interface BaseTableCellParams<T extends TableRowData = TableRowData> { row: T; rowIndex: number; col: BaseTableCol<T>; colIndex: number }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/table/type.ts) | N
class-name | String / Object / Array / Function | - | 列类名，值类型是 Function 使用返回值作为列类名；值类型不为 Function 时，值用于整列类名（含表头）。泛型 T 指表格数据类型。TS 类型：`TableColumnClassName<T> \| TableColumnClassName<T>[]` `type TableColumnClassName<T extends TableRowData = TableRowData> = ClassName \| ((context: CellData<T>) => ClassName)` `interface CellData<T extends TableRowData = TableRowData> extends BaseTableCellParams<T> { type: 'th' \| 'td' }`。[通用类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/common/common.ts)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/table/type.ts) | N
col-key | String | - | 渲染列所需字段，值为 `serial-number` 表示当前列为「序号」列 | N
fixed | String | left | 固定列显示位置。可选项：left/right | N
min-width | String / Number | - | 透传 CSS 属性 `min-width` 到 `<col>` 元素。⚠️ 仅少部分浏览器支持，如：使用 [TablesNG](https://docs.google.com/document/d/16PFD1GtMI9Zgwu0jtPaKZJ75Q2wyZ9EZnVbBacOfiNA/preview) 渲染的 Chrome 浏览器支持 `minWidth` | N
width | String / Number | - | 列宽，可以作为最小宽度使用。当列宽总和小于 `table` 元素时，浏览器根据宽度设置情况自动分配宽度；当列宽总和大于 `table` 元素，表现为定宽。可以同时调整 `table` 元素的宽度来达到自己想要的效果 | N

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-table-body-text-color | @text-color-primary | -
--td-table-border-color | @component-border | -
--td-table-fixed-cell-border-color | @component-border | -
--td-table-font-size | @font-body-medium | -
--td-table-header-bg-color | @bg-color-container | -
--td-table-header-text-color | @text-color-placeholder | -
--td-table-loading-bg-color | rgba(255, 255, 255, 0.55) | -
--td-table-row-height | 82rpx | -
--td-table-stripe-bg-color | @bg-color-secondarycontainer | -
--td-table-td-padding | @spacer @spacer-1 | -
--td-table-th-padding | @spacer @spacer-1 | -

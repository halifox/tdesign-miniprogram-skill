# DropdownMenu 下拉菜单

菜单呈现数个并列的选项类目，用于整个页面的内容筛选，由菜单面板和菜单选项组成。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/dropdown-menu)。

> 该组件于 0.8.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

### 引入组件

在 `app.json` 或 `page.json` 中引入组件：

```json
"usingComponents": {
  "t-dropdown-menu": "tdesign-miniprogram/dropdown-menu/dropdown-menu",
  "t-dropdown-item": "tdesign-miniprogram/dropdown-item/dropdown-item"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/ncvL0Mmd8e5n)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 单选下拉菜单

```wxml
<t-dropdown-menu>
  <t-dropdown-item options="{{product.options}}" placement="right" value="{{product.value}}" bindchange="onChange" />
  <t-dropdown-item options="{{sorter.options}}" placement="right" default-value="{{sorter.value}}" />
</t-dropdown-menu>

```
```js
Component({
  data: {
    product: {
      value: 'all',
      options: [
        {
          value: 'all',
          label: '全部产品',
        },
        {
          value: 'new',
          label: '最新产品',
        },
        {
          value: 'hot',
          label: '最火产品',
        },
        {
          value: 'disabled',
          label: '禁用选项',
          disabled: true,
        },
      ],
    },
    sorter: {
      value: 'default',
      options: [
        {
          value: 'default',
          label: '默认排序',
        },
        {
          value: 'price',
          label: '价格从高到低',
        },
      ],
    },
  },
  methods: {
    onChange(e) {
      this.setData({
        'product.value': e.detail.value,
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-dropdown-menu": "tdesign-miniprogram/dropdown-menu/dropdown-menu",
    "t-dropdown-item": "tdesign-miniprogram/dropdown-item/dropdown-item"
  }
}

```

### 多列下拉菜单

```wxml
<t-dropdown-menu>
  <t-dropdown-item
    label="单列多选"
    keepLabelActive
    options="{{multipleSelect.options}}"
    value="{{multipleSelect.value}}"
    bindchange="handleMultipleSelect"
    multiple
  />
  <t-dropdown-item
    label="双列多选"
    optionsColumns="2"
    options="{{doubleColumnsOptions}}"
    defaultValue="{{['option_1', 'option_2']}}"
    multiple
  />
  <t-dropdown-item
    label="三列多选"
    keepLabelActive
    optionsColumns="3"
    options="{{tripleColumnsOptions}}"
    defaultValue="{{[]}}"
    multiple
  />
</t-dropdown-menu>

```
```js
const chineseNumber = '一二三四五六七八九十'.split('');

const singleSelectOptions = new Array(8).fill(null).map((_, i) => ({
  label: `选项${chineseNumber[i]}`,
  value: `option_${i + 1}`,
  disabled: false,
}));

singleSelectOptions.push({
  label: '禁用选项',
  value: 'disabled',
  disabled: true,
});

const doubleColumnsOptions = [
  ...singleSelectOptions,
  {
    label: '禁用选项',
    value: 'disabled',
    disabled: true,
  },
];

const tripleColumnsOptions = [
  ...doubleColumnsOptions,
  {
    label: '禁用选项',
    value: 'disabled',
    disabled: true,
  },
];

tripleColumnsOptions.splice(8, 0, {
  label: `选项${chineseNumber[8]}`,
  value: `option_${9}`,
  disabled: false,
});

Component({
  data: {
    multipleSelect: {
      value: ['option_1'],
      options: singleSelectOptions,
    },
    doubleColumnsOptions,
    tripleColumnsOptions,
  },

  methods: {
    handleMultipleSelect(e) {
      this.setData({
        'multipleSelect.value': e.detail.value,
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-dropdown-menu": "tdesign-miniprogram/dropdown-menu/dropdown-menu",
    "t-dropdown-item": "tdesign-miniprogram/dropdown-item/dropdown-item"
  }
}

```

### 树形下拉菜单

```wxml
<t-dropdown-menu>
  <t-dropdown-item
    label="树形双列"
    optionsLayout="tree"
    options="{{doubleColumnsTree.options}}"
    value="{{doubleColumnsTree.value}}"
    bindchange="handleTreeSelect"
  />
  <t-dropdown-item
    label="选项最多八字树形三列"
    optionsLayout="tree"
    options="{{tripleColumnsTree.options}}"
    defaultValue="{{tripleColumnsTree.value}}"
    multiple
  />
</t-dropdown-menu>

```
```js
const chineseNumber = '一二三四五六七八九十'.split('');

const generateTree = function (deep = 0, count = 10, prefix) {
  const ans = [];

  for (let i = 0; i < count; i += 1) {
    const value = prefix ? `${prefix}-${i}` : `${i}`;
    const rect = {
      label: `选项${chineseNumber[i]}`,
      value,
    };

    if (deep > 0) {
      rect.options = generateTree(deep - 1, 10, value);
    }
    ans.push(rect);
  }

  return ans;
};

Component({
  data: {
    doubleColumnsTree: {
      options: generateTree(1),
      value: ['0', '0-0'],
    },
    tripleColumnsTree: {
      options: generateTree(2),
      value: ['0', '0-0', ['0-0-0', '0-0-1']],
    },
  },

  methods: {
    handleTreeSelect(e) {
      this.setData({
        'doubleColumnsTree.value': e.detail.value,
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-dropdown-menu": "tdesign-miniprogram/dropdown-menu/dropdown-menu",
    "t-dropdown-item": "tdesign-miniprogram/dropdown-item/dropdown-item"
  }
}

```

## API

### DropdownMenu Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
arrow-icon | String / Object | 'caret-down-small' | 自定义箭头图标 | N
close-on-click-overlay | Boolean | true | 是否在点击遮罩层后关闭菜单 | N
duration | String / Number | 200 | 动画时长 | N
show-overlay | Boolean | true | 是否显示遮罩层 | N
z-index | Number | - | 菜单栏 z-index 层级，默认为 11600 | N

### DropdownMenu Events

名称 | 参数 | 描述
-- | -- | --
close | \- | 菜单关闭时触发
open | \- | 菜单展开时触发

### DropdownMenu Slots

名称 | 描述
-- | --
\- | 默认插槽，自定义内容区域内容

### DropdownMenu External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-icon | 图标样式类
t-class-item | 选项样式类
t-class-label | 标签样式类


### DropdownItem Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
disabled | Boolean | false | 是否禁用操作项 | N
keep-label-active | Boolean | false | `1.18.0`。是否保持标题高亮（含菜单收起态），仅多选场景生效 | N
keys | Object | - | 用来定义 value / label / disabled 在 `options` 中对应的字段别名。TS 类型：`KeysType`。[通用类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/common/common.ts) | N
label | String | - | 标题 | N
multiple | Boolean | false | 是否多选 | N
options | Array | [] | 选项数据。TS 类型：`Array<DropdownOption>` `interface DropdownOption { label: string; disabled?: boolean; value: DropdownValue; }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/dropdown-item/type.ts) | N
options-columns | String / Number | 1 | 选项分栏（1-3） | N
options-layout | String | columns | 已废弃。选项排列；不再支持 tree 布局，可与 treeSelect 配合使用 | N
placement | String | left | 复选框和内容相对位置，仅单选菜单栏有效。可选项：left/right | N
value | String / Number / Array | undefined | 选中值。TS 类型：`DropdownValue ` `type DropdownValue = string \| number \| Array<DropdownValue>;`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/dropdown-item/type.ts) | N
default-value | String / Number / Array | undefined | 选中值。非受控属性。TS 类型：`DropdownValue ` `type DropdownValue = string \| number \| Array<DropdownValue>;`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/dropdown-item/type.ts) | N

### DropdownItem Events

名称 | 参数 | 描述
-- | -- | --
change | `(value: DropdownValue)` | 值改变时触发
close | \- | 关闭时触发
closed | \- | 关闭且动画结束后触发
confirm | `(value: DropdownValue)` | 点击确认时触发
open | \- | 打开时触发
opened | \- | 打开且动画结束后触发
reset | \- | 点击重置时触发

### DropdownItem Slots

名称 | 描述
-- | --
\- | 默认插槽，自定义内容区域内容
footer | 底部

### DropdownItem External Classes

类名 | 描述
-- | --
t-class | 根节点样式类
t-class-column | 菜单列样式类
t-class-column-item | 菜单列选项样式类
t-class-column-item-label | 菜单列选项标签样式类
t-class-content | 内容样式类
t-class-footer | 底部样式类

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-dropdown-menu-active-color | @brand-color | -
--td-dropdown-menu-bg-color | @bg-color-container | -
--td-dropdown-menu-border-width | 1px | -
--td-dropdown-menu-color | @text-color-primary | -
--td-dropdown-menu-disabled-color | @text-color-disabled | -
--td-dropdown-menu-font-size | @font-size-base | -
--td-dropdown-menu-height | 96rpx | -
--td-dropdown-menu-icon-size | 40rpx | -
--td-dropdown-body-max-height | 560rpx | -

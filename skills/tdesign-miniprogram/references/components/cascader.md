# Cascader 级联选择器

级联选择器适用于有清晰层级结构的数据集合，用户可以通过逐级查看并选择。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/cascader)。

> 该组件于 0.23.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-cascader": "tdesign-miniprogram/cascader/cascader"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/WOWeTNmJ8X5B)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 基础用法

```wxml
<t-cell title="地址" note="{{note}}" bind:click="showCascader" arrow />

<t-cascader
  visible="{{visible}}"
  value="{{value}}"
  options="{{options}}"
  title="请选择地址"
  bind:change="onChange"
  bind:pick="onPick"
/>

```
```js
const data = {
  areaList: [
    {
      label: '北京市',
      value: '110000',
      children: [
        {
          value: '110100',
          label: '北京市',
          children: [
            { value: '110101', label: '东城区' },
            { value: '110102', label: '西城区' },
            { value: '110105', label: '朝阳区' },
            { value: '110106', label: '丰台区' },
            { value: '110107', label: '石景山区' },
            { value: '110108', label: '海淀区' },
            { value: '110109', label: '门头沟区' },
            { value: '110111', label: '房山区' },
            { value: '110112', label: '通州区' },
            { value: '110113', label: '顺义区' },
            { value: '110114', label: '昌平区' },
            { value: '110115', label: '大兴区' },
            { value: '110116', label: '怀柔区' },
            { value: '110117', label: '平谷区' },
            { value: '110118', label: '密云区' },
            { value: '110119', label: '延庆区' },
          ],
        },
      ],
    },
    {
      label: '天津市',
      value: '120000',
      children: [
        {
          value: '120100',
          label: '天津市',
          children: [
            { value: '120101', label: '和平区' },
            { value: '120102', label: '河东区' },
            { value: '120103', label: '河西区' },
            { value: '120104', label: '南开区' },
            { value: '120105', label: '河北区' },
            { value: '120106', label: '红桥区' },
            { value: '120110', label: '东丽区' },
            { value: '120111', label: '西青区' },
            { value: '120112', label: '津南区' },
            { value: '120113', label: '北辰区' },
            { value: '120114', label: '武清区' },
            { value: '120115', label: '宝坻区' },
            { value: '120116', label: '滨海新区' },
            { value: '120117', label: '宁河区' },
            { value: '120118', label: '静海区' },
            { value: '120119', label: '蓟州区' },
          ],
        },
      ],
    },
  ],
};

Component({
  data: {
    options: data.areaList,
    note: '请选择地址',
    visible: false,
    value: '',
  },
  methods: {
    showCascader() {
      this.setData({ visible: true });
    },
    onPick(e) {
      console.log(e.detail);
    },
    onChange(e) {
      const { selectedOptions, value } = e.detail;

      this.setData({
        value,
        note: selectedOptions.map((item) => item.label).join('/'),
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-cascader": "tdesign-miniprogram/cascader/cascader"
  }
}

```

### 选项卡风格

```wxml
<t-cell title="地址" note="{{note}}" bind:click="showCascader" arrow></t-cell>

<t-cascader
  visible="{{visible}}"
  theme="tab"
  options="{{options}}"
  title="请选择地址"
  bind:change="onChange"
></t-cascader>

```
```js
const data = {
  areaList: [
    {
      label: '北京市',
      value: '110000',
      children: [
        {
          value: '110100',
          label: '北京市',
          children: [
            { value: '110101', label: '东城区' },
            { value: '110102', label: '西城区' },
            { value: '110105', label: '朝阳区' },
            { value: '110106', label: '丰台区' },
            { value: '110107', label: '石景山区' },
            { value: '110108', label: '海淀区' },
            { value: '110109', label: '门头沟区' },
            { value: '110111', label: '房山区' },
            { value: '110112', label: '通州区' },
            { value: '110113', label: '顺义区' },
            { value: '110114', label: '昌平区' },
            { value: '110115', label: '大兴区' },
            { value: '110116', label: '怀柔区' },
            { value: '110117', label: '平谷区' },
            { value: '110118', label: '密云区' },
            { value: '110119', label: '延庆区' },
          ],
        },
      ],
    },
    {
      label: '天津市',
      value: '120000',
      children: [
        {
          value: '120100',
          label: '天津市',
          children: [
            { value: '120101', label: '和平区' },
            { value: '120102', label: '河东区' },
            { value: '120103', label: '河西区' },
            { value: '120104', label: '南开区' },
            { value: '120105', label: '河北区' },
            { value: '120106', label: '红桥区' },
            { value: '120110', label: '东丽区' },
            { value: '120111', label: '西青区' },
            { value: '120112', label: '津南区' },
            { value: '120113', label: '北辰区' },
            { value: '120114', label: '武清区' },
            { value: '120115', label: '宝坻区' },
            { value: '120116', label: '滨海新区' },
            { value: '120117', label: '宁河区' },
            { value: '120118', label: '静海区' },
            { value: '120119', label: '蓟州区' },
          ],
        },
      ],
    },
  ],
};

Component({
  data: {
    options: data.areaList,
    note: '请选择地址',
    visible: false,
  },
  methods: {
    showCascader() {
      this.setData({ visible: true });
    },
    onChange(e) {
      const { selectedOptions } = e.detail;

      this.setData({
        note: selectedOptions.map((item) => item.label).join('/'),
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-cascader": "tdesign-miniprogram/cascader/cascader"
  }
}

```

### 进阶

#### 带初始值

```wxml
<t-cell title="地址" note="{{note}}" bind:click="showCascader" arrow></t-cell>

<t-cascader
  visible="{{visible}}"
  value="120119"
  options="{{options}}"
  title="请选择地址"
  bind:change="onChange"
></t-cascader>

```
```js
const data = {
  areaList: [
    {
      label: '北京市',
      value: '110000',
      children: [
        {
          value: '110100',
          label: '北京市',
          children: [
            { value: '110101', label: '东城区' },
            { value: '110102', label: '西城区' },
            { value: '110105', label: '朝阳区' },
            { value: '110106', label: '丰台区' },
            { value: '110107', label: '石景山区' },
            { value: '110108', label: '海淀区' },
            { value: '110109', label: '门头沟区' },
            { value: '110111', label: '房山区' },
            { value: '110112', label: '通州区' },
            { value: '110113', label: '顺义区' },
            { value: '110114', label: '昌平区' },
            { value: '110115', label: '大兴区' },
            { value: '110116', label: '怀柔区' },
            { value: '110117', label: '平谷区' },
            { value: '110118', label: '密云区' },
            { value: '110119', label: '延庆区' },
          ],
        },
      ],
    },
    {
      label: '天津市',
      value: '120000',
      children: [
        {
          value: '120100',
          label: '天津市',
          children: [
            { value: '120101', label: '和平区' },
            { value: '120102', label: '河东区' },
            { value: '120103', label: '河西区' },
            { value: '120104', label: '南开区' },
            { value: '120105', label: '河北区' },
            { value: '120106', label: '红桥区' },
            { value: '120110', label: '东丽区' },
            { value: '120111', label: '西青区' },
            { value: '120112', label: '津南区' },
            { value: '120113', label: '北辰区' },
            { value: '120114', label: '武清区' },
            { value: '120115', label: '宝坻区' },
            { value: '120116', label: '滨海新区' },
            { value: '120117', label: '宁河区' },
            { value: '120118', label: '静海区' },
            { value: '120119', label: '蓟州区' },
          ],
        },
      ],
    },
  ],
};

Component({
  data: {
    options: data.areaList,
    note: '请选择地址',
    visible: false,
  },
  methods: {
    showCascader() {
      this.setData({ visible: true });
    },
    onChange(e) {
      const { selectedOptions } = e.detail;

      this.setData({
        note: selectedOptions.map((item) => item.label).join('/'),
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-cascader": "tdesign-miniprogram/cascader/cascader"
  }
}

```

#### 自定义 keys

```wxml
<t-cell title="地址" note="{{note}}" bind:click="showCascader" arrow></t-cell>

<t-cascader
  class="demo"
  visible="{{visible}}"
  keys="{{keys}}"
  options="{{options}}"
  title="请选择地址"
  placeholder="未选中时的提示文案"
  bind:change="onChange"
></t-cascader>

```
```js
const data = {
  areaList: [
    {
      name: '北京市',
      id: '110000',
      sub: [
        {
          id: '110100',
          name: '北京市',
          sub: [
            { id: '110101', name: '东城区' },
            { id: '110102', name: '西城区' },
            { id: '110105', name: '朝阳区' },
            { id: '110106', name: '丰台区' },
            { id: '110107', name: '石景山区' },
            { id: '110108', name: '海淀区' },
            { id: '110109', name: '门头沟区' },
            { id: '110111', name: '房山区' },
            { id: '110112', name: '通州区' },
            { id: '110113', name: '顺义区' },
            { id: '110114', name: '昌平区' },
            { id: '110115', name: '大兴区' },
            { id: '110116', name: '怀柔区' },
            { id: '110117', name: '平谷区' },
            { id: '110118', name: '密云区' },
            { id: '110119', name: '延庆区' },
          ],
        },
      ],
    },
    {
      name: '天津市',
      id: '120000',
      sub: [
        {
          id: '120100',
          name: '天津市',
          sub: [
            { id: '120101', name: '和平区' },
            { id: '120102', name: '河东区' },
            { id: '120103', name: '河西区' },
            { id: '120104', name: '南开区' },
            { id: '120105', name: '河北区' },
            { id: '120106', name: '红桥区' },
            { id: '120110', name: '东丽区' },
            { id: '120111', name: '西青区' },
            { id: '120112', name: '津南区' },
            { id: '120113', name: '北辰区' },
            { id: '120114', name: '武清区' },
            { id: '120115', name: '宝坻区' },
            { id: '120116', name: '滨海新区' },
            { id: '120117', name: '宁河区' },
            { id: '120118', name: '静海区' },
            { id: '120119', name: '蓟州区' },
          ],
        },
      ],
    },
  ],
};

Component({
  data: {
    options: data.areaList,
    note: '请选择地址',
    visible: false,
    keys: {
      label: 'name',
      value: 'id',
      children: 'sub',
    },
  },
  methods: {
    showCascader() {
      this.setData({ visible: true });
    },
    onChange(e) {
      const { selectedOptions } = e.detail;

      this.setData({
        note: selectedOptions.map((item) => item.name).join('/'),
      });
    },
  },
});

```
```wxss
page .demo {
  --td-cascader-active-color: green;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-cascader": "tdesign-miniprogram/cascader/cascader"
  }
}

```

#### 使用次级标题

```wxml
<t-cell title="地址" note="{{note}}" bind:click="showCascader" arrow></t-cell>

<t-cascader
  visible="{{visible}}"
  options="{{options}}"
  title="请选择地址"
  sub-titles="{{subTitles}}"
  bind:change="onChange"
></t-cascader>

```
```js
const data = {
  areaList: [
    {
      label: '北京市',
      value: '110000',
      children: [
        {
          value: '110100',
          label: '北京市',
          children: [
            { value: '110101', label: '东城区' },
            { value: '110102', label: '西城区' },
            { value: '110105', label: '朝阳区' },
            { value: '110106', label: '丰台区' },
            { value: '110107', label: '石景山区' },
            { value: '110108', label: '海淀区' },
            { value: '110109', label: '门头沟区' },
            { value: '110111', label: '房山区' },
            { value: '110112', label: '通州区' },
            { value: '110113', label: '顺义区' },
            { value: '110114', label: '昌平区' },
            { value: '110115', label: '大兴区' },
            { value: '110116', label: '怀柔区' },
            { value: '110117', label: '平谷区' },
            { value: '110118', label: '密云区' },
            { value: '110119', label: '延庆区' },
          ],
        },
      ],
    },
    {
      label: '天津市',
      value: '120000',
      children: [
        {
          value: '120100',
          label: '天津市',
          children: [
            { value: '120101', label: '和平区' },
            { value: '120102', label: '河东区' },
            { value: '120103', label: '河西区' },
            { value: '120104', label: '南开区' },
            { value: '120105', label: '河北区' },
            { value: '120106', label: '红桥区' },
            { value: '120110', label: '东丽区' },
            { value: '120111', label: '西青区' },
            { value: '120112', label: '津南区' },
            { value: '120113', label: '北辰区' },
            { value: '120114', label: '武清区' },
            { value: '120115', label: '宝坻区' },
            { value: '120116', label: '滨海新区' },
            { value: '120117', label: '宁河区' },
            { value: '120118', label: '静海区' },
            { value: '120119', label: '蓟州区' },
          ],
        },
      ],
    },
  ],
};

Component({
  data: {
    options: data.areaList,
    note: '请选择地址',
    visible: false,
    subTitles: ['请选择省份', '请选择城市', '请选择区/县'],
  },
  methods: {
    showCascader() {
      this.setData({ visible: true });
    },
    onChange(e) {
      const { selectedOptions } = e.detail;

      this.setData({
        note: selectedOptions.map((item) => item.label).join('/'),
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-cascader": "tdesign-miniprogram/cascader/cascader"
  }
}

```

#### 选择任意一项

```wxml
<t-cell title="地址" note="{{note}}" bind:click="showCascader" arrow />

<t-cascader
  close-btn="{{false}}"
  check-strictly="{{true}}"
  visible="{{visible}}"
  value="{{value}}"
  options="{{options}}"
  title="请选择地址"
  bind:change="onChange"
  bind:pick="onPick"
>
  <text class="confirm-btn" slot="close-btn">确定</text>
</t-cascader>

```
```js
const data = {
  areaList: [
    {
      label: '北京市',
      value: '110000',
      children: [
        {
          value: '110100',
          label: '北京市',
          children: [
            { value: '110101', label: '东城区' },
            { value: '110102', label: '西城区' },
            { value: '110105', label: '朝阳区' },
            { value: '110106', label: '丰台区' },
            { value: '110107', label: '石景山区' },
            { value: '110108', label: '海淀区' },
            { value: '110109', label: '门头沟区' },
            { value: '110111', label: '房山区' },
            { value: '110112', label: '通州区' },
            { value: '110113', label: '顺义区' },
            { value: '110114', label: '昌平区' },
            { value: '110115', label: '大兴区' },
            { value: '110116', label: '怀柔区' },
            { value: '110117', label: '平谷区' },
            { value: '110118', label: '密云区' },
            { value: '110119', label: '延庆区' },
          ],
        },
      ],
    },
    {
      label: '天津市',
      value: '120000',
      children: [
        {
          value: '120100',
          label: '天津市',
          children: [
            { value: '120101', label: '和平区' },
            { value: '120102', label: '河东区' },
            { value: '120103', label: '河西区' },
            { value: '120104', label: '南开区' },
            { value: '120105', label: '河北区' },
            { value: '120106', label: '红桥区' },
            { value: '120110', label: '东丽区' },
            { value: '120111', label: '西青区' },
            { value: '120112', label: '津南区' },
            { value: '120113', label: '北辰区' },
            { value: '120114', label: '武清区' },
            { value: '120115', label: '宝坻区' },
            { value: '120116', label: '滨海新区' },
            { value: '120117', label: '宁河区' },
            { value: '120118', label: '静海区' },
            { value: '120119', label: '蓟州区' },
          ],
        },
      ],
    },
  ],
};

Component({
  data: {
    options: data.areaList,
    note: '请选择地址',
    visible: false,
    value: '',
  },
  methods: {
    showCascader() {
      this.setData({ visible: true });
    },
    onPick(e) {
      console.log(e.detail);
    },
    onChange(e) {
      const { selectedOptions, value } = e.detail;
      console.log(value);
      this.setData({
        value,
        note: selectedOptions.map((item) => item.label).join('/'),
      });
    },
  },
});

```
```wxss
.confirm-btn {
  color: #0052d9;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-cascader": "tdesign-miniprogram/cascader/cascader"
  }
}

```

#### 支持搜索

```wxml
<t-cell title="地址" note="{{note}}" bind:click="showCascader" arrow />

<t-cascader
  visible="{{visible}}"
  value="{{value}}"
  options="{{options}}"
  title="请选择地址"
  filterable
  filter-placeholder="搜索省/市/区"
  bind:change="onChange"
  bind:pick="onPick"
/>

```
```js
const data = {
  areaList: [
    {
      label: '北京市',
      value: '110000',
      children: [
        {
          value: '110100',
          label: '北京市',
          children: [
            { value: '110101', label: '东城区' },
            { value: '110102', label: '西城区' },
            { value: '110105', label: '朝阳区' },
            { value: '110106', label: '丰台区' },
            { value: '110107', label: '石景山区' },
            { value: '110108', label: '海淀区' },
            { value: '110109', label: '门头沟区' },
            { value: '110111', label: '房山区' },
            { value: '110112', label: '通州区' },
            { value: '110113', label: '顺义区' },
            { value: '110114', label: '昌平区' },
            { value: '110115', label: '大兴区' },
            { value: '110116', label: '怀柔区' },
            { value: '110117', label: '平谷区' },
            { value: '110118', label: '密云区' },
            { value: '110119', label: '延庆区' },
          ],
        },
      ],
    },
    {
      label: '上海市',
      value: '310000',
      children: [
        {
          value: '310100',
          label: '上海市',
          children: [
            { value: '310101', label: '黄浦区' },
            { value: '310104', label: '徐汇区' },
            { value: '310105', label: '长宁区' },
            { value: '310106', label: '静安区' },
            { value: '310107', label: '普陀区' },
            { value: '310109', label: '虹口区' },
            { value: '310110', label: '杨浦区' },
            { value: '310112', label: '闵行区' },
            { value: '310113', label: '宝山区' },
            { value: '310114', label: '嘉定区' },
            { value: '310115', label: '浦东新区' },
          ],
        },
      ],
    },
    {
      label: '广东省',
      value: '440000',
      children: [
        {
          value: '440100',
          label: '广州市',
          children: [
            { value: '440103', label: '荔湾区' },
            { value: '440104', label: '越秀区' },
            { value: '440105', label: '海珠区' },
            { value: '440106', label: '天河区' },
            { value: '440111', label: '白云区' },
          ],
        },
        {
          value: '440300',
          label: '深圳市',
          children: [
            { value: '440303', label: '罗湖区' },
            { value: '440304', label: '福田区' },
            { value: '440305', label: '南山区' },
            { value: '440306', label: '宝安区' },
            { value: '440307', label: '龙岗区' },
          ],
        },
      ],
    },
  ],
};

Component({
  data: {
    options: data.areaList,
    note: '请选择地址',
    visible: false,
    value: '',
  },
  methods: {
    showCascader() {
      this.setData({ visible: true });
    },
    onPick(e) {
      console.log(e.detail);
    },
    onChange(e) {
      const { selectedOptions, value } = e.detail;

      this.setData({
        value,
        note: selectedOptions.map((item) => item.label).join('/'),
      });
    },
  },
});

```
```json
{
  "component": true,
  "usingComponents": {
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-cascader": "tdesign-miniprogram/cascader/cascader"
  }
}

```

## API

### Cascader Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
check-strictly | Boolean | false | 父子节点选中状态不再关联，可各自选中或取消 | N
close-btn | Boolean | true | 关闭按钮 | N
filter | Function | - |  自定义过滤函数。返回 true 表示匹配，未设置时使用内置匹配规则：对路径中所有 label 拼接后做大小写不敏感的 includes 匹配。TS 类型：`CascaderFilterFunction ` `type CascaderFilterFunction<CascaderOption extends TreeOptionData = TreeOptionData> = (keyword: string, option: CascaderOption, path: CascaderOption[]) => boolean`。[通用类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/common/common.ts)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/cascader/type.ts) | N
filter-placeholder | String | - | 搜索框占位符描述文本 | N
filterable | Boolean | false | 是否可搜索，开启后顶部会展示一个搜索框  | N
keys | Object | - | 用来定义 value / label / children / disabled 在 `options` 中对应的字段别名。TS 类型：`CascaderKeysType` `type CascaderKeysType = TreeKeysType`。[通用类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/common/common.ts)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/cascader/type.ts) | N
options | Array | [] | 可选项数据源。TS 类型：`Array<CascaderOption>` | N
placeholder | String | - | 未选中时的提示文案。组件内置默认值为：'选择选项' | N
sub-titles | Array | [] | 每级展示的次标题。TS 类型：`Array<string>` | N
theme | String | step | 展示风格。可选项：step/tab | N
title | String | - | 标题 | N
value | String / Number | null | 选项值 | N
default-value | String / Number | undefined | 选项值。非受控属性 | N
visible | Boolean | false | 是否展示 | N

### Cascader Events

名称 | 参数 | 描述
-- | -- | --
change | `(detail: { value: string \| number, selectedOptions: string[] })` | `1.0.1`。值发生变更时触发
close | `(trigger: CascaderTriggerSource)` | `1.0.1`。关闭时触发。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/cascader/type.ts)。<br/>`type CascaderTriggerSource = 'overlay' \| 'close-btn' \| 'finish'`<br/>
pick | `(value: string \| number, label: string, index: number, level: number)` | `1.0.1`。选择后触发

### Cascader Slots

名称 | 描述
-- | --
close-btn | 自定义 `close-btn` 显示内容
header | `1.9.1`。头部
middle-content | `1.12.2`。中间内容
title | 自定义 `title` 显示内容

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-cascader-active-color | @brand-color | -
--td-cascader-bg-color | @bg-color-container | -
--td-cascader-border-color | @component-stroke | -
--td-cascader-content-height | 78vh | -
--td-cascader-disabled-color | @text-color-disabled | -
--td-cascader-filter-empty-color | @text-color-placeholder | -
--td-cascader-filter-empty-padding | @spacer-5 @spacer-2 | -
--td-cascader-filter-highlight-color | @brand-color | -
--td-cascader-filter-item-color | @text-color-primary | -
--td-cascader-filter-item-disabled-color | @text-color-disabled | -
--td-cascader-filter-item-hover-bg | @bg-color-secondarycontainer | -
--td-cascader-filter-item-padding | @spacer-1 @spacer-2 | -
--td-cascader-filter-padding | 0 @spacer-2 @spacer-1 | -
--td-cascader-options-height | calc(100% - @cascader-step-height) | -
--td-cascader-options-title-color | @text-color-placeholder | -
--td-cascader-step-arrow-color | @text-color-placeholder | -
--td-cascader-step-dot-size | 16rpx | -
--td-cascader-step-height | 88rpx | -
--td-cascader-title-color | @text-color-primary | -
--td-cascader-title-font | @font-title-large | -
--td-cascader-title-padding | @spacer-2 | -

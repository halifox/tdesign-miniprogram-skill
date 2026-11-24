# Form 表单

用以收集、校验和提交数据，一般由输入框、单选框、复选框、选择器等控件组成。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/form)。

> 该组件于 1.13.0 版本上线，请留意版本
> 渲染框架支持情况：WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-form": "tdesign-miniprogram/form/form",
  "t-form-item": "tdesign-miniprogram/form-item/form-item"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/HX1m0HmX8A7M)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"


### 01 组件类型

#### 基础表单

```wxml
<t-form
  id="form"
  class="form"
  data="{{formData}}"
  rules="{{rules}}"
  reset-type="initial"
  show-error-message
  using-custom-navbar
  scrollToFirstError="smooth"
  label-align="left"
  bind:reset="onReset"
  bind:submit="onSubmit"
>
  <t-form-item label="用户名" name="name">
    <t-input
      value="{{formData.name}}"
      borderless
      placeholder="请输入用户名"
      disabled="{{disabled}}"
      bind:change="onInputChange"
      data-field="name"
    />
  </t-form-item>

  <t-form-item label="密码" name="password">
    <t-input
      value="{{formData.password}}"
      borderless
      type="password"
      clearable="{{false}}"
      placeholder="请输入密码"
      disabled="{{disabled}}"
      bind:change="onInputChange"
      data-field="password"
    />
  </t-form-item>

  <t-form-item label="性别" name="gender">
    <t-radio-group
      value="{{formData.gender}}"
      disabled="{{disabled}}"
      class="box"
      borderless
      bind:change="onRadioChange"
    >
      <t-radio block="{{false}}" name="radio" value="man" label="男" />
      <t-radio block="{{false}}" name="radio" value="women" label="女" />
      <t-radio block="{{false}}" name="radio" value="secret" label="保密" />
    </t-radio-group>
  </t-form-item>

  <t-form-item label="生日" arrow name="birth">
    <t-input
      value="{{formData.birth}}"
      disabled="{{disabled}}"
      borderless
      readonly
      placeholder="请输入生日"
      bind:tap="showDatePicker"
    />
    <t-date-time-picker
      title="选择日期"
      visible="{{dateVisible}}"
      mode="date"
      format="YYYY-MM-DD"
      bind:change="onDatePickerConfirm"
      bind:close="onDatePickerClose"
      start="{{start}}"
      end="{{end}}"
    />
  </t-form-item>

  <t-form-item arrow label="籍贯" name="place">
    <t-input
      value="{{formData.place}}"
      disabled="{{disabled}}"
      borderless
      readonly
      placeholder="请选择籍贯"
      bind:tap="showCascader"
    />
    <t-cascader
      visible="{{visibleCascader}}"
      value="{{address}}"
      title="选择地址"
      options="{{options}}"
      bind:change="onChangeCascader"
      bind:visible-change="onCascaderVisibleChange"
    />
  </t-form-item>

  <t-form-item label="年限" name="age">
    <t-stepper value="{{formData.age}}" disabled="{{disabled}}" theme="filled" bind:change="onChangeStepper" />
  </t-form-item>

  <t-form-item label="自我评价" name="description">
    <t-rate
      value="{{formData.description}}"
      disabled="{{disabled}}"
      variant="filled"
      allow-half
      gap="{{rateGap}}"
      bind:change="onRateChange"
    />
  </t-form-item>

  <t-form-item label="个人简介" name="resume" t-class-label="my-label">
    <t-textarea
      value="{{formData.resume}}"
      disabled="{{disabled}}"
      class="textarea"
      indicator
      maxlength="{{50}}"
      placeholder="请输入个人简介"
      bind:change="onTextareaChange"
    />
  </t-form-item>

  <t-form-item label="上传照片" name="photo">
    <t-upload
      class="upload"
      files="{{formData.photo}}"
      disabled="{{disabled}}"
      multiple
      max="{{6}}"
      action="{{action}}"
      grid-config="{{gridConfig}}"
      bind:fail="onFail"
      bind:progress="onProgress"
      bind:change="onChangeUpload"
      bind:preview="onPreview"
      bind:success="onSuccess"
      bind:remove="onRemove"
    />
  </t-form-item>

  <view class="button-group">
    <t-button theme="primary" formType="submit" size="large" bind:tap="submit">提交</t-button>
    <t-button theme="default" variant="base" formType="reset" size="large" bind:tap="reset">重置</t-button>
  </view>
</t-form>

```
```js
Component({
  properties: {
    disabled: {
      type: Boolean,
      value: false,
    },
  },

  data: {
    formData: {
      name: '',
      password: '',
      gender: '',
      birth: '',
      place: '',
      age: 3,
      description: 2,
      resume: '',
      photo: [
        {
          url: 'https://tdesign.gtimg.com/mobile/demos/example4.png',
          name: 'uploaded1.png',
          type: 'image',
        },
        {
          url: 'https://tdesign.gtimg.com/mobile/demos/example6.png',
          name: 'uploaded2.png',
          type: 'image',
        },
      ],
    },
    visibleCascader: false,
    dateVisible: false,
    address: '120119',
    rateGap: 8,
    action: 'https://service-bv448zsw-1257786608.gz.apigw.tencentcs.com/api/upload-demo',
    gridConfig: {
      column: 3,
    },
    options: [
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
    rules: {},
  },

  lifetimes: {
    attached() {
      this.setData({
        'rules.name': [
          { pattern: '[a-zA-Z]{8}', validator: (val) => val.length === 8, message: '只能输入8个字符英文' },
        ],
        'rules.password': [{ validator: (val) => val.length > 6, message: '长度大于6个字符' }],
        'rules.description': [{ validator: (val) => val > 3, message: '分数过低会影响整体评价' }],
        'rules.gender': [{ validator: (val) => val !== '', message: '不能为空' }],
        'rules.birth': [{ validator: (val) => val !== '', message: '不能为空' }],
        'rules.place': [{ validator: (val) => val !== '', message: '不能为空' }],
        'rules.resume': [{ validator: (val) => val !== '', message: '不能为空' }],
      });
    },
  },

  methods: {
    onReset(e) {
      this.setData({
        formData: e.detail.formData,
      });
    },

    onSubmit(e) {
      console.log('===onSubmit', e);
    },

    submit() {
      const form = this.selectComponent('#form');
      form.submit();
    },
    reset() {
      const form = this.selectComponent('#form');
      form.reset();
    },

    onInputChange(e) {
      const { field } = e.currentTarget.dataset;
      this.setData({
        [`formData.${field}`]: e.detail.value,
      });
    },

    onRadioChange(e) {
      this.setData({
        'formData.gender': e.detail.value,
      });
    },

    onRateChange(e) {
      this.setData({
        'formData.description': e.detail.value,
      });
    },

    onTextareaChange(e) {
      this.setData({
        'formData.resume': e.detail.value,
      });
    },

    groupChangeFn(e) {
      console.log('groupChange:', e.detail.value);
    },

    onCascaderVisibleChange(e) {
      this.setData({ visibleCascader: e.detail.visible });
    },

    onChangeCascader(e) {
      const { selectedOptions } = e.detail;
      const placeText = selectedOptions?.map((item) => item.label).join('/');
      this.setData({
        'formData.place': placeText,
        visibleCascader: false,
      });
    },

    showCascader() {
      this.setData({ visibleCascader: true });
    },

    onChangeStepper(e) {
      this.setData({
        'formData.age': e.detail.value,
      });
    },

    onFail(e) {
      console.log('---onFail', e);
    },

    onProgress(e) {
      console.log('---onProgress:', e);
    },

    onChangeUpload(e) {
      console.log('====onChange', e);
    },

    onPreview(e) {
      console.log('====onPreview', e);
    },

    onSuccess(e) {
      const { files } = e.detail;
      this.setData({
        'formData.photo': [...files],
      });
    },

    onRemove(e) {
      const { index } = e.detail;
      const { photo } = this.data.formData;
      photo.splice(index, 1);
      this.setData({
        'formData.photo': photo,
      });
    },

    showDatePicker() {
      this.setData({ dateVisible: true });
    },

    onDatePickerConfirm(e) {
      const { value } = e.detail;
      this.setData({
        'formData.birth': value,
        dateVisible: false,
      });
    },

    onDatePickerClose() {
      this.setData({
        dateVisible: false,
      });
    },
  },
});

```
```wxss
.box {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.form {
}
.upload {
  width: 100%;
}

.textarea {
  height: 200rpx;
  width: 100%;
  --td-textarea-padding: 0;
}
page .textarea .t-textarea {
  padding: 0 !important;
}

.button-group {
  background-color: var(--bg-color-demo, #fff);
  box-sizing: border-box;
  padding: 32rpx;
  display: flex;
  justify-content: space-between;
  position: relative;
  border-bottom: 1rpx solid var(--td-component-stroke);
}

.button-group .t-button {
  height: 80rpx;
  flex: 1;
}

.button-group .t-button:not(:last-child) {
  margin-right: 32rpx;
}

.my-label {
  align-self: flex-start;
}

```
```json
{
  "component": true,
  "styleIsolation": "shared",
  "usingComponents": {
    "t-form": "tdesign-miniprogram/form/form",
    "t-form-item": "tdesign-miniprogram/form-item/form-item",
    "t-input": "tdesign-miniprogram/input/input",
    "t-radio-group": "tdesign-miniprogram/radio-group/radio-group",
    "t-radio": "tdesign-miniprogram/radio/radio",
    "t-popup": "tdesign-miniprogram/popup/popup",
    "t-cascader": "tdesign-miniprogram/cascader/cascader",
    "t-stepper": "tdesign-miniprogram/stepper/stepper",
    "t-rate": "tdesign-miniprogram/rate/rate",
    "t-textarea": "tdesign-miniprogram/textarea/textarea",
    "t-upload": "tdesign-miniprogram/upload/upload",
    "t-button": "tdesign-miniprogram/button/button",
    "t-date-time-picker": "tdesign-miniprogram/date-time-picker/date-time-picker"
  }
}

```

```wxml
<t-form
  id="form"
  data="{{formData}}"
  rules="{{rules}}"
  reset-type="empty"
  show-error-message
  using-custom-navbar
  scrollToFirstError="smooth"
  label-align="top"
  bind:reset="onReset"
  bind:submit="onSubmit"
>
  <t-form-item label="用户名" name="name">
    <t-input
      value="{{formData.name}}"
      disabled="{{disabled}}"
      borderless
      placeholder="请输入用户名"
      bind:change="onInputChange"
      data-field="name"
    />
  </t-form-item>

  <t-form-item label="密码" name="password">
    <t-input
      value="{{formData.password}}"
      disabled="{{disabled}}"
      borderless
      type="password"
      clearable="{{false}}"
      placeholder="请输入密码"
      bind:change="onInputChange"
      data-field="password"
    />
  </t-form-item>

  <t-form-item label="性别" name="gender">
    <t-radio-group
      value="{{formData.gender}}"
      disabled="{{disabled}}"
      class="box"
      borderless
      bind:change="onRadioChange"
    >
      <t-radio block="{{false}}" name="radio" value="man" label="男" />
      <t-radio block="{{false}}" name="radio" value="women" label="女" />
      <t-radio block="{{false}}" name="radio" value="secret" label="保密" />
    </t-radio-group>
  </t-form-item>

  <t-form-item label="生日" name="birth" arrow>
    <t-input
      value="{{formData.birth}}"
      disabled="{{disabled}}"
      borderless
      placeholder="请输入生日"
      readonly
      bind:tap="showDatePicker"
      data-field="birth"
    />
    <t-date-time-picker
      title="选择日期"
      visible="{{dateVisible}}"
      mode="date"
      format="YYYY-MM-DD"
      bind:change="onDatePickerConfirm"
      bind:close="onDatePickerClose"
      start="{{start}}"
      end="{{end}}"
    />
  </t-form-item>

  <t-form-item arrow label="籍贯" name="place">
    <t-input
      value="{{formData.place}}"
      disabled="{{disabled}}"
      readonly
      borderless
      placeholder="请选择籍贯"
      bind:tap="showCascader"
    />
    <t-cascader
      visible="{{visibleCascader}}"
      value="{{address}}"
      title="选择地址"
      options="{{options}}"
      bind:change="onChangeCascader"
      bind:visible-change="onCascaderVisibleChange"
    />
  </t-form-item>

  <t-form-item label="年限" name="age">
    <t-stepper value="{{formData.age}}" disabled="{{disabled}}" theme="filled" bind:change="onChangeStepper" />
  </t-form-item>

  <t-form-item label="自我评价" name="description">
    <t-rate
      value="{{formData.description}}"
      disabled="{{disabled}}"
      variant="filled"
      allow-half
      gap="{{rateGap}}"
      bind:change="onRateChange"
    />
  </t-form-item>

  <t-form-item label="个人简介" name="resume">
    <t-textarea
      value="{{formData.resume}}"
      disabled="{{disabled}}"
      class="textarea"
      indicator
      maxlength="{{50}}"
      placeholder="请输入个人简介"
      class="textarea"
      bind:change="onTextareaChange"
    />
  </t-form-item>

  <t-form-item label="上传照片" label-align="top" name="photo">
    <t-upload
      files="{{formData.photo}}"
      disabled="{{disabled}}"
      multiple
      max="{{8}}"
      action="{{action}}"
      class="upload"
      bind:fail="onFail"
      grid-config="{{gridConfig}}"
      bind:progress="onProgress"
      bind:change="onChangeUpload"
      bind:preview="onPreview"
      bind:success="onSuccess"
      bind:remove="onRemove"
    />
  </t-form-item>

  <view class="button-group">
    <t-button theme="primary" variant="light" type="submit" size="large" bind:tap="submit">提交</t-button>
    <t-button theme="default" variant="base" type="reset" size="large" bind:tap="reset">重置</t-button>
  </view>
</t-form>

```
```js
Component({
  properties: {
    disabled: {
      type: Boolean,
      value: false,
    },
  },

  data: {
    formData: {
      name: '',
      password: '',
      gender: '',
      birth: '',
      place: '',
      age: 3,
      description: 2,
      resume: '',
      photo: [
        {
          url: 'https://tdesign.gtimg.com/mobile/demos/example4.png',
          name: 'uploaded1.png',
          type: 'image',
        },
        {
          url: 'https://tdesign.gtimg.com/mobile/demos/example6.png',
          name: 'uploaded2.png',
          type: 'image',
        },
      ],
    },
    visibleCascader: false,
    dateVisible: false,
    address: '120119',
    rateGap: 8,
    action: 'https://service-bv448zsw-1257786608.gz.apigw.tencentcs.com/api/upload-demo',
    gridConfig: {
      column: 4,
    },
    options: [
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
    rules: {},
  },

  lifetimes: {
    attached() {
      this.setData({
        'rules.name': [
          { pattern: '[a-zA-Z]{8}', validator: (val) => val.length === 8, message: '只能输入8个字符英文' },
        ],
        'rules.password': [{ validator: (val) => val.length > 6, message: '长度大于6个字符' }],
        'rules.description': [{ validator: (val) => val > 3, message: '分数过低会影响整体评价' }],
        'rules.gender': [{ validator: (val) => val !== '', message: '不能为空' }],
        'rules.birth': [{ validator: (val) => val !== '', message: '不能为空' }],
        'rules.place': [{ validator: (val) => val !== '', message: '不能为空' }],
        'rules.resume': [{ validator: (val) => val !== '', message: '不能为空' }],
      });
    },
  },

  methods: {
    onReset(e) {
      this.setData({
        formData: e.detail.formData,
      });
    },

    onSubmit(e) {
      console.log('===onSubmit', e);
    },

    submit() {
      const form = this.selectComponent('#form');
      form.submit();
    },
    reset() {
      const form = this.selectComponent('#form');
      form.reset();
    },

    onInputChange(e) {
      const { field } = e.currentTarget.dataset;
      this.setData({
        [`formData.${field}`]: e.detail.value,
      });
    },

    onRadioChange(e) {
      this.setData({
        'formData.gender': e.detail.value,
      });
    },

    onRateChange(e) {
      this.setData({
        'formData.description': e.detail.value,
      });
    },

    onTextareaChange(e) {
      this.setData({
        'formData.resume': e.detail.value,
      });
    },

    groupChangeFn(e) {
      console.log('groupChange:', e.detail.value);
    },

    onCascaderVisibleChange(e) {
      this.setData({ visibleCascader: e.detail.visible });
    },

    onChangeCascader(e) {
      const { selectedOptions } = e.detail;
      const placeText = selectedOptions?.map((item) => item.label).join('/');
      this.setData({
        'formData.place': placeText,
        visibleCascader: false,
      });
    },

    showCascader() {
      this.setData({ visibleCascader: true });
    },

    onChangeStepper(e) {
      this.setData({
        'formData.age': e.detail.value,
      });
    },

    onFail(e) {
      console.log('---onFail', e);
    },

    onProgress(e) {
      console.log('---onProgress:', e);
    },

    onChangeUpload(e) {
      console.log('====onChange', e);
    },

    onPreview(e) {
      console.log('====onPreview', e);
    },

    onSuccess(e) {
      const { files } = e.detail;
      this.setData({
        'formData.photo': [...files],
      });
    },

    onRemove(e) {
      const { index } = e.detail;
      const { photo } = this.data.formData;
      photo.splice(index, 1);
      this.setData({
        'formData.photo': photo,
      });
    },

    showDatePicker() {
      this.setData({ dateVisible: true });
    },

    onDatePickerConfirm(e) {
      const { value } = e.detail;
      this.setData({
        'formData.birth': value,
        dateVisible: false,
      });
    },

    onDatePickerClose() {
      this.setData({
        dateVisible: false,
      });
    },
  },
});

```
```wxss
.box {
  width: 100%;
  display: flex;
  justify-content: space-between;
}

.textarea {
  height: 200rpx;
  width: 100%;
  --td-textarea-padding: 0;
}

.button-group {
  background-color: var(--bg-color-demo, #fff);
  box-sizing: border-box;
  padding: 32rpx;
  display: flex;
  justify-content: space-between;
  position: relative;
  border-bottom: 1rpx solid var(--td-component-stroke);
}
.upload {
  width: 100%;
}

.button-group .t-button {
  height: 80rpx;
  flex: 1;
}

.button-group .t-button:not(:last-child) {
  margin-right: 32rpx;
}

```
```json
{
  "component": true,
  "styleIsolation": "shared",
  "usingComponents": {
    "t-form": "tdesign-miniprogram/form/form",
    "t-form-item": "tdesign-miniprogram/form-item/form-item",
    "t-input": "tdesign-miniprogram/input/input",
    "t-radio-group": "tdesign-miniprogram/radio-group/radio-group",
    "t-radio": "tdesign-miniprogram/radio/radio",
    "t-popup": "tdesign-miniprogram/popup/popup",
    "t-cascader": "tdesign-miniprogram/cascader/cascader",
    "t-stepper": "tdesign-miniprogram/stepper/stepper",
    "t-rate": "tdesign-miniprogram/rate/rate",
    "t-textarea": "tdesign-miniprogram/textarea/textarea",
    "t-upload": "tdesign-miniprogram/upload/upload",
    "t-button": "tdesign-miniprogram/button/button",
    "t-date-time-picker": "tdesign-miniprogram/date-time-picker/date-time-picker"
  }
}

```


## API

### Form Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
colon | Boolean | false | 是否在表单标签字段右侧显示冒号 | N
content-align | String | left | 表单内容对齐方式：左对齐、右对齐。可选项：left/right | N
data | Object | {} | 表单数据。TS 类型：`FormData` | N
error-message | Object | - | 表单错误信息配置，示例：`{ idcard: '请输入正确的身份证号码', max: '字符长度不能超过 ${max}' }`。TS 类型：`FormErrorMessage` | N
label-align | String | right | 表单字段标签对齐方式：左对齐、右对齐、顶部对齐。可选项：left/right/top | N
label-width | String / Number | '81px' | 可以整体设置label标签宽度，默认为81px | N
required-mark | Boolean | true | 是否显示必填符号（*），默认显示 | N
required-mark-position | String | left | 表单必填符号（*）显示位置。可选项：left/right | N
reset-type | String | empty | 重置表单的方式，值为 empty 表示重置表单为空，值为 initial 表示重置表单数据为初始值。可选项：empty/initial | N
rules | Object | - | 表单字段校验规则。TS 类型：`FormRules<FormData>` `type FormRules<T extends Data = any> = { [field in keyof T]?: Array<FormRule> }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts) | N
scroll-to-first-error | String | - | 表单校验不通过时，是否自动滚动到第一个校验不通过的字段，平滑滚动或是瞬间直达。值为空则表示不滚动。可选项：''/smooth/auto | N
show-error-message | Boolean | true | 校验不通过时，是否显示错误提示信息，统一控制全部表单项。如果希望控制单个表单项，请给 FormItem 设置该属性 | N
submit-with-warning-message | Boolean | false | 【讨论中】当校验结果只有告警信息时，是否触发 `submit` 提交事件 | N

### Form Events

名称 | 参数 | 描述
-- | -- | --
reset | `(detail: { e?: FormResetEvent })` | 表单重置时触发。[通用类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/common/common.ts)
submit | `(detail: SubmitContext<FormData>)` | 表单提交时触发。其中 `context.validateResult` 表示校验结果，`context.firstError` 表示校验不通过的第一个规则提醒。`context.validateResult` 值为 `true` 表示校验通过；如果校验不通过，`context.validateResult` 值为校验结果列表。<br />【注意】⚠️ 默认情况，输入框按下 Enter 键会自动触发提交事件，如果希望禁用这个默认行为，可以给输入框添加  enter 事件，并在事件中设置 `e.preventDefault()`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts)。<br/>`interface SubmitContext<T extends Data = Data> { e?: FormSubmitEvent; validateResult: FormValidateResult<T>; firstError?: string; fields?: any }`<br/><br/>`type FormValidateResult<T> = boolean \| ValidateResultObj<T>`<br/><br/>`type ValidateResultObj<T> = { [key in keyof T]: boolean \| ValidateResultList }`<br/><br/>`type ValidateResultList = Array<AllValidateResult>`<br/><br/>`type AllValidateResult = CustomValidateObj \| ValidateResultType`<br/><br/>`interface ValidateResultType extends FormRule { result: boolean }`<br/><br/>`type ValidateResult<T> = { [key in keyof T]: boolean \| ErrorList }`<br/><br/>`type ErrorList = Array<FormRule>`<br/>
validate | `(result: ValidateResultContext<FormData>)` | 校验结束后触发，result 值为 true 表示校验通过；如果校验不通过，result 值为校验结果列表。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts)。<br/>`type ValidateResultContext<T extends Data> = Omit<SubmitContext<T>, 'e'>`<br/>

### FormInstanceFunctions 组件实例方法

名称 | 参数 | 返回值 | 描述
-- | -- | -- | --
clear-validate | `(fields?: Array<keyof FormData>)` | \- | 必需。清空校验结果。可使用 fields 指定清除部分字段的校验结果，fields 值为空则表示清除所有字段校验结果。清除邮箱校验结果示例：`clearValidate(['email'])`
reset | `(params?: FormResetParams<FormData>)` | \- | 必需。重置表单，表单里面没有重置按钮`<button type=\"reset\" />`时可以使用该方法，默认重置全部字段为空，该方法会触发 `reset` 事件。<br />如果表单属性 `resetType='empty'` 或者 `reset.type='empty'` 会重置为空；<br />如果表单属性 `resetType='initial'` 或者 `reset.type='initial'` 会重置为表单初始值。<br />`reset.fields` 用于设置具体重置哪些字段，示例：`reset({ type: 'initial', fields: ['name', 'age'] })`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts)。<br/>`interface FormResetParams<FormData> { type?: 'initial' \| 'empty'; fields?: Array<keyof FormData> }`<br/>
set-validate-message | `(message: FormValidateMessage<FormData>)` | \- | 必需。设置自定义校验结果，如远程校验信息直接呈现。注意需要在组件挂载结束后使用该方法。`FormData` 指表单数据泛型。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts)。<br/>`type FormValidateMessage<FormData> = { [field in keyof FormData]: FormItemValidateMessage[] }`<br/><br/>`interface FormItemValidateMessage { type: 'warning' \| 'error'; message: string }`<br/>
submit | `(params?: { showErrorMessage?: boolean })` | \- | 必需。提交表单，表单里面没有提交按钮`<button type=\"submit\" />`时可以使用该方法。`showErrorMessage` 表示是否在提交校验不通过时显示校验不通过的原因，默认显示。该方法会触发 `submit` 事件
validate | `(params?: FormValidateParams)` | `Promise<FormValidateResult<FormData>> ` | 必需。校验函数，包含错误文本提示等功能。泛型 `FormData` 表示表单数据 TS 类型。<br/>【关于参数】`params.fields` 表示校验字段，如果设置了 `fields`，本次校验将仅对这些字段进行校验。`params.trigger` 表示本次触发校验的范围，'params.trigger = blur' 表示只触发校验规则设定为 trigger='blur' 的字段，'params.trigger = change' 表示只触发校验规则设定为 trigger='change' 的字段，默认触发全范围校验。`params.showErrorMessage` 表示校验结束后是否显示错误文本提示，默认显示。<br />【关于返回值】返回值为 true 表示校验通过；如果校验不通过，返回值为校验结果列表。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts)。<br/>`interface FormValidateParams { fields?: Array<string>; showErrorMessage?: boolean; trigger?: ValidateTriggerType }`<br/><br/>`type ValidateTriggerType = 'blur' \| 'change' \| 'submit' \| 'all'`<br/><br/>`type FormValidateResult<T> = boolean \| ValidateResultObj<T>`<br/><br/>`type ValidateResultObj<T> = { [key in keyof T]: boolean \| ValidateResultList }`<br/><br/>`type ValidateResultList = Array<AllValidateResult>`<br/><br/>`type AllValidateResult = CustomValidateObj \| ValidateResultType`<br/><br/>`interface ValidateResultType extends FormRule { result: boolean }`<br/>


### FormItem Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
arrow | Boolean | false | 是否显示右侧箭头 | N
content-align | String | - | 表单内容对齐方式：左对齐、右对齐，优先级高于 Form.contentAlign。可选项：left/right | N
help | String | - | 表单项说明内容 | N
label | String | '' | 字段标签名称 | N
label-align | String | - | 表单字段标签对齐方式：左对齐、右对齐、顶部对齐。默认使用 Form 的对齐方式，优先级高于 Form.labelAlign。可选项：left/right/top | N
label-width | String / Number | - | 可以整体设置标签宽度，优先级高于 Form.labelWidth | N
name | String | - | 表单字段名称 | N
required-mark | Boolean | undefined | 是否显示必填符号（*），优先级高于 Form.requiredMark | N
rules | Array | - | 表单字段校验规则。TS 类型：`Array<FormRule> `，[Form API Documents](form.md#api)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form-item/type.ts) | N
show-error-message | Boolean | undefined | 校验不通过时，是否显示错误提示信息，优先级高于 `Form.showErrorMessage` | N

### FormItem Slots

名称 | 描述
-- | --
help | 自定义 `help` 显示内容
label | 自定义 `label` 显示内容

### FormRule

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
boolean | Boolean | - | 内置校验方法，校验值类型是否为布尔类型，示例：`{ boolean: true, message: '数据类型必须是布尔类型' }` | N
date | Boolean / Object | - | 内置校验方法，校验值是否为日期格式，[参数文档](https://github.com/validatorjs/validator.js)，示例：`{ date: { delimiters: '-' }, message: '日期分隔线必须是短横线（-）' }`。TS 类型：`boolean \| IsDateOptions` `interface IsDateOptions { format: string; strictMode: boolean; delimiters: string[] }`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts) | N
email | Boolean / Object | - | 内置校验方法，校验值是否为邮件格式，[参数文档](https://github.com/validatorjs/validator.js)，示例：`{ email: { ignore_max_length: true }, message: '请输入正确的邮箱地址' }`。TS 类型：`boolean \| IsEmailOptions` `import { IsEmailOptions } from 'validator/es/lib/isEmail'`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts) | N
enum | Array | - | 内置校验方法，校验值是否属于枚举值中的值。示例：`{ enum: ['primary', 'info', 'warning'], message: '值只能是 primary/info/warning 中的一种' }`。TS 类型：`Array<string>` | N
idcard | Boolean | - | 内置校验方法，校验值是否为身份证号码，组件校验正则为 `/^(\\d{18,18}\|\\d{15,15}\|\\d{17,17}x)$/i`，示例：`{ idcard: true, message: '请输入正确的身份证号码' }` | N
len | Number / Boolean | - | 内置校验方法，校验值固定长度，如：len: 10 表示值的字符长度只能等于 10 ，中文表示 2 个字符，英文为 1 个字符。示例：`{ len: 10, message: '内容长度不对' }`。<br />如果希望字母和中文都是同样的长度，示例：`{ validator: (val) => val.length === 10, message: '内容文本长度只能是 10 个字' }` | N
max | Number / Boolean | - | 内置校验方法，校验值最大长度，如：max: 100 表示值最多不能超过 100 个字符，中文表示 2 个字符，英文为 1 个字符。示例：`{ max: 10, message: '内容超出' }`。<br />如果希望字母和中文都是同样的长度，示例：`{ validator: (val) => val.length <= 10, message: '内容文本长度不能超过 10 个字' }`<br />如果数据类型数字（Number），则自动变为数字大小的比对 | N
message | String | - | 校验未通过时呈现的错误信息，值为空则不显示 | N
min | Number / Boolean | - | 内置校验方法，校验值最小长度，如：min: 10 表示值最多不能少于 10 个字符，中文表示 2 个字符，英文为 1 个字符。示例：`{ min: 10, message: '内容长度不够' }`。<br />如果希望字母和中文都是同样的长度，示例：`{ validator: (val) => val.length >= 10, message: '内容文本长度至少为 10 个字' }`。<br />如果数据类型数字（Number），则自动变为数字大小的比对 | N
number | Boolean | - | 内置校验方法，校验值是否为数字（1.2 、 1e5  都算数字），示例：`{ number: true, message: '请输入数字' }` | N
pattern | String / Object | - | 内置校验方法，校验值是否符合正则表达式匹配结果，示例：`{ pattern: /@qq.com/, message: '请输入 QQ 邮箱' }`。TS 类型：`RegExp \| string` | N
required | Boolean | - | 内置校验方法，校验值是否已经填写。该值为 true，默认显示必填标记，可通过设置 `requiredMark: false` 隐藏必填标记 | N
telnumber | Boolean | - | 内置校验方法，校验值是否为手机号码，校验正则为 `/^1[3-9]\d{9}$/`，示例：`{ telnumber: true, message: '请输入正确的手机号码' }` | N
trigger | String | change | 校验触发方式。TS 类型：`ValidateTriggerType` | N
type | String | error | 校验未通过时呈现的错误信息类型，有 告警信息提示 和 错误信息提示 等两种。可选项：error/warning | N
url | Boolean / Object | - | 内置校验方法，校验值是否为网络链接地址，[参数文档](https://github.com/validatorjs/validator.js)，示例：`{ url: { protocols: ['http','https','ftp'] }, message: '请输入正确的 Url 地址' }`。TS 类型：`boolean \| IsURLOptions` `import { IsURLOptions } from 'validator/es/lib/isURL'`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts) | N
validator | Function | - | 自定义校验规则，context 中 formData 为当前完整表单值，name为该字段的标识，示例：`{ validator: (val) => val.length > 0, message: '请输入内容'}`。TS 类型：`CustomValidator` `type CustomValidator = (val: ValueType, context?: { formData: Data , name: string }) => CustomValidateResolveType \| Promise<CustomValidateResolveType>` `type CustomValidateResolveType = boolean \| CustomValidateObj` `interface CustomValidateObj { result: boolean; message: string; type?: 'error' \| 'warning' \| 'success' }` `type ValueType = any`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/form/type.ts) | N
whitespace | Boolean | - | 内置校验方法，校验值是否为空格。示例：`{ whitespace: true, message: '值不能为空' }` | N

### FormErrorMessage

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
boolean | String | - | 布尔类型校验不通过时的表单项显示文案，全局配置默认是：`'${name}数据类型必须是布尔类型'` | N
date | String | - | 日期校验规则不通过时的表单项显示文案，全局配置默认是：`'请输入正确的${name}'` | N
enum | String | - | 枚举值校验规则不通过时的表单项显示文案，全局配置默认是：`${name}只能是${validate}等` | N
idcard | String | - | 身份证号码校验不通过时的表单项显示文案，全局配置默认是：`'请输入正确的${name}'` | N
len | String | - | 值长度校验不通过时的表单项显示文案，全局配置默认是：`'${name}字符长度必须是 ${validate}'` | N
max | String | - | 值的长度太长或值本身太大时，校验不通过的表单项显示文案，全局配置默认是：`'${name}字符长度不能超过 ${validate} 个字符，一个中文等于两个字符'` | N
min | String | - | 值的长度太短或值本身太小时，校验不通过的表单项显示文案，全局配置默认是：`'${name}字符长度不能少于 ${validate} 个字符，一个中文等于两个字符'` | N
number | String | - | 数字类型校验不通过时的表单项显示文案，全局配置默认是：`'${name}必须是数字'` | N
pattern | String | - | 正则表达式校验不通过时的表单项显示文案，全局配置默认是：`'请输入正确的${name}'` | N
required | String | - | 没有填写必填项时的表单项显示文案，全局配置默认是：`'${name}必填'` | N
telnumber | String | - | 手机号号码校验不通过时的表单项显示文案，全局配置默认是：`'请输入正确的${name}'` | N
url | String | - | 链接校验规则不通过时的表单项显示文案，全局配置默认是：`'请输入正确的${name}'` | N
validator | String | - | 自定义校验规则校验不通过时的表单项显示文案，全局配置默认是：'${name}不符合要求' | N
whitespace | String | - | 值为空格校验不通过时表单项显示文案，全局配置默认是：`'${name}不能为空` | N

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。
名称 | 默认值 | 描述
-- | -- | --
--td-form-bg-color | @bg-color-container | -
--td-form-item-arrow-align | center | -
--td-form-item-arrow-color | @text-color-placeholder | -
--td-form-item-arrow-size | 48rpx | -
--td-form-item-border-color | @component-stroke | -
--td-form-item-border-left-space | @form-item-vertical-padding | -
--td-form-item-border-right-space | 0 | -
--td-form-item-padding | @form-item-horizontal-padding @form-item-vertical-padding | -
--td-form-label-font | @font-body-large | -

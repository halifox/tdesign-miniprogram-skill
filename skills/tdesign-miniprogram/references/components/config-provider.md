# 全局特性配置

全局特性配置包含各个组件的文本语言配置及其他通用配置，可以减少重复的通用配置。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/config-provider)。

> 该组件于 1.13.0 版本上线，请留意版本
> 渲染框架支持情况：WebView、Skyline

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-config-provider": "tdesign-miniprogram/config-provider/config-provider"
}
```

## 代码演示

> [在微信开发者工具中预览效果](https://developers.weixin.qq.com/s/JIP3acmy8l7F)

> Tips: 请确保开发者工具为打开状态。导入开发者工具后，依次执行：npm i > 构建npm包 > 勾选 "将JS编译成ES5"

### 国际化配置

TDesign 支持国际化/多语言配置，目前支持的语言包括:

| 语言     | 对应文件 |
| -------- | -------- |
| 简体中文 | `zh_CN`  |
| 繁体中文 | `zh_TW`  |
| 英语     | `en_US`  |
| 韩语     | `ko_KR`  |
| 日语     | `ja_JP`  |
| 俄语     | `ru_RU`  |
| 意大利语 | `it_IT`  |
| 阿拉伯语 | `ar_KW`  |

如果你想贡献更多语言包，欢迎参考 [如何新增语言包](https://github.com/Tencent/tdesign-common/blob/develop/js/global-config/locale/CONTRIBUTING.md) 发起 PR。

### 01 配置示例

### Upload

```wxml
<t-config-provider global-config="{{globalConfig}}">
  <view class="upload-demo">
    <t-upload
      disabled
      media-type="{{['video','image']}}"
      files="{{originFiles}}"
      gridConfig="{{gridConfig}}"
      bind:success="handleSuccess"
      bind:remove="handleRemove"
      bind:click="handleClick"
    />
  </view>
</t-config-provider>

```
```js
import enUS from 'tdesign-miniprogram/locale/en_US';

Component({
  data: {
    globalConfig: enUS,
    originFiles: [
      {
        url: 'https://tdesign.gtimg.com/mobile/demos/example4.png',
        name: 'uploaded1.png',
        type: 'image',
        status: 'loading',
      },
      {
        url: 'https://tdesign.gtimg.com/mobile/demos/example5.png',
        name: 'uploaded2.png',
        type: 'image',
        percent: 68,
        status: 'loading',
      },
      {
        url: 'https://tdesign.gtimg.com/mobile/demos/example5.png',
        name: 'uploaded4.png',
        type: 'image',
        status: 'failed',
      },
    ],
    gridConfig: {
      column: 4,
      width: 160,
      height: 160,
    },
    config: {
      count: 1,
    },
  },
  methods: {
    handleSuccess(e) {
      const { files } = e.detail;
      this.setData({
        originFiles: files,
      });
    },
    handleRemove(e) {
      const { index } = e.detail;
      const { originFiles } = this.data;
      originFiles.splice(index, 1);
      this.setData({
        originFiles,
      });
    },
    handleClick(e) {
      console.log(e.detail.file);
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-config-provider": "tdesign-miniprogram/config-provider/config-provider",
    "t-upload": "tdesign-miniprogram/upload/upload"
  }
}

```

### Chat

```wxml
<t-config-provider global-config="{{globalConfig}}" themeVars="{{themeVars}}">
  <view class="chat-demo">
    <t-chat-thinking
      content="{{content}}"
      layout="block"
      status="{{status}}"
      animation="moving"
      bind:expandChange="handleExpandChange"
    />
  </view>
</t-config-provider>

```
```js
import enUS from 'tdesign-miniprogram/locale/en_US';

Component({
  data: {
    thinking: true,
    fullText:
      '嗯，用户问牛顿第一定律是不是适用于所有参考系。首先，我得先回忆一下牛顿第一定律的内容。牛顿第一定律，也就是惯性定律，说物体在没有外力作用时会保持静止或匀速直线运动。也就是说， 保持原来的运动状态。',
    currentText: '',
    isTyping: true,
    content: {
      text: '',
    },
    typeSpeed: 50,
    status: 'pending',
    startTime: 0,

    // 全部配置
    globalConfig: enUS,
    themeVars: {
      buttonPrimaryBorderColor: '#ff6b00',
      'button-primary-color': '#ff6b00',
      'button-primary-bg-color': '#ff6a0094',
    },
  },

  lifetimes: {
    attached() {
      this.setData({
        startTime: Date.now(),
      });
      this.startTyping();
    },

    detached() {
      if (this.typingTimer) {
        clearTimeout(this.typingTimer);
      }
    },
  },

  methods: {
    startTyping() {
      const { fullText, typeSpeed } = this.data;
      let currentIndex = 0;
      const typeNextChar = () => {
        if (currentIndex <= fullText.length) {
          const currentText = fullText.substring(0, currentIndex);
          // 检查是否已经完成打字
          if (currentIndex === fullText.length) {
            this.setData({
              currentText,
              content: {
                text: currentText,
              },
              isTyping: false,
              status: 'complete',
            });
            return; // 直接返回，不再继续执行
          }
          // 正常打字过程
          this.setData({
            currentText,
            content: {
              text: currentText,
            },
            isTyping: currentIndex < fullText.length,
          });
          if (currentIndex < fullText.length) {
            this.typingTimer = setTimeout(typeNextChar, typeSpeed);
          }
          currentIndex += 1;
        }
      };
      typeNextChar();
    },
    replayTyping() {
      if (this.typingTimer) {
        clearTimeout(this.typingTimer);
      }
      this.setData({
        currentText: '',
        content: {
          text: '',
        },
        isTyping: true,
        startTime: Date.now(),
      });
      this.startTyping();
    },
    onStop() {
      console.log('停止思考');
      this.setData({
        thinking: false,
      });
      wx.showToast({
        title: '已停止思考',
        icon: 'success',
      });
    },
    toggleThinking() {
      this.setData({
        thinking: !this.data.thinking,
      });
    },
    resetThinking() {
      this.setData({
        thinking: true,
      });
      wx.showToast({
        title: '已重置',
        icon: 'success',
      });
    },
  },
});

```
```wxss
.chat-example-block {
  background-color: var(--td-bg-color-container);
  padding: 32rpx;
}

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-config-provider": "tdesign-miniprogram/config-provider/config-provider",
    "t-chat-thinking": "tdesign-miniprogram/chat-thinking/chat-thinking"
  }
}

```

### 其他组件

```wxml
<wxs src="../config-provider.wxs" module="_this" />

<t-config-provider :global-config="globalConfig">
  <!-- rate -->
  <view class="rate-demo-cell">
    <view class="rate-demo-cell__title">Rating</view>

    <t-rate value="{{rateValue}}" show-text bind:change="onRateChange" />
  </view>

  <!-- calendar -->
  <t-calendar
    visible="{{visible}}"
    value="{{value}}"
    bind:confirm="handleCalendarConfirm"
    bind:close="onCalendarClose"
  />
  <t-cell arrow title="Single select date" note="{{_this.formatTimestamp(value)}}" bind:tap="handleCalendar" />

  <!-- date-time-picker -->
  <t-cell
    title="Select time"
    hover
    note="{{dateText || 'YY-MM-DD'}}"
    arrow
    data-mode="date"
    bindtap="showPicker"
    class="test"
    t-class="panel-item"
  />

  <t-date-time-picker
    auto-close
    showWeek
    visible="{{dateVisible}}"
    mode="date"
    default-value="{{date}}"
    format="YYYY-MM-DD ddd"
    filter="{{filter}}"
    formatter="{{formatter}}"
    popup-props="{{popupProps}}"
    bindchange="onConfirm"
    bindpick="onColumnChange"
    bindcancel="hidePicker"
    bindclose="handleClose"
  />

  <!-- comment -->
  <view class="comment-demo">
    <t-comment
      avatar="{{commentAvatar}}"
      author="Name1"
      content="This is a comment content."
      datetime="Today 16:38"
      folds="{{commentFold}}"
      bind:folds="handleUpdateFold"
    >
      <view slot="reply">
        <view wx:for="{{visibleReplies}}" wx:key="author">
          <t-comment
            avatar="{{item.avatar}}"
            author="{{item.author}}"
            content="{{item.content}}"
            datetime="{{item.datetime}}"
          />
        </view>
      </view>
    </t-comment>
  </view>
</t-config-provider>

```
```js
import enUS from 'tdesign-miniprogram/locale/en_US';

const REPLY_COUNT = 6;

Component({
  data: {
    globalConfig: enUS,

    // rate
    rateValue: 3,

    // calendar
    visible: false,
    value: null,

    // date-time-picker
    mode: '',
    dateVisible: false,
    date: new Date('2021-12-23').getTime(), // 支持时间戳传入
    dateText: '',
    popupProps: {
      usingCustomNavbar: true,
    },

    // comment（不传 folds.content，折叠/展开文案走全局国际化配置）
    commentAvatar: {
      shape: 'circle',
      size: '64rpx',
      image: 'https://tdesign.gtimg.com/mobile/demos/avatar1.png',
    },
    commentFold: {
      state: 'collapsed',
      total: REPLY_COUNT,
      step: 3,
    },
    replyInfo: [],
    visibleReplies: [],
  },

  lifetimes: {
    attached() {
      const replyInfo = new Array(REPLY_COUNT).fill({}).map((_, index) => ({
        author: `Name${index + 1}`,
        avatar: {
          shape: 'circle',
          size: '40rpx',
          image: 'https://tdesign.gtimg.com/mobile/demos/avatar1.png',
        },
        content: 'This is a reply content.',
        datetime: 'Today 16:38',
      }));
      this.setData({
        replyInfo,
        visibleReplies: replyInfo.slice(0, 1),
      });
    },
  },

  methods: {
    // rate
    onRateChange(e) {
      const { value } = e.detail;
      this.setData({
        rateValue: value,
      });
    },

    // calendar
    handleCalendar() {
      this.setData({ visible: true });
    },

    handleCalendarConfirm(e) {
      const { value } = e.detail;
      console.log(value);
      this.setData({
        value,
      });
    },

    onCalendarClose({ detail }) {
      console.log(detail.trigger);
    },

    // date-time-picker
    showPicker(e) {
      const { mode } = e.currentTarget.dataset;
      this.setData({
        mode,
        [`${mode}Visible`]: true,
      });
    },

    handlePickerClose(e) {
      console.log('handleClose:', e);
    },

    onPickerConfirm(e) {
      const { value } = e.detail;
      const { mode } = this.data;

      console.log('confirm', value);

      this.setData({
        [mode]: value,
        [`${mode}Text`]: value,
      });
    },

    onPickerColumnChange(e) {
      console.log('pick', e.detail.value);
    },

    // comment
    handleUpdateFold(e) {
      const { fold } = e.detail;
      const { replyInfo } = this.data;

      let visibleReplies;
      if (fold.state === 'collapsed') {
        visibleReplies = replyInfo.slice(0, 1);
      } else if (fold.state === 'partial') {
        visibleReplies = replyInfo.slice(0, 3);
      } else {
        visibleReplies = replyInfo;
      }

      this.setData({ commentFold: fold, visibleReplies });
    },
  },
});

```
```json
{
  "component": true,
  "styleIsolation": "apply-shared",
  "usingComponents": {
    "t-config-provider": "tdesign-miniprogram/config-provider/config-provider",
    "t-calendar": "tdesign-miniprogram/calendar/calendar",
    "t-cell": "tdesign-miniprogram/cell/cell",
    "t-comment": "tdesign-miniprogram/comment/comment",
    "t-date-time-picker": "tdesign-miniprogram/date-time-picker/date-time-picker",
    "t-rate": "tdesign-miniprogram/rate/rate"
  }
}

```


## API

### ConfigProvider Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
global-config | Object | - | 全局配置。TS 类型：`GlobalConfigProvider` | N
theme-vars | Object | - | 全局配置 | N

### GlobalConfigProvider

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
action-sheet | Object | - | 动作面板全局配置。TS 类型：`ActionSheetConfig` | N
calendar | Object | - | 日历组件全局配置。TS 类型：`CalendarConfig` | N
cascader | Object | - | 级联选择器全局配置。TS 类型：`CascaderConfig` | N
class-prefix | String | t | CSS 类名前缀 | N
date-time-picker | Object | - | 时间选择器全局配置。TS 类型：`DateTimePickerConfig` | N
dropdown-menu | Object | - | 下拉菜单全局配置。TS 类型：`DropdownMenuConfig` | N
guide | Object | - | 引导全局配置。TS 类型：`GuideConfig` | N
picker | Object | - | 选择器全局配置。TS 类型：`PickerConfig` | N
pull-down-refresh | Object | - | 下拉刷新全局配置。TS 类型：`PullDownRefreshConfig` | N
qrcode | Object | - | 二维码全局配置。TS 类型：`QRCodeConfig` | N
rate | Object | - | 评分全局配置。TS 类型：`RateConfig` | N
tab-bar | Object | - | 标签栏全局配置。TS 类型：`TabBarConfig` | N
upload | Object | - | 上传组件全局配置。TS 类型：`UploadConfig` | N

### ActionSheetConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
cancel | String | - | 语言配置，“取消” 按钮描述文本 | N

### AttachmentsConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
status | Object | - | 语言配置，附件上传状态描述文本。TS 类型：`{ pending: string; fail: string; }` | N

### CalendarConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
confirm | String | - | 语言配置，“确定” 按钮描述文本 | N
month-title | String | - | 语言配置，日期月面板标题描述文本。示例：“{year} / {month}” | N
months | Array | - | 月文本描述，默认值：['1 月', '2 月', '3 月', '4 月', '5 月', '6 月', '7 月', '8 月', '9 月', '10 月', '11 月', '12 月']。TS 类型：`string[]` | N
title | String | - | 语言配置，组件标题“请选择日期”描述文本 | N
weekdays | Array | - | 星期文本描述，默认值：['日', '一', '二', '三', '四', '五', '六']。TS 类型：`string[]` | N

### CascaderConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
placeholder | String | - | 语言配置，未选中时的提示文案“选择选项”描述文本 | N
title | String | - | 语言配置，组件标题“选择地址”描述文本 | N

### ChatActionbarConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
action-bar | Object | - | 语言配置，对话操作栏描述文本。TS 类型：`{ replay: string; copy: string; good: string; bad: string; share: string; quote: string; }` | N

### ChatSenderConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
placeholder | String | - | 语言配置，占位符描述文本 | N
send-text | String | - | 语言配置，发送按钮描述文本 | N
stop-text | String | - | 语言配置，停止发送按钮描述文本 | N

### ChatThinkingConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
status | Object | - | 语言配置，思考状态描述文本。TS 类型：`{ pending: string; complete: string; stop: string; }` | N

### DateTimePickerConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
cancel | String | - | 语言配置，“取消”按钮描述文本 | N
confirm | String | - | 语言配置，“确定”按钮描述文本 | N
date-label | String | - | 语言配置，“日” 描述文本 | N
format | String | 'YYYY-MM-DD HH:mm:ss' | 日期格式化规则 | N
hour-label | String | - | 语言配置，“时” 描述文本 | N
minute-label | String | - | 语言配置，“分” 描述文本 | N
month-label | String | - | 语言配置，“月” 描述文本 | N
second-label | String | - | 语言配置，“秒” 描述文本 | N
title | String | - | 语言配置，组件标题“选择时间”描述文本 | N
year-label | String | - | 语言配置，“年” 描述文本 | N

### DropdownMenuConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
confirm | String | - | 语言配置，“确定” 按钮描述文本 | N
reset | String | - | 语言配置，“重置” 按钮描述文本 | N

### FormConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
colon-text | String | - | 字段旁边的冒号，中文为“：” | N
error-message | Object | - | 表单错误信息配置，示例：`{ idcard: '请输入正确的身份证号码', max: '字符长度不能超过 ${max}' }`。TS 类型：`FormErrorMessage`，[Form API Documents](form.md#api)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/config-provider/type.ts) | N
required-mark | Boolean | true | 是否显示必填符号（*），默认显示 | N
required-mark-position | String | left | 表单必填符号（*）显示位置。可选项：left/right | N

### GuideConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
back | String | - | 语言配置， “返回” 描述文本 | N
finish | String | - | 语言配置， “完成” 描述文本 | N
next | String | - | 语言配置， “下一步” 描述文本 | N
skip | String | - | 语言配置， “跳过” 描述文本 | N

### ImageConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
error-text | String | - | 图片加载失败显示的文本，中文默认为“图片无法显示” | N
loading-text | String | - | 图片加载中显示的文本，中文默认为“图片加载中” | N
replace-image-src | Function | - | 统一替换图片 `src` 地址，参数为组件的全部属性，返回值为新的图片地址。TS 类型：`(params: ImageProps) => string`，[Image API Documents](image.md#api)。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/config-provider/type.ts) | N

### InputConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
placeholder | String | - | 语言配置，“请输入”占位符描述文本 | N

### PickerConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
cancel | String | - | 语言配置，“取消” 按钮描述文本 | N
confirm | String | - | 语言配置，“确认” 按钮描述文本 | N

### PullDownRefreshConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
loading-texts | Array | - | 提示文本描述，默认值：['下拉刷新', '松手刷新', '正在刷新', '刷新完成']。TS 类型：`string[]` | N

### QRCodeConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
expired-text | String | - | 语言配置，“二维码过期”描述文本 | N
refresh-text | String | - | 语言配置，“点击刷新”描述文本 | N
scanned-text | String | - | 语言配置，“已扫描”描述文本 | N

### RateConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
no-value-text | String | - | 语言配置，“未评分”描述文本 | N
value-text | String | - | 语言配置，评分值描述文本。示例：“{value} 分” | N

### TabBarConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
have-more-news-aria-label | String | - | 语言配置，“有n+条新的消息”描述文本。示例：“有 {value}+ 条消息” | N
have-news-aria-label | String | - | 语言配置，“有n条新的消息”描述文本。示例：“有 {value} 条消息” | N
more-news-aria-label | String | - | 语言配置，“有很多消息”描述文本 | N
news-aria-label | String | - | 语言配置，“有新的消息”描述文本 | N

### UploadConfig

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
progress | Object | - | 语言配置，上传进度相关。示例：{ uploadText: '上传中', waitingText: '待上传', 'failText': '上传失败', successText: '上传成功' }。TS 类型：`UploadConfigProgress` | N

### UploadConfigProgress

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
fail-text | String | - | 语言配置，“上传失败”文本描述 | N
success-text | String | - | 语言配置，“上传成功”文本描述 | N
uploading-text | String | - | 语言配置，“上传中”文本描述 | N
waiting-text | String | - | 语言配置，“待上传”文本描述 | N

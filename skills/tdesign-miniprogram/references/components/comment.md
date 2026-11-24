# Comment 评论

用于展示评论信息，支持回复、点赞等操作，以及折叠/展开回复区。

原文：[TDesign 官网](https://tdesign.tencent.com/miniprogram/components/comment)。

> 渲染框架支持情况：Skyline、WebView

## 引入

全局引入，在 miniprogram 根目录下的`app.json`中配置，局部引入，在需要引入的页面或组件的`index.json`中配置。

```json
"usingComponents": {
  "t-comment": "tdesign-miniprogram/comment/comment"
}
```

## 代码演示

### 基础评论

```wxml
<view class="mobile-comment">
  <t-comment
    avatar="{{avatar}}"
    content="这是一段很长很长很长很长很长很长的评论内容。"
    datetime="今天16:38·广东"
    actions="{{actions}}"
    bind:actions="onAction"
  >
    <view slot="author" class="mobile-comment__author">
      <view>Name1 名称</view>
      <t-tag class="mobile-comment__author-tag" theme="primary" variant="light" shape="round">作者</t-tag>
    </view>
  </t-comment>
</view>

```
```js
Component({
  data: {
    avatar: {
      shape: 'circle',
      size: '64rpx',
      image: 'https://tdesign.gtimg.com/mobile/demos/avatar1.png',
    },
    actions: [
      { key: 'reply', content: '回复', placement: 'start' },
      { key: 'like', content: '6', icon: 'thumb-up', placement: 'end' },
      { key: 'dislike', icon: 'uncomfortable-1', placement: 'end' },
    ],
  },
  methods: {
    onAction(e) {
      const { action } = e.detail;
      console.log('action:', action);
    },
  },
});

```
```wxss
.mobile-comment__author {
  display: flex;
  align-items: center;
  font: var(--td-font-body-small);
  color: var(--td-text-color-placeholder);
}

.mobile-comment__author-tag {
  border: none;
  --td-tag-medium-padding: 0 var(--td-spacer);
  --td-tag-primary-light-color: transparent;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-comment": "tdesign-miniprogram/comment/comment",
    "t-tag": "tdesign-miniprogram/tag/tag"
  }
}

```


### 图片评论

```wxml
<view class="mobile-comment">
  <t-comment avatar="{{avatar}}" datetime="今天16:38·广东">
    <view slot="author" class="mobile-comment__author">
      <view>Name1 名称</view>
      <t-tag class="mobile-comment__author-tag" theme="primary" variant="light" shape="round">作者</t-tag>
    </view>
    <view slot="content" class="mobile-comment__images">
      <view
        wx:for="{{images}}"
        wx:key="index"
        class="mobile-comment__images-item"
        data-index="{{index}}"
        bindtap="onImageClick"
      >
        <t-image src="{{item}}" mode="aspectFill" shape="round" style="width: 156rpx; height: 156rpx" />
      </view>
    </view>
    <view slot="actions" class="mobile-comment__actions">
      <view class="mobile-comment__reply-button">回复</view>
      <view class="mobile-comment__actions-right">
        <t-button class="mobile-comment__actions-button" icon="thumb-up" variant="text">6</t-button>
        <t-button class="mobile-comment__actions-button" icon="uncomfortable-1" variant="text" />
      </view>
    </view>
  </t-comment>
</view>

```
```js
Component({
  data: {
    avatar: {
      shape: 'circle',
      size: '64rpx',
      image: 'https://tdesign.gtimg.com/mobile/demos/avatar1.png',
    },
    images: ['https://tdesign.gtimg.com/mobile/demos/swiper1.png'],
  },
  methods: {
    onImageClick(e) {
      const { index } = e.currentTarget.dataset;
      wx.previewImage({
        current: this.data.images[index],
        urls: this.data.images,
      });
    },
    onAction(e) {
      const { action } = e.detail;
      console.log('action:', action);
    },
  },
});

```
```wxss
.mobile-comment__author {
  display: flex;
  align-items: center;
  font: var(--td-font-body-small);
  color: var(--td-text-color-placeholder);
}

.mobile-comment__author-tag {
  border: none;
  --td-tag-medium-padding: 0 var(--td-spacer);
  --td-tag-primary-light-color: transparent;
}

.mobile-comment__reply-button {
  color: var(--td-text-color-secondary);
  font: var(--td-font-body-small);
}

.mobile-comment__actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex: 1;
}

.mobile-comment__actions-right {
  display: flex;
  align-items: center;
  gap: var(--td-spacer-2);
}

.mobile-comment__actions-button {
  --td-button-default-color: var(--td-text-color-placeholder);
  --td-button-medium-padding-horizontal: calc(var(--td-spacer) / 4);
  --td-button-medium-height: var(--td-spacer-3);
  --td-button-medium-font: var(--td-font-body-small);
  --td-button-medium-icon-size: 32rpx;
  box-sizing: border-box;
}

.mobile-comment__images {
  display: flex;
  gap: var(--td-spacer);
}

.mobile-comment__images-item {
  position: relative;
  width: 156rpx;
  height: 156rpx;
  border-radius: 16rpx;
  overflow: hidden;
  flex-shrink: 0;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-comment": "tdesign-miniprogram/comment/comment",
    "t-icon": "tdesign-miniprogram/icon/icon",
    "t-tag": "tdesign-miniprogram/tag/tag",
    "t-image": "tdesign-miniprogram/image/image",
    "t-button": "tdesign-miniprogram/button/button"
  }
}

```

### 文字+图片评论

```wxml
<view class="mobile-comment">
  <t-comment avatar="{{avatar}}" datetime="今天16:38·广东">
    <view slot="author" class="mobile-comment__author">
      <view>Name1 名称</view>
      <t-tag class="mobile-comment__author-tag" theme="primary" variant="light" shape="round">作者</t-tag>
    </view>
    <view slot="content">
      <view class="mobile-comment__text">这是一段很长很长很长很长很长很长的评论内容。</view>
      <view class="mobile-comment__images">
        <view
          wx:for="{{showImages}}"
          wx:key="index"
          class="mobile-comment__images-item"
          data-index="{{index}}"
          bindtap="onImageClick"
        >
          <t-image src="{{item}}" mode="aspectFill" shape="round" style="width: 156rpx; height: 156rpx" />
          <view wx:if="{{index === maxShow - 1 && images.length > maxShow}}" class="mobile-comment__images-badge">
            共{{images.length}}张
          </view>
        </view>
      </view>
    </view>
    <view slot="actions" class="mobile-comment__actions">
      <view class="mobile-comment__reply-button">回复</view>
      <view class="mobile-comment__actions-right">
        <t-button class="mobile-comment__actions-button" icon="thumb-up" variant="text">6</t-button>
        <t-button class="mobile-comment__actions-button" icon="uncomfortable-1" variant="text" />
      </view>
    </view>
  </t-comment>
</view>

```
```js
Component({
  data: {
    avatar: {
      shape: 'circle',
      size: '64rpx',
      image: 'https://tdesign.gtimg.com/mobile/demos/avatar1.png',
    },
    images: [
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
      'https://tdesign.gtimg.com/mobile/demos/swiper1.png',
    ],
    maxShow: 3,
    showImages: [],
  },
  lifetimes: {
    attached() {
      this.setData({
        showImages: this.data.images.slice(0, this.data.maxShow),
      });
    },
  },
  methods: {
    onImageClick(e) {
      const { index } = e.currentTarget.dataset;
      wx.previewImage({
        current: this.data.images[index],
        urls: this.data.images,
      });
    },
    onAction(e) {
      const { action } = e.detail;
      console.log('action:', action);
    },
  },
});

```
```wxss
.mobile-comment__author {
  display: flex;
  align-items: center;
  font: var(--td-font-body-small);
  color: var(--td-text-color-placeholder);
}

.mobile-comment__author-tag {
  border: none;
  --td-tag-medium-padding: 0 var(--td-spacer);
  --td-tag-primary-light-color: transparent;
}

.mobile-comment__reply-button {
  color: var(--td-text-color-secondary);
  font: var(--td-font-body-small);
}

.mobile-comment__actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex: 1;
}

.mobile-comment__actions-right {
  display: flex;
  align-items: center;
  gap: var(--td-spacer-2);
}

.mobile-comment__actions-button {
  --td-button-default-color: var(--td-text-color-placeholder);
  --td-button-medium-padding-horizontal: calc(var(--td-spacer) / 4);
  --td-button-medium-height: var(--td-spacer-3);
  --td-button-medium-font: var(--td-font-body-small);
  --td-button-medium-icon-size: 32rpx;
  box-sizing: border-box;
}

.mobile-comment__text {
  margin-bottom: calc(var(--td-spacer) / 2);
}

.mobile-comment__images {
  display: flex;
  gap: var(--td-spacer);
}

.mobile-comment__images-item {
  position: relative;
  width: 156rpx;
  height: 156rpx;
  border-radius: 16rpx;
  overflow: hidden;
  flex-shrink: 0;
}

.mobile-comment__images-badge {
  position: absolute;
  right: 8rpx;
  bottom: 8rpx;
  padding: 0 var(--td-spacer);
  background: var(--td-mask-active);
  color: var(--td-text-color-anti);
  font: var(--td-font-body-extraSmall);
  border-radius: 24rpx;
  white-space: nowrap;
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-comment": "tdesign-miniprogram/comment/comment",
    "t-icon": "tdesign-miniprogram/icon/icon",
    "t-tag": "tdesign-miniprogram/tag/tag",
    "t-image": "tdesign-miniprogram/image/image",
    "t-button": "tdesign-miniprogram/button/button"
  }
}

```

### 展开/收起评论

```wxml
<view class="mobile-comment">
  <view data-author="Name1 名称" bind:longpress="onLongPress">
    <t-comment
      avatar="{{avatar}}"
      content="这是一段很长很长很长很长很长很长的评论内容。"
      datetime="今天16:38·广东"
      folds="{{folds}}"
      bind:folds="onFolds"
    >
      <view slot="author" class="mobile-comment__author">
        <view>Name1 名称</view>
        <t-tag class="mobile-comment__author-tag" theme="primary" variant="light" shape="round">作者</t-tag>
      </view>
      <view slot="actions" class="mobile-comment__actions">
        <view class="mobile-comment__reply-button" data-author="Name1 名称" bindtap="onReply">回复</view>
        <view class="mobile-comment__actions-right">
          <t-button class="mobile-comment__actions-button" icon="thumb-up" variant="text">6</t-button>
          <t-button class="mobile-comment__actions-button" icon="uncomfortable-1" variant="text" />
        </view>
      </view>
      <!-- 回复区 -->
      <view slot="reply">
        <view wx:for="{{visibleReplies}}" wx:key="index" data-author="{{item.author}}" bind:longpress="onLongPress">
          <t-comment avatar="{{item.avatar}}" datetime="{{item.datetime}}">
            <view slot="author" class="mobile-comment__author">
              <view>{{item.author}}</view>
            </view>
            <view slot="content">
              <block wx:if="{{item.replyTo}}">
                <text>回复</text>
                <text class="mobile-comment__reply-name">{{item.replyTo}}</text>
                <text>：{{item.content}}</text>
              </block>
              <block wx:else>{{item.content}}</block>
            </view>
            <view slot="actions" class="mobile-comment__actions">
              <view class="mobile-comment__reply-button" data-author="{{item.author}}" bindtap="onReply">回复</view>
              <view class="mobile-comment__actions-right">
                <t-button
                  class="mobile-comment__actions-button"
                  icon="thumb-up"
                  variant="text"
                  data-index="{{index}}"
                  bindtap="onLike"
                  >{{item.likeNum || ''}}</t-button
                >
                <t-button class="mobile-comment__actions-button" icon="uncomfortable-1" variant="text" />
              </view>
            </view>
          </t-comment>
        </view>
      </view>
    </t-comment>
  </view>

  <!-- 回复输入框 -->
  <view wx:if="{{showReplyInput}}" class="mobile-comment__input">
    <input
      class="mobile-comment__input-content"
      placeholder="{{replyTarget ? '回复' + replyTarget : '请输入内容'}}"
      value="{{replyValue}}"
      bindinput="onInputChange"
      bindconfirm="onSubmit"
      focus="{{focusInput}}"
    />
    <t-button
      class="mobile-comment__input-button"
      theme="primary"
      shape="circle"
      size="small"
      icon="send"
      disabled="{{!replyValue}}"
      bindtap="onSubmit"
    />
  </view>

  <!-- ActionSheet -->
  <t-action-sheet
    visible="{{showActionSheet}}"
    cancel-text="取消"
    items="{{actionSheetItems}}"
    bind:selected="onActionSheetSelect"
    bind:close="onActionSheetClose"
    bind:cancel="onActionSheetClose"
  />
</view>

```
```js
const REPLY_COUNT = 6;

Component({
  data: {
    avatar: {
      shape: 'circle',
      size: '64rpx',
      image: 'https://tdesign.gtimg.com/mobile/demos/avatar1.png',
    },
    folds: {
      state: 'collapsed',
      total: REPLY_COUNT,
      step: 3,
      content: {
        collapsed: `展开${REPLY_COUNT - 1}条回复`,
        partial: ['展开更多回复', '收起'],
        expanded: '收起',
      },
    },
    replyInfo: [],
    visibleReplies: [],
    // 回复输入框（待对齐视觉，暂不展示）
    showReplyInput: false,
    replyValue: '',
    replyTarget: '',
    focusInput: false,
    // ActionSheet
    showActionSheet: false,
    actionSheetItems: ['回复', '转发', '复制', '举报'],
    longPressTarget: '',
  },

  lifetimes: {
    attached() {
      const replyInfo = [];
      for (let i = 0; i < REPLY_COUNT; i += 1) {
        replyInfo.push({
          author: `Name${i + 1} 名称`,
          avatar: {
            shape: 'circle',
            size: '40rpx',
            image: 'https://tdesign.gtimg.com/mobile/demos/avatar1.png',
          },
          content: '这是一段很长很长很长很长很长很长的评论内容。',
          datetime: '今天16:38·广东',
          likeNum: 6,
        });
      }
      this.setData({
        replyInfo,
        visibleReplies: replyInfo.slice(0, 1),
      });
    },
  },

  methods: {
    onFolds(e) {
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

      this.setData({ folds: fold, visibleReplies });
    },

    onAction(e) {
      const { action } = e.detail;
      console.log('action:', action);
    },

    onReply(e) {
      const { author } = e.currentTarget.dataset;
      // 待对齐视觉后展示输入框，当前仅记录回复目标
      this.setData({ replyTarget: author });
    },

    onLike(e) {
      const { index } = e.currentTarget.dataset;
      const { replyInfo } = this.data;
      this.setData({
        [`replyInfo[${index}].likeNum`]: replyInfo[index].likeNum + 1,
      });
    },

    onLongPress(e) {
      const { author } = e.currentTarget.dataset;
      this.setData({
        longPressTarget: author || 'Name1 名称',
        showActionSheet: true,
      });
    },

    onActionSheetSelect(e) {
      const { label } = e.detail;
      if (label === '回复' && this.data.longPressTarget) {
        // 待对齐视觉后展示输入框
        this.setData({ replyTarget: this.data.longPressTarget });
      }
      this.setData({ showActionSheet: false });
    },

    onActionSheetClose() {
      this.setData({ showActionSheet: false });
    },

    onInputChange(e) {
      this.setData({ replyValue: e.detail.value });
    },

    onSubmit() {
      const { replyValue, replyTarget, replyInfo } = this.data;
      if (!replyValue.trim()) return;

      const now = new Date();
      const hours = String(now.getHours()).padStart(2, '0');
      const minutes = String(now.getMinutes()).padStart(2, '0');

      const newReply = {
        author: '我',
        avatar: {
          shape: 'circle',
          size: '40rpx',
          image: 'https://tdesign.gtimg.com/mobile/demos/avatar2.png',
        },
        content: replyValue,
        datetime: `今天${hours}:${minutes}·广东`,
        likeNum: 0,
        ...(replyTarget ? { replyTo: replyTarget } : {}),
      };

      const newReplyInfo = [...replyInfo, newReply];
      const newTotal = newReplyInfo.length;

      this.setData({
        replyInfo: newReplyInfo,
        visibleReplies: newReplyInfo,
        folds: {
          ...this.data.folds,
          state: 'expanded',
          total: newTotal,
          content: {
            collapsed: `展开${newTotal - 1}条回复`,
            partial: ['展开更多回复', '收起'],
            expanded: '收起',
          },
        },
        replyValue: '',
        replyTarget: '',
        showReplyInput: false,
        focusInput: false,
      });
    },
  },
});

```
```wxss
.mobile-comment__author {
  display: flex;
  align-items: center;
  font: var(--td-font-body-small);
  color: var(--td-text-color-placeholder);
}

.mobile-comment__author-tag {
  border: none;
  --td-tag-medium-padding: 0 var(--td-spacer);
  --td-tag-primary-light-color: transparent;
}

.mobile-comment__reply-button {
  color: var(--td-text-color-secondary);
  font: var(--td-font-body-small);
}

.mobile-comment__reply-name {
  color: var(--td-text-color-secondary);
  font: var(--td-font-body-medium);
}

.mobile-comment__actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex: 1;
}

.mobile-comment__actions-right {
  display: flex;
  align-items: center;
  gap: var(--td-spacer-2);
}

.mobile-comment__actions-button {
  --td-button-default-color: var(--td-text-color-placeholder);
  --td-button-medium-padding-horizontal: calc(var(--td-spacer) / 4);
  --td-button-medium-height: var(--td-spacer-3);
  --td-button-medium-font: var(--td-font-body-small);
  --td-button-medium-icon-size: 32rpx;
  box-sizing: border-box;
}

.mobile-comment__input {
  display: flex;
  padding: 24rpx;
  gap: var(--td-spacer);
  border-radius: 32rpx;
  border: 1px solid #dcdcdc;
  background: #ffffff;
  box-shadow:
    0 12rpx 60rpx 10rpx rgba(0, 0, 0, 0.05),
    0 32rpx 48rpx 4rpx rgba(0, 0, 0, 0.04),
    0 16rpx 20rpx -10rpx rgba(0, 0, 0, 0.08);
  margin-top: 96rpx;
}

.mobile-comment__input-content {
  border: none;
  flex: 1;
  background: transparent;
}

.mobile-comment__input-button {
  --td-button-primary-disabled-bg: #dcdcdc;
  --td-button-primary-disabled-border-color: transparent;
  transform: rotate(-90deg);
}

```
```json
{
  "component": true,
  "usingComponents": {
    "t-comment": "tdesign-miniprogram/comment/comment",
    "t-icon": "tdesign-miniprogram/icon/icon",
    "t-tag": "tdesign-miniprogram/tag/tag",
    "t-button": "tdesign-miniprogram/button/button",
    "t-action-sheet": "tdesign-miniprogram/action-sheet/action-sheet"
  }
}

```

## API

### Comment Props

名称 | 类型 | 默认值 | 描述 | 必传
-- | -- | -- | -- | --
style | Object | - | 样式 | N
custom-style | Object | - | 样式，一般用于开启虚拟化组件节点场景 | N
actions | Array | - | 操作。TS 类型：`Array<CommentActionItem>` `type ActionPlacement = 'start' \| 'end'` `interface CommentActionItem { key: string; content?: string; icon?: string \| object; placement?: ActionPlacement; disabled?: boolean}`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/comment/type.ts) | N
author | String | - | 作者 | N
avatar | String / Object | - | 头像。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/comment/type.ts) | N
content | String | - | 内容 | N
datetime | String | - | 时间 | N
folds | Object | - | 折叠/展开配置项。TS 类型：`CommentFold ` `type CommentFoldState = 'collapsed' \| 'partial' \| 'expanded'` `interface CommentFold { state: CommentFoldState; total?: number; step?: number; content?: Partial<Record<CommentFoldState, string \| [string, string]>>}`。[详细类型定义](https://github.com/Tencent/tdesign-miniprogram/blob/develop/packages/components/comment/type.ts) | N
reply | String | - | 回复 | N

### Comment Events

名称 | 参数 | 描述
-- | -- | --
actions | `(detail: { action: CommentActionItem;})` | 点击任一操作项（如回复/点赞/不喜欢）时触发并返回当前操作项
folds | `(detail: { fold: CommentFold;})` | 用户点击“展开回复/收起”时触发，并返回点击后的 fold 配置

### Comment Slots

名称 | 描述
-- | --
actions | 自定义 `actions` 显示内容
author | 自定义 `author` 显示内容
avatar | 自定义 `avatar` 显示内容
content | 自定义 `content` 显示内容
datetime | 自定义 `datetime` 显示内容
reply | 自定义 `reply` 显示内容

### CSS Variables

组件提供了下列 CSS 变量，可用于自定义样式。

名称 | 默认值 | 描述
-- | -- | --
--td-comment-inner-padding | @spacer-1 @spacer-2 calc(@spacer / 2) @spacer-2 | 评论区内边距
--td-comment-content-color | @text-color-primary | 评论内容颜色
--td-comment-author-color | @text-color-placeholder | 作者名称颜色
--td-comment-datetime-color | @text-color-disabled | 时间颜色
--td-comment-bottom-margin-top | calc(@spacer / 2) | 底部操作区上边距

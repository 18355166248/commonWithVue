<template>
  <transition name="wl-fade">
    <div v-if="show" class="wl-fade-in">
      <h3 class="wl-fade-in-header" v-if="$slots.header">
        <slot name="header"></slot>
      </h3>
      <!-- 主体区 -->
      <el-scrollbar class="wl-fade-in-scroll" v-if="useScroll">
        <slot></slot>
      </el-scrollbar>
      <div v-else class="wl-fade-in-main" :class="ftBodyClass">
        <slot></slot>
      </div>
      <!-- 主体内容区 - 底部 -->
      <div class="wl-fade-in-footer" v-if="$slots.footer">
        <slot name="footer"></slot>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'wl-fadein',
  props: {
    // 是否显示
    show: {
      type: Boolean,
      default: false,
    },
    // 是否使用scroll组件
    useScroll: {
      type: Boolean,
      default: true,
    },
    // 自定义main的class
    ftBodyClass: [String, Function],
  },
}
</script>

<style lang="scss">
.wl-fade-in {
  display: flex;
  flex-direction: column;
  flex-grow: 1;
  flex-shrink: 1;
  position: fixed;
  top: $header_height + $main_body_padding;
  bottom: $main_body_padding;
  right: $main_body_padding;
  z-index: 9;
  width: 460px;
  background: #fff;
  border: 1px solid $border-color-eee;
  box-shadow: -2px 0 5px rgba(136, 133, 133, 0.6);

  > .wl-fade-in-header {
    padding: $space-s $space-l;
    line-height: 24px;
    font-size: 16px;
    font-weight: 600;
    color: #333;
    border-bottom: 1px solid $border-color-eee;
  }

  > .wl-fade-in-footer {
    padding: $space-s $space-l;
  }

  > .wl-fade-in-scroll {
    flex: 1;
    flex-grow: 1;
    flex-shrink: 1;
    > .el-scrollbar__wrap {
      overflow-x: hidden;
      > .el-scrollbar__view {
        padding: $space-s $space-l;
      }
    }
  }
  > .wl-fade-in-main {
    position: relative;
    flex: 1;
    flex-grow: 1;
    flex-shrink: 1;
    overflow: hidden;
    padding: $space-s $space-l;
  }
}
.wl-fade-enter-active,
.wl-fade-leave-active {
  transition: all 0.3s;
}
.wl-fade-enter, .wl-fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  transform: translateX(50%);
  opacity: 0;
}
</style>

<template>
  <text
    v-if="type"
    class="am-icon"
    :class="iconClass"
    :style="iconStyle"
  >{{Icon[type] || type}}</text>
</template>

<script>
import Icon from './icon'
const dom = weex.requireModule('dom')

export default {
  name: 'am-icon',
  props: {
    type: {
      type: String,
      default: null
    },
    size: {
      type: [String, Number],
      default: 'md' // xxs,xs,sm,md,lg
    },
    color: {
      type: String,
      default: null
    },
    fontFamily: {
      type: String,
      default: 'AMUIIconFont'
    }
  },
  data () {
    return {
      Icon
    }
  },
  computed: {
    iconClass () {
      if (isNaN(this.size)) {
        return [`am-icon-${this.size}`]
      } else {
        return null
      }
    },
    iconStyle () {
      const style = {
        color: this.color,
        fontFamily: this.fontFamily
      }
      if (!isNaN(this.size)) {
        style.fontSize = this.size + 'px'
        style.lineHeight = this.size + 'px'
      }
      return style
    }
  },
  beforeCreate () {
    dom.addRule('fontFace', {
      'fontFamily': 'AMUIIconFont',
      'src': "url('https://at.alicdn.com/t/font_666184_6i47o5l7pbiysyvi.ttf')"
    })
  }
}
</script>

<style scoped lang="less">
@import "../../theme/am-icon/index.less";
</style>

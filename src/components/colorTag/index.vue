<template>
  <div class="color-tag">
    <p>单位:mm</p>
    <ul :class="{'arrange-col': arrangeStyle === 'col'}">
      <li v-for="(item,index) in tags" :key="index">
        <span
          class="tag"
          :style="{width: (arrangeStyle === 'row' ? `${tagWidth}px` :`${tagHeight}px`), height: arrangeStyle === 'row' ? `${tagHeight}px` : `${tagWidth}px`, background: item.color}"
        >
        </span>
        <span
          class="tag-value"
          :class="{'row-center': (arrangeStyle === 'row' && valueStyle === 'center'), 'col-center': (arrangeStyle === 'col' && valueStyle === 'center')}"
          :style="tagValueStyle"
        >{{item.value}}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import tags from '../../utils/tag.js'
export default {
  data() {
    return {
      tags
    }
  },
  props: {
    valueStyle: {
      type: String,
      default: 'calipers'
    },
    arrangeStyle: {
      type: String,
      default: 'row'
    },
    arranageRow: {
      type: String,
      default: 'right'
    },
    arranageCol: {
      type: String,
      default: 'top'
    },
    tagWidth: {
      type: Number,
      default: 20
    },
    tagHeight: {
      type: Number,
      default: 40
    },
  },
  computed: {
    tagValueStyle() {
      const style = {}
      style.width = `${this.tagWidth}px`
      style.height =  `${this.tagHeight}px`
      if (this.arrangeStyle === 'row' && this.arranageRow === 'left') {
        style.left = `-${this.tagWidth + 10}px`
      } else if (this.arrangeStyle === 'row' && this.arranageRow === 'right') {
        style.left = `${this.tagWidth + 10}px`
        style.justifyContent = 'flex-start'
      } else if (this.arrangeStyle === 'col' && this.arranageCol === 'top') {
        style.width = `${this.tagHeight}px`
        style.height =  `${this.tagWidth}px`
        style.bottom = `${this.tagWidth + 10}px`
        style.right = `-10px`
      } else if (this.arrangeStyle === 'col' && this.arranageCol === 'bottom') {
        style.width = `${this.tagHeight}px`
        style.height =  `${this.tagWidth}px`
        style.bottom = `-${this.tagWidth + 10}px`
        style.right = `-10px`
        style.alignItems = `flex-start`
      }
      return style
    }
  }
}
</script>

<style lang="scss" scoped>
.color-tag {
  margin-left: 42px;
  p {
    font-size: 13px;
    color: #000;
    line-height: 19px;
    margin: 0;
    margin-bottom: 4px;
  }
  ul {
    padding: 0;
    margin: 0;
    padding-left: 20px;
  }
  .arrange-col {
    display: flex;
    margin-top:30px;
    li {
      .tag {
        border: 1px solid #000;
        border-right: none;
      }
    }
    li:last-child {
      .tag {
        border-right: 1px solid #000;
      }
    }
  }
  li {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    position: relative;
    .tag {
      border: 1px solid #000;
      border-bottom: none;
      display: block;
    }
    .tag-value {
      font-size: 14px;
      color: #000;
      position: absolute;
      bottom: -10px;
      display: flex;
      align-items: flex-end; 
      justify-content: flex-end;
    }
    .row-center {
      position: absolute;
      bottom: 0;
      align-items: center;
      right: 0 !important;
    }
    .col-center {
      position: absolute;
      bottom: 0;
      justify-content: center;
      right: 0 !important;
    }
  }
  li:last-child {
    .tag {
      border-bottom: 1px solid #000;
    }
  }
}
</style>
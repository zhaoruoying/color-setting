<template>
  <div class="color-setting">
    <div class="setting">
      <div class="head">
        <span>色谱设置</span>
        <div class="arrow"></div>
      </div>
      <div class="setting-detail value-detail">
        <span class="detail-title">数值样式</span>
        <Radio v-model="valueStyle" label="calipers" @change="changeValue">卡尺式</Radio>
        <Radio v-model="valueStyle" label="center" @change="changeValue">居中式</Radio>
      </div>
      <div class="setting-detail">
        <span class="detail-title">排列样式</span>
        <div class="arrange-style">
          <Radio v-model="arrangeStyle" label="row" @change="changeArrange">竖排</Radio>
          <div class="arranage-button">
            <span>数值在</span>
            <div class="buttons">
              <span :class="{'is-active': arranageRow === 'left'}" @click="arranageRow = 'left'">左</span>
              <span :class="{'is-active': arranageRow === 'right'}" @click="arranageRow = 'right'">右</span>
            </div>
          </div>
        </div>
        <div class="arrange-style">
          <Radio v-model="arrangeStyle" label="col" @change="changeArrange">横排</Radio>
          <div class="arranage-button">
            <span>数值在</span>
            <div class="buttons">
              <span :class="{'is-active': arranageCol === 'top'}" @click="arranageCol = 'top'">上</span>
              <span :class="{'is-active': arranageCol === 'bottom'}" @click="arranageCol = 'bottom'">下</span>
            </div>
          </div>
        </div>
      </div>
      <div class="setting-detail">
        <span class="detail-title">单色块的长宽</span>
        <div class="color-style">
          <div class="color-inner">
            <span>长</span>
            <div class="color-input">
              <input type="number" v-model="height" @input="height = parseInt(height)" @change="changeHeight"  />
              <span>px</span>
            </div>
          </div>
          <div class="color-inner">
            <span>宽</span>
            <div class="color-input">
              <input type="number" v-model="width" @input="width = parseInt(width)"  @change="changeWidth" />
              <span>px</span>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="content">
      <color-tag
        :valueStyle="valueStyle" 
        :arrangeStyle="arrangeStyle"
        :tagWidth="width"
        :tagHeight="height"
        :arranageRow='arranageRow'
        :arranageCol="arranageCol"
      />
    </div>
  </div>
</template>

<script>
import Radio from '@/components/radio/index.vue';
import ColorTag from '@/components/colorTag/index.vue'
export default {
  components: {
    Radio,
    ColorTag
  },
  data() {
    return {
      valueStyle: 'calipers', // calipers：卡尺，center：居中
      arrangeStyle: 'row', // row: 竖排，col: 横排
      arranageRow: 'right',
      arranageCol: 'top',
      width: 20,
      height: 40
    }
  },
  methods: {
    // 数值样式
    changeValue(val) {
      this.valueStyle = val
    },
    // 列表样式
    changeArrange(val) {
      this.arrangeStyle = val
    },
    changeHeight () {
      const val = parseInt(this.height)
      if (val < 20) {
        this.height = 20
      } else if ( val > 100) {
        this.height = 100
      }
      this.height = parseInt(this.height)
    },
    changeWidth () {
      const val = parseInt(this.width)
      if (val < 20) {
        this.width = 20
      } else if ( val > 100) {
        this.width = 100
      }
      this.width = parseInt(this.width)
    }
  },
}
</script>

<style lang="scss">
.color-setting {
  text-align: left;
  padding: 14px 0 0 15px;
  display: flex;
  height: 264px;
  background: #f2f2f2;
  .setting {
    width: 266px;
    background: #f8feff;
    box-shadow: 4px 4px 15px #cdcdcd;
    border-radius: 2px;
    display: inline-table;
    .head {
      height: 33px;
      background: #e3f1f5;
      line-height: 33px;
      display: flex;
      align-items: center;
      span {
        background: #38A7F0;
        height: 33px;
        display: block;
        width:77px;
        text-align: center;
        color: #ffffff;
        font-size: 14px;
      }
      .arrow {
        width: 0;
        height: 0;
        border-top: 4px solid  #e3f1f5;
        border-left: 4px solid  #e3f1f5;
        border-right: 6px solid  #e3f1f5;
        border-bottom: 6px solid #38A7F0;
        transform:rotate(90deg);
      }
    }
    .value-detail {
      display: flex;
      align-content: center;
    }
    .setting-detail {
      margin: 9px 12px 0 ;
      padding-bottom: 11px;
      border-bottom: 1px dashed #c0c4c5;
      color: #757676;
      font-size: 12px;
      .detail-title {
        font-size: 14px;
        border-left: 3px solid #f89751;
        padding-left: 6px;
        margin-right: 24px;
      }
      .arrange-style {
        margin-top:8px;
        display: flex;
        align-items: center;
      }
      .arranage-button {
        font-size: 14px;
        display: inline-block;
        .buttons {
          display: inline-flex;
          margin-left: 5px;
          width:41px;
          span {
            font-size: 12px;
            color: #7e7e7e;
            line-height: 15px;
            flex: 1;
            text-align: center;
          }
          .is-active {
            color: #ffffff;
            background: #38a7f0;
          }
          span:first-child {
            border: 1px solid #38a7f0;
            border-radius: 2px 0 0 2px;
          }
          span:last-child {
            border: 1px solid #38a7f0;
            border-radius: 0 2px 2px 0;
          }
        }
      }
      .color-style {
        display: flex;
        .color-inner {
          display: inline-flex;
          justify-content: center;
          align-items: center;
          margin-right: 15px;
          margin-top: 12px;
          .color-input {
            border: 1px solid #bebcbcbc;
            margin-left: 3px;
            padding-right: 4px;
            input {
              width: 20px;
              height: 20px;
              color: #757676;
              border: none;
              text-align: center;
            }
            input::-webkit-outer-spin-button,
            input::-webkit-inner-spin-button {
                appearance: none;
            }
            input:focus {
              outline:  none;
            }
          }
        }
      }
    }
    .setting-detail:last-child {
      border: none;
    }
  }
}

</style>
<template>
  <div class="com_pagination">
    <div>
      <el-select v-model="value" placeholder="请选择">
        <el-option v-for="item in options" :key="item.value" :label="item.label" :value="item.value">
        </el-option>
      </el-select>
    </div>
    <div><span>共{{totalNum}}条记录</span></div>
    <div @click="minusPage"><i class="el-icon-arrow-left"></i></div>
    <div><input type="text" class="choosePage" v-model="input" @blur="choosePage"></div>
    <div>/</div>
    <div>{{Math.ceil(totalNum/value)}}</div>
    <div @click="addPage"> <i class="el-icon-arrow-right"></i></div>
  </div>

</template>

<script>
  export default {
    props: [ 'totalNum' ],
    data() {
      return {
        input: '1',
        options: [ {
          value: 10,
          label: '10行/页'
        }, {
          value: 20,
          label: '20行/页'
        }, {
          value: 50,
          label: '50行/页'
        }, {
          value: 100,
          label: '100行/页'
        }, {
          value: 500,
          label: '500行/页'
        } ],
        value: 10
      }
    },
    methods: {

      choosePage() {
        if( this.input == '' ) {
          this.input = 1
        }
      },
      minusPage() {
        if( this.input != 1 ) {
          this.input--
        }
        console.log( this.value )
      },
      addPage() {
        this.input++
      }
    },
    watch: {
      input( newVal, oldVal ) {
        if( newVal != '' ) {
          if( /^[0-9]*$/.test( newVal ) ) {
            if( newVal > Math.ceil( this.totalNum / this.value ) ) {
              this.input = oldVal
            }
            if( newVal < 1 ) {
              this.input = oldVal
            }
          } else {
            this.input = oldVal
          }

        }
      }
    }

  }
</script>
<style scoped>
  .com_pagination {
    display: flex;
    align-items: center;

  }

  .com_pagination div {
    margin-left: 12px
  }

  .el-icon-arrow-left,
  .el-icon-arrow-right {
    cursor: pointer;
  }
</style>

<style>
  input {
    outline: none;
  }

  .com_pagination {
    font-size: 12px;
  }

  .com_pagination .el-input {
    font-size: 12px;
    width: 100px;
    height: 28px;
  }

  .com_pagination .el-input__inner {
    width: 100px;
    height: 28px;
    background: rgba(255, 255, 255, 1);
    border-radius: 4px;
    border: 1px solid rgba(234, 234, 234, 1);
  }

  .choosePage {
    width: 40px;
    text-align: center;
    box-sizing: border-box;
    height: 28px;
    background: rgba(255, 255, 255, 1);
    border-radius: 4px;
    border: 1px solid rgba(234, 234, 234, 1);

  }

  .choosePage:focus {
    border-color: #2b74ed;
  }

  .com_pagination .el-input__icon {
    line-height: 28px;
  }
</style>
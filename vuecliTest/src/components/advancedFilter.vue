<template>
  <div class="advanced">
    <div style="display:inline-block">
      <el-tag v-for="(tag,i) in tags" :key="i" closable size="small" color="#E0E9FA" :disable-transitions="false" @close="handleClose(tag)">{{tag.join(' ')}}</el-tag>
    </div>
    <span class="advancedFilter-btn" @click="dialogVisible = true">高级筛选</span>
    <el-dialog title="高级筛选" :visible.sync="dialogVisible" :before-close="handleClose1">
      <div class="advancedFilter">
        <div>
          <div>
            <div style="line-height:16px">筛选条件:</div>
            <div class="addFilter"><span @click="addcount()">添加筛选条件</span> </div>
            <div v-for="el in gjsxcount" :key="el" class="line">
              <el-select v-model="gjResultarr[el-1].name" placeholder="请选择" @change="yiji(el)" style="width:78px !important;height:28px !important;margin-right:4px;" size="small">
                <el-option v-for="(item,i) in data7" :key="i" :label="item.name" :value="item.name"></el-option>
              </el-select>
              <el-select style="width:78px !important;height:28px !important;margin-right:4px;" v-model="gjResultarr[el-1].compare" placeholder="请选择" size="small">
                <el-option v-for="(item,i) in gjArr[el-1].compare" :key="i" :label="item" :value="item"></el-option>
              </el-select>
              <span v-if="!gjArr[el-1].valuetype" class="lineFilter">
                <el-select v-model="gjResultarr[el-1].value" multiple placeholder="请选择" size="small" style="width:191px !important;" collapse-tags="true">

                </el-select>
              </span>
              <span v-if="gjArr[el-1].valuetype =='list'" class="lineFilter">
                <el-select v-model="gjResultarr[el-1].value" value-key="ip" multiple placeholder="请选择" size="small" style="width:191px !important;" collapse-tags="true">
                  <el-option v-for="(item,i) in gjArr[el-1].value" :key="i" :label="item" :value="item"></el-option>
                </el-select>
              </span>

              <el-input class="lineinput" v-model="gjResultarr[el-1].value" placeholder="请输入" v-if="gjArr[el-1].valuetype=='text'" size="small" style="width:191px !important;"></el-input>
              <img @click="btn2(el)" style="position: absolute;right: -26px;top: 19px;width:11px;height:11px;" src="https://salary-file.peoplus.cn/web-img/close.png">
            </div>

            <!-- <button @click="btn">唧唧复唧唧</button>
            <button @click="btn1">木兰当户织</button>-->
          </div>
        </div>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="btn">取 消</el-button>
        <el-button type="primary" @click="btn1">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>
<script>
  export default {
    props: [ "data7" ],
    methods: {},
    data() {
      return {
        dialogVisible: false,
        tagList: [],
        gjsxcount: 0,
        value: "",
        tags: [],
        gjArr: [],
        gjResultarr: [],
        obj: {
          str: ""
        },
      };
    },
    methods: {
      handleClose1( done ) {
        this.dialogVisible = false;
      },
      addcount() {
        this.gjsxcount++;
        this.gjArr.push( {
          name: ""
        } );
        let obj = {
          name: "",
          compare: '',
          value: []
        }
        this.gjResultarr.push( obj );
      },
      btn() {
        // console.log( this.gjResultarr )
        this.dialogVisible = false;
      },
      string() {
        this.tags = [];
        this.gjResultarr.forEach( el => {
          this.tags.push( [ el.value ] );
        } );
        console.log( this.tags.join( "、" ) );
      },
      btn1() {
        this.tags = [];
        console.log( this.gjResultarr )
        this.gjResultarr.forEach( ( el, i ) => {
          !Object.values( el ).some( element => element == '' || element == [] ) && this.tags.push( [ el.name, el.compare, el.value ] );
        } );
        this.$emit( 'advancedListchange', this.tags )
        this.dialogVisible = false;
      },
      btn2( num ) {
        this.gjArr.splice( num - 1, 1 );
        this.gjResultarr.splice( num - 1, 1 );
        this.gjsxcount--;
      },

      handleClose( tag ) {
        let num = this.tags.indexOf( tag );
        this.tags.splice( num, 1 );
        this.gjArr.splice( num, 1 );
        this.gjResultarr.splice( num, 1 );
        this.gjsxcount--;
      },
      yiji( num ) {
        this.data7.forEach( element => {
          element.name == this.gjResultarr[ num - 1 ].name &&
            ( this.gjArr[ num - 1 ] = element );
        } );
        this.$forceUpdate()
        console.log( this.gjArr );
      }
    },
    mounted() {}
  };
</script>
<style lang='less'>
  .advanced .el-dialog--small {
    width: 464px;
  }

  .advanced .el-tag--small {
    margin-right: 3px;
    border: none;
    line-height: 24px;
    max-width: 100px;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
    position: relative;
    padding-right: 16px;
    color: #333;
    background: #e0e9fa;
  }

  .advanced .el-select .el-tag {
    max-width: 130px;
    text-overflow: ellipsis;
    white-space: nowrap;
    overflow: hidden;
  }

  .advanced .el-input--small .el-input__inner {
    height: 28px !important;
    line-height: 28px !important;
    background: #fff;
    border-radius: 4px;
    border: 1px solid #eaeaea;
    padding-left: 8px;
    font-size: 12px;
    width: 78px;
  }

  .advanced .el-tag--small .el-icon-close {
    position: absolute;
    top: 5px;
    right: 0;
  }

  .advanced .el-select .el-input {
    width: 78px !important;
  }

  .lineFilter .el-input--small .el-input__inner {
    width: 191px !important;
  }

  .comDatapart_nav .lineFilter .el-select .el-input {
    width: 191px !important;
  }

  .advanced .el-input--small .el-input__inner {
    width: 78px;
  }

  .lineinput input {
    width: 191px !important;
  }

  .advanced {
    .el-select__tags {
      top: 92%;
      height: 28px;
      overflow: hidden;
    }
  }
</style>

<style scoped>
  .advancedFilter-btn {
    cursor: pointer;
    display: inline-block;
    width: 89px;
    height: 28px;
    background: #fff;
    border-radius: 4px;
    border: 1px solid rgba(43, 116, 237, 0.24);
    font-size: 12px;
    font-family: PingFangSC-Regular;
    font-weight: 400;
    color: #2b74ed;
    line-height: 28px;
    text-align: center;
    margin-right: 12px;
  }

  .el-input,
  .el-input--suffix .el-input__inner,
  .el-select .el-input__inner {
    width: 78px;
    height: 28px !important;
  }

  .el-input {
    width: 78px !important;
  }

  .addFilter {
    font-size: 12px;
    font-family: PingFangSC-Regular;
    font-weight: 400;
    color: #333;
    line-height: 17px;
    cursor: pointer;
    padding: 16px;
  }

  .line {
    width: 379px;
    height: 49px;
    line-height: 49px;
    background-color: #f5f7fb;
    position: relative;
    padding-left: 8px;
    margin-bottom: 8px;
  }
</style>
<template>
  <div style="width:800px">
    <el-table :data="tableDatas" border row-key="id" align="left" @selection-change="handleSelectionChange" :cell-style="cellStyle">
      <el-table-column type="selection" width="55">
      </el-table-column>
      <el-table-column v-for="(item, index) in col" :key="`col_${index}`" :prop="item.prop" :label="item.label"></el-table-column>
    </el-table>
    <button @click="con">唧唧复唧唧</button>
  </div>
</template>
<script>
  import Sortable from "sortablejs";

  export default {
    props: [ 'col', 'tableDatas' ],
    data() {
      return {
        multipleSelection: []
      };
    },
    mounted() {
      this.rowDrop();
    },
    methods: {
      //行拖拽
      rowDrop() {
        const tbody = document.querySelector( ".el-table__body-wrapper tbody" );
        const _this = this;
        Sortable.create( tbody, {
          onEnd( {
            newIndex,
            oldIndex
          } ) {
            const currRow = _this.tableDatas.splice( oldIndex, 1 )[ 0 ];
            _this.tableDatas.splice( newIndex, 0, currRow );
          }
        } );
      },
      //列拖拽
      con() {
        console.log( this.multipleSelection );
      },
      handleSelectionChange( val ) {
        this.multipleSelection = val;
      },
      cellStyle( {
        rowIndex,
        columnIndex,
        row,
        column
      } ) {
        // console.log( rowIndex, columnIndex, row, column )
        if( column ) {}
        // console.log( data )
      }
    }
  };
</script>
<style scoped>
</style>
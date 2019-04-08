<template>
  <div>
    <Tree :data6="msg" @getNewarr="getNewarr"></Tree>
  </div>
</template>
<script>
  import Tree from "./tree.vue"
  export default {
    data() {
      return {

        msg: [ {
            id: 1,
            label: "人力资源",
            children: [ {
                id: 3,
                label: "人力资源规划"
              },
              {
                id: 4,
                label: "招聘"
              },
              {
                id: 5,
                label: "薪酬"
              },
              {
                id: 6,
                label: "绩效"
              },
              {
                id: 7,
                label: "培训"
              }
            ]
          },
          {
            id: 2,
            label: "财务",
            children: [ {
                id: 8,
                label: "财务分析"
              },
              {
                id: 9,
                label: "管理会计"
              }
            ]
          }
        ],
        aaaa: [],
      }
    },
    methods: {
      getNewarr( value ) {
        console.log( value, '1111111', )
      },
    },
    mounted() {
      let obj = {
        a: '',
        b: '',
        c: []
      }
      this.aaaa.push( obj )
      console.log( this.aaaa, 'this.aaaa' )
    },
    components: {
      Tree
    }
  }
</script>
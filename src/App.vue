<template>
  <div id="app">
    <table class="app-table">
      <thead>
        <tr>
          <td
            v-for="item in tableHeadData"
            :key="item.lable"
            @click="handleTdClick(item)"
          >
            {{ item.name }}
          </td>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(item, index) in tableData"
          :key="index"
          @click="highLight(index)"
          :class="{ active: activeIndex === index }"
        >
          <td>{{ item.id }}</td>
          <td>{{ item.age }}</td>
          <td>{{ item.name }}</td>
          <td>{{ item.address }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      // 高亮索引
      activeIndex: '',
      // 是否升序
      isAsce: false,
      // 表格头部数据
      tableHeadData: [
        { lable: 'id', name: '序列' },
        { lable: 'age', name: '年龄' },
        { lable: 'name', name: '姓名' },
        { lable: 'address', name: '地址' },
      ],
      // 表格数据
      tableData: [
        {
          id: 1,
          age: 9,
          name: '王小虎',
          address: '上海市普陀区金沙江路 1518 弄',
        },
        {
          id: 2,
          age: 8,
          name: '王小虎',
          address: '上海市普陀区金沙江路 1517 弄',
        },
        {
          id: 3,
          age: 12,
          name: '王小虎',
          address: '上海市普陀区金沙江路 1519 弄',
        },
        {
          id: 4,
          age: 21,
          name: '王小虎',
          address: '上海市普陀区金沙江路 1516 弄',
        },
      ],
    }
  },
  methods: {
    /**
     * 点击列头，根据不同列头进行升序，降序
     */
    handleTdClick({ lable }) {
      this.isAsce = !this.isAsce
      this.publicSort(lable)
    },
    /**
     * 对序列进行排序
     */
    publicSort(lable) {
      // 升序
      if (this.isAsce) {
        if (lable === 'id') {
          this.tableData.sort((a, b) => {
            return a.id - b.id
          })
        } else if (lable === 'age') {
          this.tableData.sort((a, b) => {
            return a.age - b.age
          })
        } else if (lable === 'name') {
          this.tableData.sort((a, b) => {
            return a.name - b.name
          })
        } else {
          this.tableData.sort((a, b) => {
            return a.address - b.address
          })
        }
      } else {
        // 降序
        if (lable === 'id') {
          this.tableData.sort((a, b) => {
            return b.id - a.id
          })
        } else if (lable === 'age') {
          this.tableData.sort((a, b) => {
            return b.age - a.age
          })
        } else if (lable === 'name') {
          this.tableData.sort((a, b) => {
            return b.name - a.name
          })
        } else {
          this.tableData.sort((a, b) => {
            return b.address - a.address
          })
        }
      }
    },
    /**
     * 点击td使该行高亮
     */
    highLight(index) {
      this.activeIndex = index
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.active {
  background-color: red;
}
</style>

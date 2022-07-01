<template>
  <div id="app">
    <table class="tb">
      <tr>
        <th><input type="checkbox" v-model="isAll" />全选</th>
        <th>商品</th>
        <th>单价</th>
        <th>数量</th>
        <th>小记</th>
        <th>操作</th>
      </tr>
      <!-- 循环渲染的元素tr -->
      <tr v-for="item in list" :key="item.id">
        <td>
          <input type="checkbox" v-model="item.checked" />
        </td>
        <td>{{ item.name }}</td>
        <td>{{ item.price }}</td>
        <td>
          <button>-</button>
          <input style="width: 50px" type="number" v-model="item.count" />
          <button>+</button>
        </td>
        <td>{{ item.price * item.count }}</td>
        <td><button @click="del(item.id)">删除</button></td>
      </tr>

      <tr v-if="list.length === 0">
        <td colspan="6">没有数据咯~</td>
      </tr>
    </table>
    <br />
    <button @click="delChecked">删除选中商品</button>
    <button @click="clear">清理购物车</button>
    <br />
    <div style="margin-top: 20px">
      <h2>统计</h2>
      <p>已经选中商品件数</p>
      <p>总价</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      list: [
        {
          id: 1,
          name: '经典儿童文学彩图青少版八十天环游地球中学生语文教学大纲',
          price: '12.6',
          count: 0,
          checked: false,
        },

        {
          id: 2,
          name: '贴纸书 3-6岁',
          price: '24.8',
          count: 0,
          checked: false,
        },
        {
          id: 3,
          name: '唐诗三百首+成语故事全2册',
          price: '29.8',
          count: 0,
          checked: false,
        },
      ],
    };
  },
  methods: {
    del(id) {
      // 删除按钮 - 得到索引, 删除数组里元素
      const index = this.list.findIndex((item) => item.id === id);
      this.list.splice(index, 1);
    },
    // 删除选中状态的数据
    delChecked() {
      this.list = this.list.filter((item) => item.checked === false);
    },
    clear() {
      this.list = [];
    },
  },
  // 全选框
  computed: {
    isAll: {
      get() {
        return this.list.length === 0
          ? false
          : this.list.every((item) => item.checked);
      },
      set(val) {
        this.list.forEach((item) => (item.checked = val));
      },
    },
  },
};
</script>

<style>
#app {
  width: 1000px;
  margin: 10px auto;
}

.tb {
  border-collapse: collapse;
  width: 800px;
}

.tb th {
  background-color: #0094ff;
  color: white;
}

.tb td,
.tb th {
  padding: 5px;
  border: 1px solid black;
  text-align: center;
}

.add {
  padding: 5px;
  border: 1px solid black;
  margin-bottom: 10px;
}
</style>

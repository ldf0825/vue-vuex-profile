<template>
  <div class="hello">
    <!-- 个人经验 -->
    <div>
      <h4 class="mb-2">个人经验</h4>
      <table class="table">
        <thead>
          <tr>
            <th>公司</th>
            <th>工作内容</th>
            <th>工作时间</th>
            <th />
          </tr>
        </thead>
        <tbody>
          <tr v-for="(exp,index) in experience" :key="index">
            <td>{{exp.company}}</td>
            <td>{{exp.title}}</td>
            <td>{{exp.from}}~ {{exp.to ? exp.to:"至今"}}</td>
            <td>
              <button @click.prevent="handleExpDelete(index)">删除</button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    experience: Array
  },
  methods: {
    handleExpDelete(id) {
      //   this.$axios.delete("/api/profile/experience" + id).then(res => {
      //     console.log(res.data);
      //     this.experience = res.data.experience;
      //   });

      //注册事件
      this.$emit("handleDashDelete", id);
    }
  },
  created() {
    console.log(this.experience);
  }
};
</script>


<style scoped>
</style>

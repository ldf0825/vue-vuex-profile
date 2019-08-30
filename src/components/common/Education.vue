<template>
  <div class="hello">
    <!-- 个人经验 -->
    <div>
      <h4 class="mb-2">教育经历</h4>
      <table class="table">
        <thead>
          <tr>
            <th>学校</th>
            <th>学历</th>
            <th>专业</th>
            <th>工作时间</th>
            <th />
          </tr>
        </thead>
        <tbody>
          <tr v-for="(edu,index) in education" :key="index">
            <td>{{edu.school}}</td>
            <td>{{edu.degree}}</td>
            <td>{{edu.fieldofstudy}}</td>
            <td>{{edu.from}}~ {{edu.to ? edu.to:"在校"}}</td>
            <td>
              <button @click.prevent="handleEduDelete(index)">删除</button>
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
    education: Array
  },
  methods: {
    handleEduDelete(id) {
      //   this.$axios.delete("/api/profile/experience" + id).then(res => {
      //     console.log(res.data);
      //     this.experience = res.data.experience;
      //   });

      //注册事件
      this.$emit("handleEduDelete", id);
    }
  },
  created() {
    console.log(this.experience);
  }
};
</script>


<style scoped>
</style>

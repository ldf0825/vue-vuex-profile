<template>
  <div class="dashboard">
    <div class="container">
      <div class="row">
        <div class="col-md-12">
          <h1 class="display-4">仪表盘</h1>
          <p v-if="user != null  && profile != null" class="lead text-muted">
            Welcome
            <router-link :to="'/profile/' + profile.handle">{{user.name}}</router-link>
          </p>
          <div v-if="profile">
            <ProfileActived />
          </div>
          <div v-else>
            <p>没有任何您的个人信息，请添加！！！</p>
            <!-- 跳转到添加个人信息的组件中 -->
            <router-link to="/createprofile" class="btn btn-lg btn-info">添加个人信息</router-link>
          </div>

          <!-- 删除 -->
          <div v-if="profile != null" style="margin-bottom: 60px;">
            <button class="btn btn-danger" @click="deleteClick">删除当前账户</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from "vuex";
import ProfileActived from "../components/common/ProfileActived";
export default {
  name: "dashboard",
  computed: mapGetters(["user"]),
  components: { ProfileActived },
  data() {
    return {
      profile: null
    };
  },
  created() {
    this.getProfileData();
  },
  methods: {
    getProfileData() {
      this.$axios
        .get("/api/profile")
        .then(res => {
          //如果请求到数据，那么赋值给profile
          this.profile = res.data;

          //存到vuex
          this.$store.dispatch("setProfileAsync", res.data);
        })
        .catch(err => {
          this.$store.dispatch("setProfileAsync", null);
          this.profile = null;
        });
    },
    deleteClick() {
      this.$axios
        .delete("/api/profile")
        .then(res => {
          this.profile = null;

          this.$store.dispatch("setIsLoginAsync", false);
          this.$store.dispatch("setProfileAsync", null);
          this.$store.dispatch("setUserAsync", null);

          this.$router.push("/login");
        })
        .catch(err => {
          alert(err.response.data);
        });
    }
  }
};
</script>


<style scoped>
</style>

<template>
  <div>
    <el-container class="container">
      <el-aside
        width="200px"
        style="background-color: rgb(238, 241, 246); height: 1000px"
      >
        <el-menu :default-openeds="['1', '2', '3']">
          <el-submenu index="1">
            <template #title><i class="el-icon-date"></i>授课管理</template>
            <el-menu-item index="1-1" @click="changePage('TeachingTable')"
              >授课表</el-menu-item
            >
            <el-menu-item index="1-2" @click="changePage('StudentList')"
              >选课学生</el-menu-item
            >
          </el-submenu>

          <el-submenu index="2">
            <template #title><i class="el-icon-edit"></i>指导管理</template>
            <el-menu-item index="2-1" @click="changePage('LecturerManageAdvisor')"
              >指导管理</el-menu-item
            >
          </el-submenu>

          <el-submenu index="3">
            <template #title><i class="el-icon-user"></i>个人信息</template>
            <el-menu-item index="3-1" @click="changePage('LecturerChangeInfo')"
              >修改信息</el-menu-item
            >
            <el-menu-item index="3-2" @click="changePage('LecturerChangePwd')"
              >修改密码</el-menu-item
            >
          </el-submenu>
        </el-menu>
      </el-aside>

      <el-container>
        <el-header style="text-align: right; font-size: 12px">
          <el-dropdown>
            <i class="el-icon-setting" style="margin-right: 15px"></i>
            <template #dropdown>
              <el-dropdown-menu>
                <el-dropdown-item @click="changePage('Login')"
                  >退出登录</el-dropdown-item
                >
              </el-dropdown-menu>
            </template>
          </el-dropdown>
          <span id="lect_name"> {{ lect_name }} </span>
        </el-header>

        <el-main>
          <router-view></router-view>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>


<script>
import axios from "axios";
import { useRouter } from "vue-router";
export default {
  data() {
    return {
      lect_name: "",
    };
  },

  mounted() {
    let that = this;
    axios
      .post("http://muzi.fun:4455/class_selection/lect/getById", {
        lect_id: this.$root.lect_id,
      })
      .then(function (response) {
        that.lect_name = response.data.lect_name;
      })
      .catch(function (error) {
        console.log(error);
      });
  },
  setup() {
    const router = useRouter();
    const changePage = (destination) => {
      router.push({
        name: destination,
      });
    };
    return {
      changePage,
    };
  },
};
</script>

<style>
#Frame {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.el-header {
  background-color: #b3c0d1;
  color: #333;
  line-height: 60px;
}

.el-aside {
  color: #333;
}

html,
body {
  height: 100%;
}

.container {
  height: 100%;
}
</style>
<template>
  <div>
    <el-container class="container">
      <el-aside
        width="200px"
        style="background-color: rgb(238, 241, 246); height: 1000px"
      >
        <el-menu :default-openeds="['1', '2', '3']">
          <el-submenu index="1">
            <template #title><i class="el-icon-date"></i>指导管理</template>
            <el-menu-item index="1-1" @click="changePage('Selection')"
              >选课</el-menu-item
            >
            <el-menu-item index="1-2" @click="changePage('Drop')"
              >退课</el-menu-item
            >
            <el-menu-item index="1-3" @click="changePage('History')"
              >历年课表</el-menu-item
            >
          </el-submenu>

          <el-submenu index="2">
            <template #title><i class="el-icon-edit"></i>指导管理</template>
            <el-menu-item index="2-1" @click="changePage('StudentManageAdvisor')"
              >指导管理</el-menu-item>
          </el-submenu>

          <el-submenu index="3">
            <template #title><i class="el-icon-user"></i>个人信息</template>
            <el-menu-item index="3-1" @click="changePage('QueryScore')"
              >成绩查询</el-menu-item
            >
            <el-menu-item index="3-2" @click="changePage('StudentChangeInfo')"
              >修改信息</el-menu-item
            >
            <el-menu-item index="3-3" @click="changePage('StudentChangePwd')"
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
          <span id="stud_name"> {{ stud_name }} </span>
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
      stud_name: "",
    };
  },

  mounted() {
    let that = this
     axios
      .post("http://muzi.fun:4455/class_selection/student/getById", {
        stud_id: this.$root.stud_id,
      })
      .then(function (response) {
        that.stud_name = response.data.stud_name;
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
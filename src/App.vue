<script setup lang="ts">
import { onMounted, ref } from 'vue'
import userApi from './api/user'
import orgApi from './api/org'

let user = ref<any>()
let org = ref<any>()
import OrgTree from './components/OrgTree.vue'
import UserTable from './components/UserTable.vue'
let activeName = ref<string>('member');
onMounted(() => {
  userApi.query({}).then((res) => (user.value = res))
  orgApi.query().then((res) => (org.value = res))
})
</script>

<template>
  <div class="page-container">
    <el-tabs v-model="activeName" >
      <el-tab-pane label="成员管理" name="member">
        <el-row>
          <el-col class="left-box" :span="6">
            <org-tree></org-tree>
          </el-col>
          <el-col :span="18">
            <user-table></user-table>
          </el-col>
        </el-row>
      </el-tab-pane>
      <el-tab-pane label="团队管理" name="team">团队管理</el-tab-pane>
      <el-tab-pane label="职位维护" name="position">职位维护</el-tab-pane>
    </el-tabs>
  </div>
</template>

<style lang="scss" scoped>
.page-container {
  height: 100%;
  padding: 0 15px;
  .left-box {
    border-right: 1px solid #eee;
  }
  :deep() {
    .el-tabs,
    .el-row,
    .el-tab-pane {
      height: 100%;
    }
    .el-tabs__header {
      margin: 0;
    }
    .el-tabs__content {
      height: calc(100% - 40px);
    }
  }
}
</style>
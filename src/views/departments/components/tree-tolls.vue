<template>
  <el-row style="width: 100%" type="flex">
    <el-col>{{ treeNode.name }}</el-col>
    <el-col :span="5">
      <el-row type="flex">
        <el-col>{{ treeNode.manager }}</el-col>
        <el-col>
          <el-dropdown>
            <span class="el-dropdown-link">
              操作<i class="el-icon-arrow-down el-icon--right"></i>
            </span>
            <el-dropdown-menu slot="dropdown">
              <el-dropdown-item @click.native="$emit('add', treeNdse)">添加部门</el-dropdown-item>
              <template v-if="!isRoot">
                <el-dropdown-item @click="$emit(edit)">编辑部门</el-dropdown-item>
                <el-dropdown-item @click.native="onRemove">删除部门</el-dropdown-item>
              </template>
            </el-dropdown-menu>
          </el-dropdown>
        </el-col>
      </el-row>
    </el-col>
  </el-row>
</template>
<script>
import { delDeptsApi } from '@/api/department'
export default {
  name: 'TreeTools',
  components: {},
  props: {
    treeNode: {
      type: Object,
      required: true,
    },
    isRoot: {
      type: Boolean,
      default: false
    }
  },
  created() {},
  data() {
    return {}
  },
  methods: {
    async onRemove() {
      try {
        await this.$confirm('此操作将永久删除该部门，是否继续?', '提示', {
          confirmButtonText: '继续',
          ConstantSourceNode: '取消',
          type: 'warning',
        })
        await delDeptsApi(this.treeNode.id)
        this.$message.success('删除成功')
        this.$emit('remove')
      } catch (error) {
        
      }
    }
  },
  computed: {},
  watch: {},
  mounted() {},
  beforeDestroy() {},
}
</script>
<style lang="less" scoped></style>

<template>
    <div class="container">  
        <el-row>
            <el-col :span="4">
                <el-button type="primary" size="small" @click="addNewCase">新增</el-button>
                <el-button type="primary" size="small" @click="deleteCase">删除</el-button>
                <el-button type="primary" size="small" @click="runCase">运行</el-button>
            </el-col>
        </el-row>
        <el-row>
            <el-col :span="24">
            <el-table
            :data="tableData"
            height="250"
            border
            @selection-change="handleSelectionChange"
            style="width: 100%">
                <el-table-column
                    type="selection"
                    >
                </el-table-column>
                <el-table-column
                    prop="code"
                    label="序列号"
                    >
                    </el-table-column>
                <el-table-column
                    prop="name"
                    label="名称"
                    >
                </el-table-column>
                <el-table-column
                    prop="desc"
                    label="描述"
                     width="280">
                </el-table-column>
                <el-table-column
                    prop="owner"
                    label="维护人"
                     width="80">
                </el-table-column>
                <el-table-column
                    prop="status"
                    label="状态">
                    <el-tag
                    type="success"
                    effect="dark">
                    成功
                </el-tag>
                </el-table-column>
                <el-table-column
                    fixed="right"
                    label="操作"
                    width="100">
                    <template slot-scope="scope">
                        <el-button @click="handleClick(scope.row)" type="text" size="small">查看</el-button>
                        <el-button type="text" size="small">编辑</el-button>
                    </template>
                </el-table-column>
            </el-table>
            </el-col>
        </el-row>
        

        <div>
            <el-dialog
            :visible.sync="dialogVisible"
            width="85%"
            :before-close="handleClose"
            center>
            <div>
                <Terminal />
            </div>
            <span slot="footer" class="dialog-footer">
                <el-button type="primary" @click="dialogVisible = false">中断运行</el-button>
            </span>
            </el-dialog>
        </div>
    </div>
</template>
<script>
  import Terminal from '@/components/Terminal'
  export default {
    name: 'TestCaseList',
    components: {
        Terminal
    },
   
    data() {
      return {
        dialogVisible: false,
        tableData: [
            {
            code: '1',
            name: '自动化测试1',
            desc: '上海',
            
            }
        ]
      }
    },
     methods: {
      handleClick(row) {
          console.log(row)
          if(this.dialogVisible === true) {
              this.dialogVisible = false;
          }else{
              this.dialogVisible=true;
          }
      }
    },
  }
</script>
<style lang="scss" scoped>
.el-row {
    margin-bottom: 20px;
    &:last-child {
        margin-bottom: 0;
    }
}
.el-col {
    border-radius: 4px; 
}
</style>
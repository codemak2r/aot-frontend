<template>
    <!-- 新建测试用例 -->
    <div>
        <el-dialog title="新建用例" :visible.sync="dialogFormVisible">
        <el-form :model="form">
            <el-form-item label="名称" :label-width="formLabelWidth">
            <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="活动区域" :label-width="formLabelWidth">
            <el-select v-model="form.region" placeholder="请选择活动区域">
                <el-option label="区域一" value="shanghai"></el-option>
                <el-option label="区域二" value="beijing"></el-option>
            </el-select>
            </el-form-item>
        </el-form>
        <div slot="footer" class="dialog-footer">
            <el-button @click="dialogFormVisible = false">保存</el-button>
            <el-button type="primary" @click="dialogFormVisible = false">取消</el-button>
        </div>
        </el-dialog>
    </div>
</template>
<script>
export default {
    name: 'NewTestCase', 
    form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
    },
    formLabelWidth: '120px',
    dialogFormVisible: false
}
</script>
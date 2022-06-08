<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="收入,支出,转账" prop="changeName">
      <el-input v-model="dataForm.changeName" placeholder="收入,支出,转账"></el-input>
    </el-form-item>
    <el-form-item label="备注" prop="description">
      <el-input v-model="dataForm.description" placeholder="备注"></el-input>
    </el-form-item>
    <el-form-item label="创建人ID" prop="createrId">
      <el-input v-model="dataForm.createrId" placeholder="创建人ID"></el-input>
    </el-form-item>
    <el-form-item label="创建人" prop="creater">
      <el-input v-model="dataForm.creater" placeholder="创建人"></el-input>
    </el-form-item>
    <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="修改人ID" prop="updaterId">
      <el-input v-model="dataForm.updaterId" placeholder="修改人ID"></el-input>
    </el-form-item>
    <el-form-item label="修改人" prop="updater">
      <el-input v-model="dataForm.updater" placeholder="修改人"></el-input>
    </el-form-item>
    <el-form-item label="修改时间" prop="updateTime">
      <el-input v-model="dataForm.updateTime" placeholder="修改时间"></el-input>
    </el-form-item>
    <el-form-item label="是否显示[1-显示，0-不显示]" prop="showStatus">
      <el-input v-model="dataForm.showStatus" placeholder="是否显示[1-显示，0-不显示]"></el-input>
    </el-form-item>
    <el-form-item label="排序" prop="sort">
      <el-input v-model="dataForm.sort" placeholder="排序"></el-input>
    </el-form-item>
    <el-form-item label="检索首字母" prop="firstLetter">
      <el-input v-model="dataForm.firstLetter" placeholder="检索首字母"></el-input>
    </el-form-item>
    </el-form>
    <span slot="footer" class="dialog-footer">
      <el-button @click="visible = false">取消</el-button>
      <el-button type="primary" @click="dataFormSubmit()">确定</el-button>
    </span>
  </el-dialog>
</template>

<script>
  export default {
    data () {
      return {
        visible: false,
        dataForm: {
          id: 0,
          changeName: '',
          description: '',
          createrId: '',
          creater: '',
          createTime: '',
          updaterId: '',
          updater: '',
          updateTime: '',
          showStatus: '',
          sort: '',
          firstLetter: ''
        },
        dataRule: {
          changeName: [
            { required: true, message: '收入,支出,转账不能为空', trigger: 'blur' }
          ],
          description: [
            { required: true, message: '备注不能为空', trigger: 'blur' }
          ],
          createrId: [
            { required: true, message: '创建人ID不能为空', trigger: 'blur' }
          ],
          creater: [
            { required: true, message: '创建人不能为空', trigger: 'blur' }
          ],
          createTime: [
            { required: true, message: '创建时间不能为空', trigger: 'blur' }
          ],
          updaterId: [
            { required: true, message: '修改人ID不能为空', trigger: 'blur' }
          ],
          updater: [
            { required: true, message: '修改人不能为空', trigger: 'blur' }
          ],
          updateTime: [
            { required: true, message: '修改时间不能为空', trigger: 'blur' }
          ],
          showStatus: [
            { required: true, message: '是否显示[1-显示，0-不显示]不能为空', trigger: 'blur' }
          ],
          sort: [
            { required: true, message: '排序不能为空', trigger: 'blur' }
          ],
          firstLetter: [
            { required: true, message: '检索首字母不能为空', trigger: 'blur' }
          ]
        }
      }
    },
    methods: {
      init (id) {
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/base/change/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.changeName = data.change.changeName
                this.dataForm.description = data.change.description
                this.dataForm.createrId = data.change.createrId
                this.dataForm.creater = data.change.creater
                this.dataForm.createTime = data.change.createTime
                this.dataForm.updaterId = data.change.updaterId
                this.dataForm.updater = data.change.updater
                this.dataForm.updateTime = data.change.updateTime
                this.dataForm.showStatus = data.change.showStatus
                this.dataForm.sort = data.change.sort
                this.dataForm.firstLetter = data.change.firstLetter
              }
            })
          }
        })
      },
      // 表单提交
      dataFormSubmit () {
        this.$refs['dataForm'].validate((valid) => {
          if (valid) {
            this.$http({
              url: this.$http.adornUrl(`/base/change/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'changeName': this.dataForm.changeName,
                'description': this.dataForm.description,
                'createrId': this.dataForm.createrId,
                'creater': this.dataForm.creater,
                'createTime': this.dataForm.createTime,
                'updaterId': this.dataForm.updaterId,
                'updater': this.dataForm.updater,
                'updateTime': this.dataForm.updateTime,
                'showStatus': this.dataForm.showStatus,
                'sort': this.dataForm.sort,
                'firstLetter': this.dataForm.firstLetter
              })
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.$message({
                  message: '操作成功',
                  type: 'success',
                  duration: 1500,
                  onClose: () => {
                    this.visible = false
                    this.$emit('refreshDataList')
                  }
                })
              } else {
                this.$message.error(data.msg)
              }
            })
          }
        })
      }
    }
  }
</script>

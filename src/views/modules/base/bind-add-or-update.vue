<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="支付方式ID" prop="payId">
      <el-input v-model="dataForm.payId" placeholder="支付方式ID"></el-input>
    </el-form-item>
    <el-form-item label="支付方式名称" prop="payName">
      <el-input v-model="dataForm.payName" placeholder="支付方式名称"></el-input>
    </el-form-item>
    <el-form-item label="账号ID" prop="cardId">
      <el-input v-model="dataForm.cardId" placeholder="账号ID"></el-input>
    </el-form-item>
    <el-form-item label="账号名称" prop="cardName">
      <el-input v-model="dataForm.cardName" placeholder="账号名称"></el-input>
    </el-form-item>
    <el-form-item label="账号" prop="cardNumber">
      <el-input v-model="dataForm.cardNumber" placeholder="账号"></el-input>
    </el-form-item>
    <el-form-item label="账号所属人ID" prop="cardholderId">
      <el-input v-model="dataForm.cardholderId" placeholder="账号所属人ID"></el-input>
    </el-form-item>
    <el-form-item label="账号所属人" prop="cardholder">
      <el-input v-model="dataForm.cardholder" placeholder="账号所属人"></el-input>
    </el-form-item>
    <el-form-item label="绑定关系" prop="bindRelation">
      <el-input v-model="dataForm.bindRelation" placeholder="绑定关系"></el-input>
    </el-form-item>
    <el-form-item label="绑定时间" prop="bindTime">
      <el-input v-model="dataForm.bindTime" placeholder="绑定时间"></el-input>
    </el-form-item>
    <el-form-item label="解绑时间" prop="unbindTime">
      <el-input v-model="dataForm.unbindTime" placeholder="解绑时间"></el-input>
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
          payId: '',
          payName: '',
          cardId: '',
          cardName: '',
          cardNumber: '',
          cardholderId: '',
          cardholder: '',
          bindRelation: '',
          bindTime: '',
          unbindTime: '',
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
          payId: [
            { required: true, message: '支付方式ID不能为空', trigger: 'blur' }
          ],
          payName: [
            { required: true, message: '支付方式名称不能为空', trigger: 'blur' }
          ],
          cardId: [
            { required: true, message: '账号ID不能为空', trigger: 'blur' }
          ],
          cardName: [
            { required: true, message: '账号名称不能为空', trigger: 'blur' }
          ],
          cardNumber: [
            { required: true, message: '账号不能为空', trigger: 'blur' }
          ],
          cardholderId: [
            { required: true, message: '账号所属人ID不能为空', trigger: 'blur' }
          ],
          cardholder: [
            { required: true, message: '账号所属人不能为空', trigger: 'blur' }
          ],
          bindRelation: [
            { required: true, message: '绑定关系不能为空', trigger: 'blur' }
          ],
          bindTime: [
            { required: true, message: '绑定时间不能为空', trigger: 'blur' }
          ],
          unbindTime: [
            { required: true, message: '解绑时间不能为空', trigger: 'blur' }
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
              url: this.$http.adornUrl(`/base/bind/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.payId = data.bind.payId
                this.dataForm.payName = data.bind.payName
                this.dataForm.cardId = data.bind.cardId
                this.dataForm.cardName = data.bind.cardName
                this.dataForm.cardNumber = data.bind.cardNumber
                this.dataForm.cardholderId = data.bind.cardholderId
                this.dataForm.cardholder = data.bind.cardholder
                this.dataForm.bindRelation = data.bind.bindRelation
                this.dataForm.bindTime = data.bind.bindTime
                this.dataForm.unbindTime = data.bind.unbindTime
                this.dataForm.description = data.bind.description
                this.dataForm.createrId = data.bind.createrId
                this.dataForm.creater = data.bind.creater
                this.dataForm.createTime = data.bind.createTime
                this.dataForm.updaterId = data.bind.updaterId
                this.dataForm.updater = data.bind.updater
                this.dataForm.updateTime = data.bind.updateTime
                this.dataForm.showStatus = data.bind.showStatus
                this.dataForm.sort = data.bind.sort
                this.dataForm.firstLetter = data.bind.firstLetter
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
              url: this.$http.adornUrl(`/base/bind/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'payId': this.dataForm.payId,
                'payName': this.dataForm.payName,
                'cardId': this.dataForm.cardId,
                'cardName': this.dataForm.cardName,
                'cardNumber': this.dataForm.cardNumber,
                'cardholderId': this.dataForm.cardholderId,
                'cardholder': this.dataForm.cardholder,
                'bindRelation': this.dataForm.bindRelation,
                'bindTime': this.dataForm.bindTime,
                'unbindTime': this.dataForm.unbindTime,
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

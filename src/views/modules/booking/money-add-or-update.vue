<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="银行卡ID" prop="cardId">
      <el-input v-model="dataForm.cardId" placeholder="银行卡ID"></el-input>
    </el-form-item>
    <el-form-item label="银行卡名称" prop="cardName">
      <el-input v-model="dataForm.cardName" placeholder="银行卡名称"></el-input>
    </el-form-item>
    <el-form-item label="银行卡卡号" prop="cardNumber">
      <el-input v-model="dataForm.cardNumber" placeholder="银行卡卡号"></el-input>
    </el-form-item>
    <el-form-item label="交易金额" prop="changeMoney">
      <el-input v-model="dataForm.changeMoney" placeholder="交易金额"></el-input>
    </el-form-item>
    <el-form-item label="交易类型表ID" prop="changeId">
      <el-input v-model="dataForm.changeId" placeholder="交易类型表ID"></el-input>
    </el-form-item>
    <el-form-item label="交易类型名称" prop="changeName">
      <el-input v-model="dataForm.changeName" placeholder="交易类型名称"></el-input>
    </el-form-item>
    <el-form-item label="支付类型ID" prop="payId">
      <el-input v-model="dataForm.payId" placeholder="支付类型ID"></el-input>
    </el-form-item>
    <el-form-item label="支付类型名称" prop="payName">
      <el-input v-model="dataForm.payName" placeholder="支付类型名称"></el-input>
    </el-form-item>
    <el-form-item label="交易人ID" prop="memberId">
      <el-input v-model="dataForm.memberId" placeholder="交易人ID"></el-input>
    </el-form-item>
    <el-form-item label="交易人" prop="memberName">
      <el-input v-model="dataForm.memberName" placeholder="交易人"></el-input>
    </el-form-item>
    <el-form-item label="交易内容" prop="thing">
      <el-input v-model="dataForm.thing" placeholder="交易内容"></el-input>
    </el-form-item>
    <el-form-item label="交易时间" prop="changeTime">
      <el-input v-model="dataForm.changeTime" placeholder="交易时间"></el-input>
    </el-form-item>
    <el-form-item label="备注" prop="description">
      <el-input v-model="dataForm.description" placeholder="备注"></el-input>
    </el-form-item>
    <el-form-item label="创建人ID" prop="createrId">
      <el-input v-model="dataForm.createrId" placeholder="创建人ID"></el-input>
    </el-form-item>
    <el-form-item label="创建人名字" prop="creater">
      <el-input v-model="dataForm.creater" placeholder="创建人名字"></el-input>
    </el-form-item>
    <el-form-item label="创建时间" prop="createTime">
      <el-input v-model="dataForm.createTime" placeholder="创建时间"></el-input>
    </el-form-item>
    <el-form-item label="修改人ID" prop="updaterId">
      <el-input v-model="dataForm.updaterId" placeholder="修改人ID"></el-input>
    </el-form-item>
    <el-form-item label="修改人名字" prop="updater">
      <el-input v-model="dataForm.updater" placeholder="修改人名字"></el-input>
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
          cardId: '',
          cardName: '',
          cardNumber: '',
          changeMoney: '',
          changeId: '',
          changeName: '',
          payId: '',
          payName: '',
          memberId: '',
          memberName: '',
          thing: '',
          changeTime: '',
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
          cardId: [
            { required: true, message: '银行卡ID不能为空', trigger: 'blur' }
          ],
          cardName: [
            { required: true, message: '银行卡名称不能为空', trigger: 'blur' }
          ],
          cardNumber: [
            { required: true, message: '银行卡卡号不能为空', trigger: 'blur' }
          ],
          changeMoney: [
            { required: true, message: '交易金额不能为空', trigger: 'blur' }
          ],
          changeId: [
            { required: true, message: '交易类型表ID不能为空', trigger: 'blur' }
          ],
          changeName: [
            { required: true, message: '交易类型名称不能为空', trigger: 'blur' }
          ],
          payId: [
            { required: true, message: '支付类型ID不能为空', trigger: 'blur' }
          ],
          payName: [
            { required: true, message: '支付类型名称不能为空', trigger: 'blur' }
          ],
          memberId: [
            { required: true, message: '交易人ID不能为空', trigger: 'blur' }
          ],
          memberName: [
            { required: true, message: '交易人不能为空', trigger: 'blur' }
          ],
          thing: [
            { required: true, message: '交易内容不能为空', trigger: 'blur' }
          ],
          changeTime: [
            { required: true, message: '交易时间不能为空', trigger: 'blur' }
          ],
          description: [
            { required: true, message: '备注不能为空', trigger: 'blur' }
          ],
          createrId: [
            { required: true, message: '创建人ID不能为空', trigger: 'blur' }
          ],
          creater: [
            { required: true, message: '创建人名字不能为空', trigger: 'blur' }
          ],
          createTime: [
            { required: true, message: '创建时间不能为空', trigger: 'blur' }
          ],
          updaterId: [
            { required: true, message: '修改人ID不能为空', trigger: 'blur' }
          ],
          updater: [
            { required: true, message: '修改人名字不能为空', trigger: 'blur' }
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
              url: this.$http.adornUrl(`/booking/money/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.cardId = data.money.cardId
                this.dataForm.cardName = data.money.cardName
                this.dataForm.cardNumber = data.money.cardNumber
                this.dataForm.changeMoney = data.money.changeMoney
                this.dataForm.changeId = data.money.changeId
                this.dataForm.changeName = data.money.changeName
                this.dataForm.payId = data.money.payId
                this.dataForm.payName = data.money.payName
                this.dataForm.memberId = data.money.memberId
                this.dataForm.memberName = data.money.memberName
                this.dataForm.thing = data.money.thing
                this.dataForm.changeTime = data.money.changeTime
                this.dataForm.description = data.money.description
                this.dataForm.createrId = data.money.createrId
                this.dataForm.creater = data.money.creater
                this.dataForm.createTime = data.money.createTime
                this.dataForm.updaterId = data.money.updaterId
                this.dataForm.updater = data.money.updater
                this.dataForm.updateTime = data.money.updateTime
                this.dataForm.showStatus = data.money.showStatus
                this.dataForm.sort = data.money.sort
                this.dataForm.firstLetter = data.money.firstLetter
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
              url: this.$http.adornUrl(`/booking/money/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'cardId': this.dataForm.cardId,
                'cardName': this.dataForm.cardName,
                'cardNumber': this.dataForm.cardNumber,
                'changeMoney': this.dataForm.changeMoney,
                'changeId': this.dataForm.changeId,
                'changeName': this.dataForm.changeName,
                'payId': this.dataForm.payId,
                'payName': this.dataForm.payName,
                'memberId': this.dataForm.memberId,
                'memberName': this.dataForm.memberName,
                'thing': this.dataForm.thing,
                'changeTime': this.dataForm.changeTime,
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

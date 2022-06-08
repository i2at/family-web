<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="账号名称" prop="cardName">
      <el-input v-model="dataForm.cardName" placeholder="账号名称"></el-input>
    </el-form-item>
    <el-form-item label="账号" prop="cardNumber">
      <el-input v-model="dataForm.cardNumber" placeholder="账号"></el-input>
    </el-form-item>

    <el-form-item label="所属人" prop="cardholderId">
      <!-- <el-input v-model="dataForm.cardholderId" placeholder="持卡人ID"></el-input> -->
      <el-select v-model="dataForm.cardholderId" placeholder="请选择">
        <el-option
          v-for="item in members"
          :key="item.id"
          :label="item.memberName"
          :value="item.id">
        </el-option>
      </el-select>
    </el-form-item>

    <!-- <el-form-item label="账号所属人" prop="cardholder">
      <el-input v-model="dataForm.cardholder" placeholder="账号所属人"></el-input>
    </el-form-item> -->
    
    <el-form-item label="办理时间" prop="cardTime">
      <el-date-picker
          v-model="dataForm.cardTime"
          type="datetime"
          placeholder="选择日期时间"
          align="right"
          :picker-options="pickerOptions"
          value-format="yyyy-MM-dd HH:mm:ss">
      </el-date-picker>
    </el-form-item>

    <el-form-item label="办理地址" prop="cardAddress">
      <el-input v-model="dataForm.cardAddress" placeholder="办理地址"></el-input>
    </el-form-item>
    <el-form-item label="预留电话" prop="cardTelephone">
      <el-input v-model="dataForm.cardTelephone" placeholder="预留电话"></el-input>
    </el-form-item>
    <el-form-item label="备注" prop="description">
      <el-input v-model="dataForm.description" placeholder="备注"></el-input>
    </el-form-item>
    <!-- <el-form-item label="创建人ID" prop="createrId">
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
    </el-form-item> -->
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
        members:[],
        visible: false,
        dataForm: {
          id: 0,
          cardName: '',
          cardNumber: '',
          cardholderId: '',
          cardholder: '',
          cardTime: '',
          cardAddress: '',
          cardTelephone: '',
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
            { required: false, message: '账号所属人不能为空', trigger: 'blur' }
          ],
          cardTime: [
            { required: false, message: '办理时间不能为空', trigger: 'blur' }
          ],
          cardAddress: [
            { required: false, message: '办理地址不能为空', trigger: 'blur' }
          ],
          cardTelephone: [
            { required: false, message: '预留电话不能为空', trigger: 'blur' }
          ],
          description: [
            { required: false, message: '备注不能为空', trigger: 'blur' }
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
        },
        pickerOptions: {
          shortcuts: [{
            text: '今天',
            onClick(picker) {
              picker.$emit('pick', new Date());
            }
          }, {
            text: '昨天',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit('pick', date);
            }
          }, {
            text: '一周前',
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit('pick', date);
            }
          }]
        },
      }
    },
    methods: {
      init (id) {
        this.getMembers();
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/base/card/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.cardName = data.card.cardName
                this.dataForm.cardNumber = data.card.cardNumber
                this.dataForm.cardholderId = data.card.cardholderId
                this.dataForm.cardholder = data.card.cardholder
                this.dataForm.cardTime = data.card.cardTime
                this.dataForm.cardAddress = data.card.cardAddress
                this.dataForm.cardTelephone = data.card.cardTelephone
                this.dataForm.description = data.card.description
                this.dataForm.createrId = data.card.createrId
                this.dataForm.creater = data.card.creater
                this.dataForm.createTime = data.card.createTime
                this.dataForm.updaterId = data.card.updaterId
                this.dataForm.updater = data.card.updater
                this.dataForm.updateTime = data.card.updateTime
                this.dataForm.showStatus = data.card.showStatus
                this.dataForm.sort = data.card.sort
                this.dataForm.firstLetter = data.card.firstLetter
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
              url: this.$http.adornUrl(`/base/card/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'cardName': this.dataForm.cardName,
                'cardNumber': this.dataForm.cardNumber,
                'cardholderId': this.dataForm.cardholderId,
                'cardholder': this.dataForm.cardholder,
                'cardTime': this.dataForm.cardTime,
                'cardAddress': this.dataForm.cardAddress,
                'cardTelephone': this.dataForm.cardTelephone,
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
      },
      getMembers(){
        //发送请求获取当前节点最新的数据
      this.$http({
        url: this.$http.adornUrl('/base/card/memberVos'),
        method: "get"
      })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          this.members=data.data;
        })
        .catch(() => {});
      }
    }
  }
</script>

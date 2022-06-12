<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="100px">
    <!-- <el-form-item label="银行卡ID" prop="cardId">
      <el-input v-model="dataForm.cardId" placeholder="银行卡ID"></el-input>
    </el-form-item> -->

    <el-form-item label="账号名称" prop="cardId">
      <el-select v-model="dataForm.cardId" placeholder="请选择" @change="selectChanged">
        <el-option
          v-for="item in cards"
          :key="item.id"
          :label="item.cardName"
          :value="item.id">
        </el-option>
      </el-select>
    </el-form-item>

    <!-- <el-form-item label="银行卡名称" prop="cardName">
      <el-input v-model="dataForm.cardName" placeholder="银行卡名称"></el-input>
    </el-form-item> -->
    <el-form-item label="账号" prop="cardNumber">
      <el-input v-model="dataForm.cardNumber" placeholder="银行卡卡号"></el-input>
    </el-form-item>
    <el-form-item label="账号所属人" prop="cardUser">
      <el-input v-model="dataForm.cardUser" placeholder="银行卡持卡人"></el-input>
    </el-form-item>

    <!-- <el-form-item label="银行卡初始金额" prop="cardInitMoney">
      <el-input v-model="dataForm.cardInitMoney" placeholder="银行卡初始金额"></el-input>
    </el-form-item> -->

    <!-- <el-form-item label="银行卡盘点金额" prop="cardCheckMoney">
      <el-input v-model="dataForm.cardCheckMoney" placeholder="银行卡盘点金额"></el-input>
    </el-form-item> -->
    <el-form-item label="银行卡实际金额" prop="cardRealMoney">
      <el-input v-model="dataForm.cardRealMoney" placeholder="银行卡实际金额"></el-input>
    </el-form-item>

    <!-- <el-form-item label="盘点状态" prop="statisticsStatus">
      <el-input v-model="dataForm.statisticsStatus" placeholder="盘点状态"></el-input>
    </el-form-item> -->
    <!-- <el-form-item label="盘点差异金额" prop="statisticsMoney">
      <el-input v-model="dataForm.statisticsMoney" placeholder="盘点差异金额"></el-input>
    </el-form-item> -->

    <!-- <el-form-item label="盘点人ID" prop="statisticsUserId">
      <el-input v-model="dataForm.statisticsUserId" placeholder="盘点人ID"></el-input>
    </el-form-item>
    <el-form-item label="盘点人" prop="statisticsUser">
      <el-input v-model="dataForm.statisticsUser" placeholder="盘点人"></el-input>
    </el-form-item> -->

    <!-- <el-form-item label="盘点时间" prop="statisticsTime">
      <el-input v-model="dataForm.statisticsTime" placeholder="盘点时间"></el-input>
    </el-form-item> -->

     <!-- <el-form-item label="备注" prop="description">
      <el-input v-model="dataForm.description" placeholder="备注"></el-input>
    </el-form-item> -->

    <!--<el-form-item label="创建人ID" prop="createrId">
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
        cards:[],
        visible: false,
        dataForm: {
          id: 0,
          cardId: '',
          cardName: '',
          cardNumber: '',
          cardUser: '',
          cardInitMoney: '',
          cardCheckMoney: '',
          cardRealMoney: '',
          statisticsStatus: '',
          statisticsMoney: '',
          statisticsUserId: '',
          statisticsUser: '',
          statisticsTime: '',
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
          cardUser: [
            { required: true, message: '银行卡持卡人不能为空', trigger: 'blur' }
          ],
          cardInitMoney: [
            { required: true, message: '银行卡初始金额不能为空', trigger: 'blur' }
          ],
          cardCheckMoney: [
            { required: true, message: '银行卡盘点金额不能为空', trigger: 'blur' }
          ],
          cardRealMoney: [
            { required: true, message: '银行卡实际金额不能为空', trigger: 'blur' }
          ],
          statisticsStatus: [
            { required: true, message: '盘点状态不能为空', trigger: 'blur' }
          ],
          statisticsMoney: [
            { required: true, message: '盘点差异金额不能为空', trigger: 'blur' }
          ],
          statisticsUserId: [
            { required: true, message: '盘点人ID不能为空', trigger: 'blur' }
          ],
          statisticsUser: [
            { required: true, message: '盘点人不能为空', trigger: 'blur' }
          ],
          statisticsTime: [
            { required: true, message: '盘点时间不能为空', trigger: 'blur' }
          ],
          description: [
            { required: false, message: '备注不能为空', trigger: 'blur' }
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
        this.getCards();
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/booking/statistics/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.cardId = data.statistics.cardId
                this.dataForm.cardName = data.statistics.cardName
                this.dataForm.cardNumber = data.statistics.cardNumber
                this.dataForm.cardUser = data.statistics.cardUser
                this.dataForm.cardInitMoney = data.statistics.cardInitMoney
                this.dataForm.cardCheckMoney = data.statistics.cardCheckMoney
                this.dataForm.cardRealMoney = data.statistics.cardRealMoney
                this.dataForm.statisticsStatus = data.statistics.statisticsStatus
                this.dataForm.statisticsMoney = data.statistics.statisticsMoney
                this.dataForm.statisticsUserId = data.statistics.statisticsUserId
                this.dataForm.statisticsUser = data.statistics.statisticsUser
                this.dataForm.statisticsTime = data.statistics.statisticsTime
                this.dataForm.description = data.statistics.description
                this.dataForm.createrId = data.statistics.createrId
                this.dataForm.creater = data.statistics.creater
                this.dataForm.createTime = data.statistics.createTime
                this.dataForm.updaterId = data.statistics.updaterId
                this.dataForm.updater = data.statistics.updater
                this.dataForm.updateTime = data.statistics.updateTime
                this.dataForm.showStatus = data.statistics.showStatus
                this.dataForm.sort = data.statistics.sort
                this.dataForm.firstLetter = data.statistics.firstLetter
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
              url: this.$http.adornUrl(`/booking/statistics/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'cardId': this.dataForm.cardId,
                'cardName': this.dataForm.cardName,
                'cardNumber': this.dataForm.cardNumber,
                'cardUser': this.dataForm.cardUser,
                'cardInitMoney': this.dataForm.cardInitMoney,
                'cardCheckMoney': this.dataForm.cardCheckMoney,
                'cardRealMoney': this.dataForm.cardRealMoney,
                'statisticsStatus': this.dataForm.statisticsStatus,
                'statisticsMoney': this.dataForm.statisticsMoney,
                'statisticsUserId': this.dataForm.statisticsUserId,
                'statisticsUser': this.dataForm.statisticsUser,
                'statisticsTime': this.dataForm.statisticsTime,
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
      getCards(){
        //发送请求获取当前节点最新的数据
        this.$http({
          url: this.$http.adornUrl('/booking/statistics/cardsList'),
          method: "get"
        })
          .then(({ data }) => {
            //请求成功
            // console.log("要回显的数据", data);
            this.cards=data.data;
          })
        .catch(() => {});
      },
      selectChanged(){
        //发送请求获取当前节点最新的数据
        this.$http({
          url: this.$http.adornUrl(`/base/card/info/${this.dataForm.cardId}`),
          method: "get"
        })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          // alert(data.card.cardName);
          this.dataForm.cardNumber=data.card.cardNumber;
          // this.dataForm.cardholderId=data.card.cardholderId;
          this.dataForm.cardUser=data.card.cardholder;
          // this.cards=data.card;
        })
        .catch(() => {});
      }
    }
  }
</script>

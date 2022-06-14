<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="100px">

    <!-- <el-form-item label="分类ID" prop="categoryId">
      <el-input v-model="dataForm.categoryId" placeholder="分类ID"></el-input>
    </el-form-item>
    <el-form-item label="分类名称" prop="categoryName">
      <el-input v-model="dataForm.categoryName" placeholder="分类名称"></el-input>
    </el-form-item> -->

    <el-form-item label="商品" prop="categoryId">
      <el-select v-model="dataForm.categoryId" placeholder="请选择" filterable clearable>
        <el-option
          v-for="item in categorys"
          :key="item.catId"
          :label="item.name"
          :value="item.catId">
        </el-option>
      </el-select>
    </el-form-item>


    <!-- <el-form-item label="交易类型表ID" prop="changeId">
      <el-input v-model="dataForm.changeId" placeholder="交易类型表ID"></el-input>
    </el-form-item>
    <el-form-item label="收入,支出" prop="changeName">
      <el-input v-model="dataForm.changeName" placeholder="收入,支出"></el-input>
    </el-form-item> -->

    <el-form-item label="类型" prop="changeId">
      <el-select v-model="dataForm.changeId" placeholder="请选择" clearable>
        <el-option
          v-for="item in changes"
          :key="item.id"
          :label="item.changeName"
          :value="item.id">
        </el-option>
      </el-select>
    </el-form-item>

    <el-form-item label="交易类型" prop="bindId">
      <el-select v-model="dataForm.bindId" placeholder="请选择" @change="selectChanged" filterable clearable>
        <el-option
          v-for="item in binds"
          :key="item.id"
          :label="item.payName"
          :value="item.id">
        </el-option>
      </el-select>
    </el-form-item>

    <!-- <el-form-item label="支付类型表ID" prop="payId">
      <el-input v-model="dataForm.payId" placeholder="支付类型表ID"></el-input>
    </el-form-item> -->
    <el-form-item label="交易途径" prop="payName">
      <el-input v-model="dataForm.payName" placeholder="微信,支付宝,银行卡" :disabled="true" filterable clearable></el-input>
    </el-form-item>

    <!-- <el-form-item label="银行卡管理表ID" prop="cardId">
      <el-input v-model="dataForm.cardId" placeholder="银行卡管理表ID"></el-input>
    </el-form-item> -->
    <el-form-item label="账号名称" prop="cardName">
      <el-input v-model="dataForm.cardName" placeholder="银行卡名称" :disabled="true"></el-input>
    </el-form-item>
    <el-form-item label="账号" prop="cardNumber">
      <el-input v-model="dataForm.cardNumber" placeholder="银行卡账号" :disabled="true"></el-input>
    </el-form-item>
    <el-form-item label="账号所属人" prop="cardHolder">
      <el-input v-model="dataForm.cardHolder" placeholder="银行卡持卡人" :disabled="true"></el-input>
    </el-form-item>

    <!-- <el-form-item label="单位表ID" prop="unitId">
      <el-input v-model="dataForm.unitId" placeholder="单位表ID"></el-input>
    </el-form-item>
    <el-form-item label="克,千克,斤" prop="unitName">
      <el-input v-model="dataForm.unitName" placeholder="克,千克,斤"></el-input>
    </el-form-item> -->

    <el-form-item label="单位" prop="unitId">
      <el-select v-model="dataForm.unitId" placeholder="请选择" filterable clearable>
        <el-option
          v-for="item in units"
          :key="item.id"
          :label="item.unitName"
          :value="item.id">
        </el-option>
      </el-select>
    </el-form-item>

    <!-- <el-form-item label="历史价格表ID" prop="priceId">
      <el-input v-model="dataForm.priceId" placeholder="历史价格表ID"></el-input>
    </el-form-item> -->
    <el-form-item label="价格" prop="price">
      <el-input v-model="dataForm.price" placeholder="请输入正整数或小数，最多6位小数，历史价格" oninput="if(isNaN(value)) { value = null } if(value.indexOf('.')>0){value=value.slice(0,value.indexOf('.')+8)}"
 maxLength='9'></el-input>
    </el-form-item>
    <el-form-item label="数量" prop="quantity">
      <el-input-number :min="0.1" :step="0.1" v-model="dataForm.quantity" placeholder="请输入正整数或小数，最多6位小数，支出数量,购买数量,使用数量"  oninput="if(isNaN(value)) { value = null } if(value.indexOf('.')>0){value=value.slice(0,value.indexOf('.')+8)}"
 maxLength='9'></el-input-number>
    </el-form-item>

    <!-- <el-form-item label="单条记录总金额" prop="totalAmount">
      <el-input v-model="dataForm.totalAmount" placeholder="单条记录总金额"></el-input>
    </el-form-item> -->


    <!-- <el-form-item label="交易人ID" prop="payUserId">
      <el-input v-model="dataForm.payUserId" placeholder="交易人ID"></el-input>
    </el-form-item>
    <el-form-item label="交易人" prop="payUser">
      <el-input v-model="dataForm.payUser" placeholder="交易人"></el-input>
    </el-form-item> -->

    <el-form-item label="交易人" prop="payUserId">
      <el-select v-model="dataForm.payUserId" placeholder="请选择" filterable clearable>
        <el-option
          v-for="item in payUsers"
          :key="item.id"
          :label="item.memberName"
          :value="item.id">
        </el-option>
      </el-select>
    </el-form-item>

    <!-- <el-form-item label="交易时间" prop="payTime">
      <el-input v-model="dataForm.payTime" placeholder="交易时间"></el-input>
    </el-form-item> -->

   <el-form-item label="交易时间" prop="payTime">
      <el-date-picker
          v-model="dataForm.payTime"
          type="datetime"
          placeholder="选择日期时间"
          align="right"
          :picker-options="pickerOptions"
          value-format="yyyy-MM-dd HH:mm:ss">
      </el-date-picker>
    </el-form-item>



    <el-form-item label="备注" prop="description">
      <el-input v-model="dataForm.description" placeholder="备注"></el-input>
    </el-form-item>

    <!-- <el-form-item label="创建人ID" prop="createrId">
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
        payUsers:[],
        units:[],
        changes:[],
        categorys:[],
        visible: false,
        dataForm: {
          id: 0,
          categoryId: '',
          categoryName: '',
          changeId: '',
          changeName: '',
          payId: '',
          payName: '',
          cardId: '',
          cardName: '',
          cardNumber: '',
          cardHolder: '',
          unitId: '',
          unitName: '',
          priceId: '',
          price: '',
          quantity: '',
          totalAmount: '',
          payUserId: '',
          payUser: '',
          payTime: '',
          description: '',
          createrId: '',
          creater: '',
          createTime: '',
          updaterId: '',
          updater: '',
          updateTime: '',
          showStatus: '',
          sort: '',
          firstLetter: '',
          bindId:''
        },
        dataRule: {
          categoryId: [
            { required: true, message: '分类ID不能为空', trigger: 'blur' }
          ],
          categoryName: [
            { required: true, message: '分类名称不能为空', trigger: 'blur' }
          ],
          changeId: [
            { required: true, message: '交易类型表ID不能为空', trigger: 'blur' }
          ],
          changeName: [
            { required: true, message: '收入,支出不能为空', trigger: 'blur' }
          ],
          payId: [
            { required: true, message: '支付类型表ID不能为空', trigger: 'blur' }
          ],
          payName: [
            { required: true, message: '微信,支付宝,银行卡不能为空', trigger: 'blur' }
          ],
          cardId: [
            { required: true, message: '银行卡管理表ID不能为空', trigger: 'blur' }
          ],
          cardName: [
            { required: true, message: '银行卡名称不能为空', trigger: 'blur' }
          ],
          cardNumber: [
            { required: true, message: '银行卡账号不能为空', trigger: 'blur' }
          ],
          cardHolder: [
            { required: true, message: '银行卡持卡人不能为空', trigger: 'blur' }
          ],
          unitId: [
            { required: true, message: '单位表ID不能为空', trigger: 'blur' }
          ],
          unitName: [
            { required: true, message: '克,千克,斤不能为空', trigger: 'blur' }
          ],
          priceId: [
            { required: true, message: '历史价格表ID不能为空', trigger: 'blur' }
          ],
          price: [
            { required: true, message: '历史价格不能为空', trigger: 'blur' }
          ],
          quantity: [
            { required: true, message: '支出数量,购买数量,使用数量不能为空', trigger: 'blur' }
          ],
          totalAmount: [
            { required: true, message: '单条记录总金额不能为空', trigger: 'blur' }
          ],
          payUserId: [
            { required: true, message: '交易人ID不能为空', trigger: 'blur' }
          ],
          payUser: [
            { required: true, message: '交易人不能为空', trigger: 'blur' }
          ],
          payTime: [
            { required: true, message: '交易时间不能为空', trigger: 'blur' }
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
        }
      }
    },
    methods: {
      init (id) {
        this.getPayUsers();
        this.getUnits();
        this.getBinds();
        this.getChanges();
        this.getCategorys();
        this.dataForm.id = id || 0
        this.visible = true
        this.$nextTick(() => {
          this.$refs['dataForm'].resetFields()
          if (this.dataForm.id) {
            this.$http({
              url: this.$http.adornUrl(`/booking/record/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.categoryId = data.record.categoryId
                this.dataForm.categoryName = data.record.categoryName
                this.dataForm.changeId = data.record.changeId
                this.dataForm.changeName = data.record.changeName
                this.dataForm.payId = data.record.payId
                this.dataForm.payName = data.record.payName
                this.dataForm.cardId = data.record.cardId
                this.dataForm.cardName = data.record.cardName
                this.dataForm.cardNumber = data.record.cardNumber
                this.dataForm.cardHolder = data.record.cardHolder
                this.dataForm.unitId = data.record.unitId
                this.dataForm.unitName = data.record.unitName
                this.dataForm.priceId = data.record.priceId
                this.dataForm.price = data.record.price
                this.dataForm.quantity = data.record.quantity
                this.dataForm.totalAmount = data.record.totalAmount
                this.dataForm.payUserId = data.record.payUserId
                this.dataForm.payUser = data.record.payUser
                this.dataForm.payTime = data.record.payTime
                this.dataForm.description = data.record.description
                this.dataForm.createrId = data.record.createrId
                this.dataForm.creater = data.record.creater
                this.dataForm.createTime = data.record.createTime
                this.dataForm.updaterId = data.record.updaterId
                this.dataForm.updater = data.record.updater
                this.dataForm.updateTime = data.record.updateTime
                this.dataForm.showStatus = data.record.showStatus
                this.dataForm.sort = data.record.sort
                this.dataForm.firstLetter = data.record.firstLetter
                this.dataForm.bindId = data.record.bindId
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
              url: this.$http.adornUrl(`/booking/record/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'categoryId': this.dataForm.categoryId,
                'categoryName': this.dataForm.categoryName,
                'changeId': this.dataForm.changeId,
                'changeName': this.dataForm.changeName,
                'payId': this.dataForm.payId,
                'payName': this.dataForm.payName,
                'cardId': this.dataForm.cardId,
                'cardName': this.dataForm.cardName,
                'cardNumber': this.dataForm.cardNumber,
                'cardHolder': this.dataForm.cardHolder,
                'unitId': this.dataForm.unitId,
                'unitName': this.dataForm.unitName,
                'priceId': this.dataForm.priceId,
                'price': this.dataForm.price,
                'quantity': this.dataForm.quantity,
                'totalAmount': this.dataForm.totalAmount,
                'payUserId': this.dataForm.payUserId,
                'payUser': this.dataForm.payUser,
                'payTime': this.dataForm.payTime,
                'description': this.dataForm.description,
                'createrId': this.dataForm.createrId,
                'creater': this.dataForm.creater,
                'createTime': this.dataForm.createTime,
                'updaterId': this.dataForm.updaterId,
                'updater': this.dataForm.updater,
                'updateTime': this.dataForm.updateTime,
                'showStatus': this.dataForm.showStatus,
                'sort': this.dataForm.sort,
                'firstLetter': this.dataForm.firstLetter,
                'bindId': this.dataForm.bindId
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
      getCategorys(){
        //发送请求获取当前节点最新的数据
      this.$http({
        url: this.$http.adornUrl('/booking/record/categoryVos'),
        method: "get"
      })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          this.categorys=data.data;
        })
        .catch(() => {});
      },
      getChanges(){
        //发送请求获取当前节点最新的数据
      this.$http({
        url: this.$http.adornUrl('/booking/record/changeVos'),
        method: "get"
      })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          this.changes=data.data;
        })
        .catch(() => {});
      },
      getBinds(){
        //发送请求获取当前节点最新的数据
      this.$http({
        url: this.$http.adornUrl('/booking/record/bindVos'),
        method: "get"
      })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          this.binds=data.data;
        })
        .catch(() => {});
      },
      selectChanged(){
        //发送请求获取当前节点最新的数据
        this.$http({
          url: this.$http.adornUrl(`/booking/record/bind/info/${this.dataForm.bindId}`),
          method: "get"
        })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data.data.payName);
          this.dataForm.payName=data.data.payName;
          this.dataForm.cardName=data.data.cardName;
          this.dataForm.cardNumber=data.data.cardNumber;
          this.dataForm.cardHolder=data.data.cardholder;

        })
        .catch(() => {});
      },
      getUnits(){
        //发送请求获取当前节点最新的数据
      this.$http({
        url: this.$http.adornUrl('/booking/record/unitVos'),
        method: "get"
      })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          this.units=data.data;
        })
        .catch(() => {});
      },
      getPayUsers(){
        //发送请求获取当前节点最新的数据
      this.$http({
        url: this.$http.adornUrl('/booking/record/payUserVos'),
        method: "get"
      })
        .then(({ data }) => {
          //请求成功
          // console.log("要回显的数据", data);
          this.payUsers=data.data;
        })
        .catch(() => {});
      }
    }
  }
</script>

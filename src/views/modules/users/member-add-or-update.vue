<template>
  <el-dialog
    :title="!dataForm.id ? '新增' : '修改'"
    :close-on-click-modal="false"
    :visible.sync="visible">
    <el-form :model="dataForm" :rules="dataRule" ref="dataForm" @keyup.enter.native="dataFormSubmit()" label-width="80px">
    <el-form-item label="昵称" prop="nickName">
      <el-input v-model="dataForm.nickName" placeholder="昵称"></el-input>
    </el-form-item>
    <el-form-item label="姓名" prop="memberName">
      <el-input v-model="dataForm.memberName" placeholder="姓名"></el-input>
    </el-form-item>
    <el-form-item label="年龄" prop="age">
      <el-input v-model.number="dataForm.age" placeholder="年龄"></el-input>
    </el-form-item>

    <el-form-item label="性别" prop="sex">
      <template>
        <el-radio v-model="dataForm.sex" label="0">男</el-radio>
        <el-radio v-model="dataForm.sex" label="1">女</el-radio>
      </template>
    </el-form-item>
    
    <el-form-item label="行业" prop="industry">
      <el-input v-model="dataForm.industry" placeholder="行业"></el-input>
    </el-form-item>

    <el-form-item label="出生日期" prop="birthDate">
      <!-- <el-input v-model="dataForm.birthDate" placeholder="出生日期"></el-input> -->
      <el-date-picker
          v-model="dataForm.birthDate"
          type="datetime"
          placeholder="选择日期时间"
          align="right"
          :picker-options="pickerOptions"
          value-format="yyyy-MM-dd HH:mm:ss">
      </el-date-picker>
    </el-form-item>

    <el-form-item label="生日" prop="birthday">
      <el-date-picker
        v-model="dataForm.birthday"
        align="right"
        type="datetime"
        placeholder="选择日期"
        :picker-options="pickerOptions"
        value-format="yyyy-MM-dd HH:mm:ss">
      </el-date-picker>
    </el-form-item>

    <el-form-item label="出生地址" prop="birthAddress">
      <el-input v-model="dataForm.birthAddress" placeholder="出生地址"></el-input>
    </el-form-item>
    <el-form-item label="现住址" prop="address">
      <el-input v-model="dataForm.address" placeholder="现住址"></el-input>
    </el-form-item>
    <el-form-item label="电话" prop="tel">
      <el-input v-model.number="dataForm.tel" placeholder="电话"></el-input>
    </el-form-item>
    <el-form-item label="座机" prop="mobile">
      <el-input v-model.number="dataForm.mobile" placeholder="座机"></el-input>
    </el-form-item>
    <el-form-item label="邮箱" prop="email">
      <el-input v-model="dataForm.email" placeholder="邮箱"></el-input>
    </el-form-item>
    <el-form-item label="微信号" prop="weixin">
      <el-input v-model="dataForm.weixin" placeholder="微信号"></el-input>
    </el-form-item>
    <el-form-item label="QQ" prop="qq">
      <el-input v-model.number="dataForm.qq" placeholder="QQ"></el-input>
    </el-form-item>
    <el-form-item label="抖音号" prop="douyin">
      <el-input v-model="dataForm.douyin" placeholder="抖音号"></el-input>
    </el-form-item>
    <el-form-item label="微博" prop="weibo">
      <el-input v-model="dataForm.weibo" placeholder="微博"></el-input>
    </el-form-item>
    <el-form-item label="爱好" prop="hobby">
      <el-input v-model="dataForm.hobby" placeholder="爱好"></el-input>
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
      var checkAge = (rule, value, callback) => {
        if (value !== ""){
          if (!Number.isInteger(value)) {
            callback(new Error('请输入数字值'));
          }
          if(value < rule.max_age){
            callback(new Error('必须年满18岁'));
          }
          if(value > rule.min_age){
              callback(new Error('必须小于100岁'));
          } else {
              callback();
          }
        }
      };
      var checkName = (rule, value, cb) => {
        //验证名字的正则表达式
        const regName = /^([\\u4e00-\\u9fa5]{1,20}|[a-zA-Z\\.\\s]{1,20})$/;
        if (regName.test(value)) {
          //正确的名字
          return cb();
        }
        cb(new Error("请输入正确的名字"));
      };
      var checkMobile = (rule, value, callback) => {
        if (value !== "") {
            var reg = /^1[3-9]\d{9}$/;
            if (!reg.test(value)) {
              callback(new Error("请输入有效的手机号码"));
            }
          }
      };
      var checkEmail = (rule, value, cb) => {
          //验证邮箱的正则表达式
          const regEmail = /^\w+([-+.]\w+)*@\w+([-.]\w+)*\.\w+([-.]\w+)*$/;
          if (value !== ""){
            if (regEmail.test(value)) {
              //合法的邮箱
              return cb();
            }
            cb(new Error("请输入合法的邮箱"));
          }
      };
      var checkQq = (rule, value, callback) => {
        if (value !== ""){
          if (!Number.isInteger(value)) {
            callback(new Error('请输入数字值'));
          }else {
              callback();
          }
        }
      };
      return {
        visible: false,
        dataForm: {
          id: 0,
          nickName: '',
          memberName: '',
          age: '',
          sex: '',
          industry: '',
          birthDate: '',
          birthday: '',
          birthAddress: '',
          address: '',
          tel: '',
          mobile: '',
          email: '',
          weixin: '',
          qq: '',
          douyin: '',
          weibo: '',
          hobby: '',
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
          nickName: [
            { required: false, message: '昵称不能为空', trigger: 'blur' }
          ],
          memberName: [
            { required: true, message: '姓名不能为空', trigger: 'blur' },
            // {
            //   validator: checkName,
            //   min: 2,
            //   max: 5,
            //   message: "请输入正确的名字",
            //   trigger: "blur",
            // }
          ],
          age: [
            { required: false, message: '年龄不能为空', trigger: 'blur' },
            // {max_age:18, min_age:100, validator: checkAge, trigger: 'blur'}
          ],
          sex: [
            { required: true, message: '性别不能为空', trigger: 'blur' }
          ],
          industry: [
            { required: false, message: '行业不能为空', trigger: 'blur' }
          ],
          birthDate: [
            { required: false, message: '出生日期不能为空', trigger: 'blur' }
          ],
          birthday: [
            { required: false, message: '生日不能为空', trigger: 'blur' }
          ],
          birthAddress: [
            { required: false, message: '出生地址不能为空', trigger: 'blur' }
          ],
          address: [
            { required: false, message: '现住址不能为空', trigger: 'blur' }
          ],
          tel: [
            { required: false, message: '电话不能为空', trigger: 'blur' },
            // {
            //   validator: checkMobile,
            //   min: 11,
            //   max: 11,
            //   message: "手机号格式错误",
            //   trigger: "blur",
            // }
          ],
          mobile: [
            { required: false, message: '座机不能为空', trigger: 'blur' },
            // {
            //   validator: checkMobile,
            //   min: 11,
            //   max: 11,
            //   message: "手机号格式错误",
            //   trigger: "blur",
            // }
          ],
          email: [
            { required: false, message: '邮箱不能为空', trigger: 'blur' },
            // {
            //   validator: checkEmail,
            //   min: 9,
            //   max: 18,
            //   message: "邮箱格式错误",
            //   trigger: "blur",
            // }
          ],
          weixin: [
            { required: false, message: '微信号不能为空', trigger: 'blur' }
          ],
          qq: [
            { required: false, message: 'QQ必须为数字值', trigger: 'blur' },
            // { validator: checkQq, trigger: 'blur'}
          ],
          douyin: [
            { required: false, message: '抖音号不能为空', trigger: 'blur' }
          ],
          weibo: [
            { required: false, message: '微博不能为空', trigger: 'blur' }
          ],
          hobby: [
            { required: false, message: '爱好不能为空', trigger: 'blur' }
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
              url: this.$http.adornUrl(`/users/member/info/${this.dataForm.id}`),
              method: 'get',
              params: this.$http.adornParams()
            }).then(({data}) => {
              if (data && data.code === 0) {
                this.dataForm.nickName = data.member.nickName
                this.dataForm.memberName = data.member.memberName
                this.dataForm.age = data.member.age
                this.dataForm.sex = data.member.sex
                this.dataForm.industry = data.member.industry
                this.dataForm.birthDate = data.member.birthDate
                this.dataForm.birthday = data.member.birthday
                this.dataForm.birthAddress = data.member.birthAddress
                this.dataForm.address = data.member.address
                this.dataForm.tel = data.member.tel
                this.dataForm.mobile = data.member.mobile
                this.dataForm.email = data.member.email
                this.dataForm.weixin = data.member.weixin
                this.dataForm.qq = data.member.qq
                this.dataForm.douyin = data.member.douyin
                this.dataForm.weibo = data.member.weibo
                this.dataForm.hobby = data.member.hobby
                this.dataForm.description = data.member.description
                this.dataForm.createrId = data.member.createrId
                this.dataForm.creater = data.member.creater
                this.dataForm.createTime = data.member.createTime
                this.dataForm.updaterId = data.member.updaterId
                this.dataForm.updater = data.member.updater
                this.dataForm.updateTime = data.member.updateTime
                this.dataForm.showStatus = data.member.showStatus
                this.dataForm.sort = data.member.sort
                this.dataForm.firstLetter = data.member.firstLetter
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
              url: this.$http.adornUrl(`/users/member/${!this.dataForm.id ? 'save' : 'update'}`),
              method: 'post',
              data: this.$http.adornData({
                'id': this.dataForm.id || undefined,
                'nickName': this.dataForm.nickName,
                'memberName': this.dataForm.memberName,
                'age': this.dataForm.age,
                'sex': this.dataForm.sex,
                'industry': this.dataForm.industry,
                'birthDate': this.dataForm.birthDate,
                'birthday': this.dataForm.birthday,
                'birthAddress': this.dataForm.birthAddress,
                'address': this.dataForm.address,
                'tel': this.dataForm.tel,
                'mobile': this.dataForm.mobile,
                'email': this.dataForm.email,
                'weixin': this.dataForm.weixin,
                'qq': this.dataForm.qq,
                'douyin': this.dataForm.douyin,
                'weibo': this.dataForm.weibo,
                'hobby': this.dataForm.hobby,
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

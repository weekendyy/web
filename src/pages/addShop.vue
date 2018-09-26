<template>
	<div class="addShop">
		<el-form :model="ruleForm2" status-icon :rules="rules2" ref="ruleForm2" label-width="100px" class="demo-ruleForm">
			<el-row>
				<el-col :offset="6" :span="10">
				  <el-form-item label="店铺名称" prop="pass">
				    <el-input type="password" v-model="ruleForm2.pass" autocomplete="off"></el-input>
				  </el-form-item>
				</el-col>
			</el-row>

			<el-row>
				<el-col :offset="6" :span="10">
				  <el-form-item label="手机号码" prop="age">
				    <el-input v-model.number="ruleForm2.age"></el-input>
				  </el-form-item>
				</el-col>
			</el-row>
		  <el-form-item>
		    <el-button type="primary" @click="submitForm('ruleForm2')">提交</el-button>
		    <el-button @click="resetForm('ruleForm2')">重置</el-button>
		  </el-form-item>
		</el-form>
  </div>
</template>

<script>
    export default {
    	data(){
    		var checkAge = (rule, value, callback) => {
	        if (!value) {
	          return callback(new Error('年龄不能为空'));
	        }
	        setTimeout(() => {
	          if (!Number.isInteger(value)) {
	            callback(new Error('请输入数字值'));
	          } else {
	            if (value < 18) {
	              callback(new Error('必须年满18岁'));
	            } else {
	              callback();
	            }
	          }
	        }, 1000);
	      };
	      var validatePass = (rule, value, callback) => {
	        if (value === '') {
	          callback(new Error('请输入密码'));
	        } else {
	          if (this.ruleForm2.checkPass !== '') {
	            this.$refs.ruleForm2.validateField('checkPass');
	          }
	          callback();
	        }
	      };
	      var validatePass2 = (rule, value, callback) => {
	        if (value === '') {
	          callback(new Error('请再次输入密码'));
	        } else if (value !== this.ruleForm2.pass) {
	          callback(new Error('两次输入密码不一致!'));
	        } else {
	          callback();
	        }
	      };
	      return {
	      	showContent: false,
	        ruleForm2: {
	          pass: '',
	          checkPass: '',
	          age: ''
	        },
	        rules2: {
	          pass: [
	            { validator: validatePass, trigger: 'blur' }
	          ],
	          checkPass: [
	            { validator: validatePass2, trigger: 'blur' }
	          ],
	          age: [
	            { validator: checkAge, trigger: 'blur' }
	          ]
	        }
	      }
    	},
			computed: {
				
			},
			methods: {
	      
	    },
	    mounted(){
	      setTimeout(()=>{
	        this.showContent = true
	      },100)
	    }
    }
</script>

<style lang="less" scoped>
	.addShop{
		margin-top: 50px;
	}
</style>

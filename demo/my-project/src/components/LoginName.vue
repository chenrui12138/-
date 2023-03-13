    <template>
        <div id="LoginName">
            <h1>{{ msg }}</h1>
        <div id="loginBox">
            <!-- <el-form :model="loginForm" status-icon :rules="loginRules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
                <el-form-item label="账号" prop="name">
                    <el-input type="text" v-model="loginForm.name" autocomplete="off"></el-input>
                </el-form-item>
 
                <el-form-item label="密码" prop="age">
                    <el-input type="text" v-model="loginForm.age" autocomplete="off"></el-input>
                </el-form-item>
 
                <el-form-item>
                    <el-button type="primary" @click="login()">提交</el-button>
                    <el-button>重置</el-button>
                </el-form-item>
            </el-form> -->
        </div>
    </div>
</template>
 
<script>
    export default {
        name: "LoginName",
        props: {
            msg:String
        },
        data(){
            return{
                loginForm:{name:"",age:""},
                //校验
                loginRules:{
                    name:[{ required: true, message: '请输入账号', trigger: 'blur' },],
                    age:[{ required: true, message: '请输入密码', trigger: 'blur' },]
                }
            }
        },
        methods:{
            login(){
                this.$http.post("http://localhost:8000/login",this.loginForm).then(resp=>{
                    console.log(resp.data.code)
                    if (resp.data.code===2000){
 
                        //登录成功 获取服务器相应的token值,保存到localStorage
                        localStorage.setItem("token",resp.data.data);
                        //路由跳转  不能使用  location.href
                        this.$router.push("/student")
                    }else {
                        this.$message.error("登陆失败,账号密码错误");
                    }
                })
            }
        }
    }
</script>
 
<style>
    #loginBox{
        width: 500px;
        height: 290PX;
        margin: 100px auto;
    }
    #loginForm{
        margin:50px auto;
 
    }
</style>
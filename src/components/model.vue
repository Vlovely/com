<template>
      <!-- 模态框 -->
      <div v-show="mtk" class="mtk">
      <div class="mtk_center">
      <div class="mtk_top">
        <ul>
          <li>修改密码</li>
          <li class="close" @click="close">×</li>
        </ul>
      </div>
      <div class="mtk_bottom">
        <div class="mtk_bottom_center">
          <div class="oldpw">
          <label for="oldPassword" >*当前密码：</label>
          <input id="oldPassword" type="text" ref="oldPassword">
        </div>
        <div class="newpw">
          <label for="newPassword">　*新密码：</label>
          <input id="newPassword" type="text" ref="newPassword">
        </div>
        <div class="qrnewpw">
          <label for="qrnewPassword">*确认密码：</label>
          <input id="qrnewPassword" type="text" ref="qrnewPassword">
        </div>
        <div class="mtk_btn">
          <div class="mtk_yes" @click="updatepass">确定</div>
          <div class="mtk_no" @click="cancel">取消</div>
        </div>
        </div>
      </div>
      </div>
    </div>

</template>


<script>
import Axios from "axios"
import '../css/common.css'
export default {
  data(){
    return{
      mtk:false,
      userName:'',
    }
  },
  methods:{
    safety(){
      this.mtk=true;
    },
    close(){
      this.mtk=false;
    },
    getInfo(){
      Axios({
        url:'/Handler/AdminLoginHandler?action=returninfo',
        method:"get",
      }).then(res=>{
        this.userName=res.data.data.userName
      })
    },
    quit(){
      Axios({
         url:'/Handler/AdminLoginHandler?action=quit',
         method:"get",
      }).then(res=>{
        alert(res.data.success)
        if(res.data.success){
          this.$router.push('/')

        }
      })
    },
    updatepass(){
      if (this.$refs.newPassword.value === this.$refs.qrnewPassword.value) {
        Axios({
        url:'/Handler/AdminRegHandler?action=updatepass',
        method:"post",
        data:{
          password: this.$refs.oldPassword.value,
          newpass: this.$refs.newPassword.value
        }
      }).then(res=>{
        if(res.data.success){
          console.log(res)
          this.$router.push('/')
        }

      })
      this.mtk=false;
      }else{
        alert("确认密码")
      }
      
    
    },
    cancel(){
      this.mtk=false;

    }
  },
  mounted(){
      this.getInfo();

  }
    
}
</script>


<style>
.mtk {
  width: 100%;
  height: 100%;
  background: rgba(255, 255, 255, 0.5);
  position: fixed;
  top: 0;
}
.mtk_center {
  width: 600px;
  height: 330px;
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}
.mtk_top {
  width: 100%;
  height: 30px;
  background: #4664ad;
}
.mtk_top ul {
  padding: 10px;
  color: #e8ebed;
  display: flex;
  justify-content: space-between;
}
.mtk_top ul .close {
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.6);
  color: #4664ad;
  text-align: center;
  line-height: 20px;
  font-size: 20px;
  font-weight: 800;
  cursor: pointer;
}
.mtk_bottom_center {
  width: 500px;
  margin: auto;
}
.oldpw,
.newpw,
.qrnewpw {
  display: flex;
  margin: 10px auto;
  justify-content: space-between;
}
.oldpw {
  margin-top: 40px;
}
.mtk_bottom {
  box-sizing: border-box;
  width: 100%;
  height: 300px;
  background: #fff;
  border: 10px solid #4664ad;
}
.mtk_bottom input {
  width: 400px;
  border: 1px solid #dfdad7;
}
.mtk_btn {
  display: flex;
  margin: 40px auto;
  justify-content: space-around;
}
.mtk_yes,
.mtk_no {
  width: 100px;
  height: 40px;
  text-align: center;
  line-height: 40px;
  color: #fff;
}
.mtk_yes {
  background-color: #46c540;
}
.mtk_no {
  background-color: #4664ad;
}

</style>

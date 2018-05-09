<template>
  <div>
    <userNav></userNav>
    <div class="home_box">
      <!-- kec列表 -->
         <div class="home_cont1" v-for="item,index in homeData.list" @mouseover="over(index)" @mouseout="out(index)">
           <h3>{{item.title}}</h3>
           <p>{{item.title_e}}</p>
           <div class="cont1_hover"></div>
           <div class="cont1_hover1" v-show="index==sIndex">
             {{item.data}}
           </div>
          </div>
      <!-- 学习人数比例 -->

      <div class="home_cont2">
        <div class="cont2_1" id="chart"></div>
        <div class="cont2_2" id="chart2"></div>

      </div>



    </div>
  </div>
  
</template>

<script>
import userNav from '../page/usernav'
import echarts from 'echarts'
var homeData={
  list:[
    {
      title:"课程列表",
      title_e:"Course list",
      data:"查询现有课程,添加课程,管理课程"
    },
    {
      title:"课程添加",
      title_e:"Course list",
      data:"查询现有课程,添加课程,管理课程"
    },
    {
      title:"课程置顶",
      title_e:"Course list",
      data:"查询现有课程,添加课程,管理课程"
    },
    {
      title:"视频管理",
      title_e:"Video Manggest",
      data:"查询现有课程,添加课程,管理课程"
    },
    {
      title:"用户管理",
      title_e:"User Manggest",
      data:"查询现有课程,添加课程,管理课程"
    },
    {
      title:"学院管理",
      title_e:"Course Mangge ",
      data:"查询现有课程,添加课程,管理课程"
    },
  ],
     
}
export default {
  name:'home',
  components:{userNav},
  data(){
    return{
      homeData:homeData,
      hide:false,
      sIndex:null,
    }
    
  },
  methods:{
    over(index){
      this.sIndex=index;
      // this.hide=true;
    },
    out(index){
      this.sIndex=null;
    }   
    },
    mounted(){
      let myChart = echarts.init(document.getElementById('chart'))
        // 绘制图表
            myChart.setOption({
              //提示信息
            tooltip : {
                  //悬浮框数据
                    formatter: "{a} <br/>{b} : {c}%"
            },
            //工具箱
            toolbox: {
              show:true,
              feature: {
              
              }
           },
           series: [
              {
                name: '业务指标',
                type: 'gauge',
                detail: {formatter:'{value}%'},
                data: [{value: 50, name: '完成率'}]
              }
            ]
        });
        
      let seChart = echarts.init(document.getElementById('chart2'))
        seChart.setOption( {
          tooltip : {
              trigger: 'item',
              formatter: "{a} <br/>{b} : {c} ({d}%)"
          },
          legend: {
              orient : 'vertical',
              x : 'left',
              data:['直接访问','邮件营销','联盟广告','视频广告','搜索引擎']
          },
          toolbox: {
              show : true,
              feature : {

              }
          },
          calculable : true,
          series : [
              {
                  name:'访问来源',
                  type:'pie',
                  radius : ['50%', '70%'],
                  itemStyle : {
                      normal : {
                          label : {
                              show : false
                          },
                          labelLine : {
                              show : false
                          }
                      },
                      emphasis : {
                          label : {
                              show : true,
                              position : 'center',
                              textStyle : {
                                  fontSize : '30',
                                  fontWeight : 'bold'
                              }
                          }
                      }
                  },
                  data:[
                      {value:335, name:'直接访问'},
                      {value:310, name:'邮件营销'},
                      {value:234, name:'联盟广告'},
                      {value:135, name:'视频广告'},
                      {value:1548, name:'搜索引擎'}
                  ]
              }
            ]
        });
    }
}
</script>

<style>
html,body{
  background: linear-gradient(right bottom,#807ea3,#0c1c4f); 
}
.home_box{
  width: 70%;
  margin: 0 auto;
  overflow: hidden;
 
}
.home_cont1{
  float: left;
  width: 160px;
  height: 200px;
  background: #39528a; 
  margin-left: 60px;
  margin-top: 100px;
  position: relative;
  cursor: pointer;
}
.home_cont1 h3{
  color: #fff;
  text-align: center;
  font-weight: 500;
  margin-top: 30px;
}
.home_cont1 p{
  text-align: center;
  font-size: 12px;
  color: #fff;
}
.cont1_hover{
  width: 60px;
  height: 60px;
  background: olivedrab;
  position: absolute;
  top: 100px;
  left: 50px;
}
.cont1_hover1{
  padding: 0 8px;
  /* background: olivedrab; */
  position: absolute;
  top: 100px;
  left: 5px;
  color: #fff;
}
.home_cont2{
  width: 100%;
  height: 480px;
  background: #6c739f;
  margin-top: 450px;
  margin-left: 30px
}
.cont2_1{
  width: 400px;
  height: 360px;
  background: #fff;
  float: left;
  margin: 70px 80px;
}
.cont2_2{
  width: 530px;
  height: 360px;
  background: #fff;
  float: right;
  margin: 70px 100px;

}

</style>

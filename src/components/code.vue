<template>
    <div>
        <canvas id="canvas" width="100%" height="40px" @click="change"></canvas>
    </div>
</template>

<script>
/*
四方面
    1.绘制矩形
        1.1 rect() x y w h
        1.2 填充颜色 fillstyle=''
    2.绘制小点
        2.1 arc() x y r 0 2pi bool
    3.绘制干扰线
        3.1 line 
    4.绘制文字
        4.1 font
*/
import Axios from 'axios'
export default {
    name:'canva',
    data(){
        return{
            width:'',
            canvas:'',
            height:'',
            ctx:''
        }
    },
 methods:{
        randomNum(min,max){
            return Math.floor(Math.random()*(max-min)+min)
        },
        randomColor(min,max){
            var r=this.randomNum(min,max);
            var g=this.randomNum(min,max);
            var b=this.randomNum(min,max);
            return 'rgb('+r+','+g+','+b+')'
        },
        
        change(){
            Axios.get('/Handler/AdminLoginHandler?action=veri')
            .then(res=> {
            this.drawpic(res.data.data)
        })
        },
        drawpic(res){
                // this.ctx.strokeStyle=this.randomColor(0,255);
            this.ctx.fillStyle=this.randomColor(180,240);
            // this.ctx.rect(0,0,100,40);
            this.ctx.fillRect(0,0,this.width,this.height)
            // 绘制干扰线
            for(var i =0;i<8;i++){
                this.ctx.strokeStyle=this.randomColor(80,150)
                this.ctx.beginPath();
                this.ctx.moveTo(this.randomNum(0,this.width),this.randomNum(0,this.height))
                this.ctx.lineTo(this.randomNum(0,this.width),this.randomNum(0,this.height))
                this.ctx.lineWidth=1
                this.ctx.closePath()
                this.ctx.stroke()
            }
            // 绘制干扰点
            for(var i=0; i<50; i++){
                    this.ctx.fillStyle = this.randomColor(0,255);
                    this.ctx.beginPath();
                    this.ctx.arc(this.randomNum(0,this.width),this.randomNum(0,this.height), 1, 0, 2*Math.PI);
                    this.ctx.fill();
            }
            // 绘制文字
            var i=0
            for(i; i<4; i++){
                var txt=res[i]
                // var txt = str[this.randomNum(0,str.length)];
                this.ctx.fillStyle = this.randomColor(50,100);  //随机生成字体颜色
                this.ctx.font = this.randomNum(20,40)+'px SimHei'; //随机生成字体大小
                var x = 20+i*15;
                var y = this.randomNum(25,30);
                var deg = this.randomNum(-30, 30);
                //修改坐标原点和旋转角度
                this.ctx.translate(x,y);
                this.ctx.rotate(deg*Math.PI/180);
                this.ctx.fillText(txt, 0,0);
                //恢复坐标原点和旋转角度
                this.ctx.rotate(-deg*Math.PI/180);
                this.ctx.translate(-x,-y);
            }
            console.log(res)
            this.$emit('code',res)
        }

    },
    mounted(){
        this.canvas=document.getElementById('canvas');
        this.width=this.canvas.width;
        this.height=this.canvas.height;
        this.ctx=this.canvas.getContext('2d');
        // 绘制矩形
        this.change()
        
    }
}
</script>

<style>

</style>

<template>
  <div class="wrapper">
    <image :src="logo" class="logo" />
    <text class="greeting">The environment is ready!</text>
    <router-view/>
    <div ref="test" style="background-color: #1ba1e2">
      <gcanvas @touchstart="touchstart" @touchmove="touchmove" @touchend="touchend" ref="gcanvess"
                                style="width: 650px;height: 1000px;background-color: yellow;margin-left: 50px"></gcanvas>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      startX:0,
      startY:0,
      currentX:0,
      currentY:0,
      context:{},
      canvasObj:{},
      logo: 'https://gw.alicdn.com/tfs/TB1yopEdgoQMeJjy1XaXXcSsFXa-640-302.png'
    }
  },
  methods:{
    touchstart(event){
      this.startX=event.changedTouches[0].pageX;
      this.startY=event.changedTouches[0].pageY;
      this.context.strokeStyle = "#17acf6" ;  //设置线的颜色状态
      this.context.lineWidth = 10;          //设置线宽状态
    },
    touchmove(event){
      this.currentX=event.changedTouches[0].pageX;
      this.currentY=event.changedTouches[0].pageY;
      //进行绘制
      this.context.move (this.startX,this.startY);
      this.context.lineTo(this.currentX,this.currentY);
      this.context.stroke();

      this.startX=event.changedTouches[0].pageX;
      this.startY=event.changedTouches[0].pageY;

    },
    touchend(event){

    },
    created(){
      var self=this;
      var gcanvas = enable(this.$refs.canvas_holder, {bridge: WeexBridge});
      var ctx = gcanvas.getContext("2d");
      self.context = ctx
//rect
      ctx.fillStyle = 'red';
      ctx.fillRect(0, 0, 100, 100);

//rect
      ctx.fillStyle = 'black';
      ctx.fillRect(100, 100, 100, 100);
      ctx.fillRect(25, 210, 700, 5);

//circle
      ctx.arc(450, 200, 100, 0, Math.PI * 2, true);
      ctx.fill();
    }
  }
}
</script>

<style scoped>
  .wrapper {
    justify-content: center;
    align-items: center;
  }
  .logo {
    width: 424px;
    height: 200px;
  }
  .greeting {
    text-align: center;
    margin-top: 70px;
    font-size: 50px;
    color: #41B883;
  }
  .message {
    margin: 30px;
    font-size: 32px;
    color: #727272;
  }
</style>

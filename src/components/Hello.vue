<template>
  <div class="hello">
    <div class="box line box1" style="transform: translate(-28%,-34%) scale(.33)" @click="choose(1)">
      <lines></lines>
    </div>
    <div class="box point box2" style="transform: translate(-28%,0) scale(.33)"  @click="choose(2)">
      <pie></pie>
    </div>
    <div class="box pie box3" style="transform: translate(-28%,34%) scale(.33)"  @click="choose(3)">
      <point></point>
    </div>
    <div class="box map box4 activ" style="transform: translate(38%,0) scale(1)"  @click="choose(4)">
      <maps></maps>
    </div>
  </div>
</template>

<script>
  import lines from './line'
  import pie from './pie'
  import point from './point'
  import maps from './map'
export default {
  data () {
    return {
      items:[]
    }
  },
  components:{
    lines,
    pie,
    point,
    maps
  },
  mounted(){
    this.init()
  },
  methods:{
    init() {
        //获取所有box的data-order的值
      this.items = document.querySelectorAll('.box')
      for (let i = 0; i < this.items.length; i++) {
        this.items[i].dataset.order = i;
      }
    },
    choose(clickIndex) {
        //获取当前显示的元素
      let activeItem = document.querySelector('.activ')
      //获取当前显示元素的data-order
      let activeIndex = activeItem.dataset.order
      //获取当前元素的下一个元素的data-order
      let clickItem = this.items[clickIndex - 1]

      //判断当前点击的元素的id和当前显示元素的data-order是否相等
      if (activeIndex === clickIndex) {
        return
      }
      //更换样式
      activeItem.classList.remove('activ')
      clickItem.classList.add('activ')
      this._setStyle(clickItem, activeItem)
    },
    _setStyle(el1, el2) {
        //更换transform样式
      let transform1 = el1.style.transform
      let transform2 = el2.style.transform
      el1.style.transform = transform2
      el2.style.transform = transform1
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  body,html{width:100%;height: 100%;overflow: hidden}
  body{background: midnightblue}
  .hello{width: 100%;height:98%;position: relative}
  .box{position: absolute;width: 60%;height: 100%;transition:all 0.8s;}

</style>

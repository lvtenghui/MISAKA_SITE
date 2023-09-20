<template>
    <div class="wrapper">
      <div class="swiperBox" :style="`transform:translateY(${translateLength})`">
        <section v-for="item of dataList" :key="item.id" :style="'background-color:' + item.style"> {{ item.name }}</section>
      </div>
      <div class="indicatorBox">
        <div v-for="(item,index) of dataList" :key="item.id" class="indicatorItem" :style="index === moveIndex ? 'width: 12px;height: 12px;background-color:#fff; cursor:auto;' : '' " @click="changeIndex(index)"></div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HelloWorld',
    props: {
      dataList: {
        type: Array
      }
    },
    data () {
      return {
        canDo: true,
        moveIndex: 0,
        maxIndex: null
      }
    },
    mounted () {
      this.calcIndex()
      window.addEventListener('mousewheel', this.throttle)
    },
    computed: {
      translateLength () {
        return this.moveIndex * 100 * -1 + 'vh'
      }
    },
    methods: {
      // 计算当前索引
      calcIndex () {
        const cIndex = this.dataList.length - 1
        this.maxIndex = cIndex
      },
      // 节流函数
      throttle (e) {
        if (!this.canDo) {
          return false
        }
        this.scrollPage(e.deltaY)
        this.canDo = false
        setTimeout(() => {
          this.canDo = true
        }, 600)
      },
      // 滚动页面效果
      scrollPage (scrollHeight) {
        if (scrollHeight > 0) {
          // console.log('向下滚动', scrollHeight)
          this.moveIndex++
          if (this.moveIndex > this.maxIndex) {
            this.moveIndex--
            this.$msg({
              message: '已经到底了哦~',
              type: 'warning',
              duration: 1000
            })
          }
        } else {
          // console.log('向上滚动', scrollHeight)
          this.moveIndex--
          if (this.moveIndex < 0) {
            this.moveIndex = 0
            this.$msg({
              message: '已经到头了哦~',
              type: 'warning',
              duration: 1000
            })
          }
        }
      },
      // 指示器点击
      changeIndex (cIndex) {
        if (cIndex === this.moveIndex) return
        this.moveIndex = cIndex
      }
    }
  }
  </script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
  .wrapper {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
  }
  .swiperBox {
    width: 100vw;
    transition: .6s;
  }
  section {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 48px;
    font-weight: 700;
  }
  .indicatorBox {
    position: fixed;
    top: 50%;
    transform: translateY(-50%);
    right: 20px;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .indicatorItem {
    width: 8px;
    height: 8px;
    margin: 8px 0;
    background-color:rgba(255,255,255,.6);
    border-radius: 50%;
    transition: .6s;
    cursor: pointer;
  }
  </style>
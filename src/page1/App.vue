<template>
    <div class="wrap">
        <ul :class="['swiperUl', isLeft ? '':'isLeft', isRight ? '': 'isRight']">
            <li v-for="(v,i) in dataList" :key="i" :class="classList[i]" @touchstart="start()" @touchmove="move()" @touchend="end()">{{ v }}</li>
        </ul>
    </div>
</template>

<script>

export default {
    data: _ => ({
        dataList: ['L0','L1','L2','L3','L4','L5','L6','L7','L8','L9'],
        classList: [],
        showVal: 'L0', // 初始值
        page1: '',
        page2: '',
        pageName: '',
        isMove: false, // 判断点击是否移动
        changeX: '',
        isLeft: true, // 判断左边是否显示
        isRight: true // 判断右边是否显示
    }),
    created() {
        // 设置classList的初始值
        let that = this
        for (var i in that.dataList) {
            if (i != 2) {
                that.classList.push('p'+ i)
            }
        }
        that.classList.push('p2')

        // 初始化classList的排列顺序
        that.classSort(that.showVal)
    },
    methods: {
        // 根据showVal的值判断classList的排列
        classSort(val) {
            let that = this,
                data = that.dataList,
                arr1 = [],
                arr2 = []
            for (var i = 0 , l = data.length ; i < l ; i++) {
                if (val == data[i]) {
                    arr1 = that.classList.slice(0,l - i)
                    arr2 = that.classList.slice(l - i)
                    that.classList = arr2.concat(arr1)
                    break;
                }
            }
            that.judgeHidden(val)
        },
        // 判断左右是否隐藏
        judgeHidden(newVal) {
            let that = this
            let listLen = that.dataList.length
            if (newVal == that.dataList[0]) {
                that.isLeft = false
            } else {
                that.isLeft = true
            }
            if (newVal == that.dataList[listLen-1]) {
                that.isRight = false
            } else {
                that.isRight = true
            }
        },
        // touchstart
        start(e) {
            let that = this
            let eve = e || window.event
            that.page1 = eve.targetTouches[0].pageX;
            that.pageName = eve.target.className
            if (that.pageName == 'p0') {
                that.isMove = false
            } else {
                that.isMove = true
            }
        },
        // touchmove
        move(e) {
            let that = this
            let eve = e || window.event
            that.page2 = eve.targetTouches[0].pageX
            that.isMove = true
        },
        // touchend
        end(e) {
            let that = this
            let eve = e || window.event
            let liList = document.querySelectorAll(".swiperUl li");
            let showVal = document.querySelector('.p0').innerText;
            let listLen = this.classList.length
            if (that.isMove) {
                if (that.page2) {
                    that.changeX = that.page2 - that.page1
                } else {
                    if(that.pageName == 'p2') {
                        that.changeX = 1
                    } else if(that.pageName == 'p1') {
                        that.changeX = -1
                    }
                }
            } else {
                that.changeX = 0
            }
            if (this.changeX < 0 && showVal != this.dataList[listLen-1]) {
                //往左滑
                this.classList.unshift(this.classList[listLen-1]);
                this.classList.pop();
                for (let i = 0; i < liList.length; i++) {
                    liList[i].setAttribute("class", "");
                    liList[i].setAttribute("class", this.classList[i]);
                }
            }
            if (this.changeX > 0 && showVal != this.dataList[0]) {
                //往右滑
                this.classList.push(this.classList[0]);
                this.classList.shift();
                for (let i = 0; i < liList.length; i++) {
                    liList[i].setAttribute("class", "");
                    liList[i].setAttribute("class", this.classList[i]);
                }
            }
            that.page1 = ''
            that.page2 = ''
            // 判断在数据最前或者最后是否显示
            let newVal = document.querySelector('.p0').innerText;
            that.judgeHidden(newVal)
        }
    }
}
</script>
<style lang="scss" scoped>
    $c: #c77083;
    $f: 16;
    $w: calc(100%/3);

    body {font-family: "Microsoft YaHei", Arial, Helvetica, sans-serif, "宋体"; }
   * {
        margin: 0;
        padding: 0;
        text-decoration: none;
        list-style: none;
        box-sizing: border-box;
   }
   .swiperUl {
        width: 357rem/$f;
        padding: 20rem/$f;
        margin-top: 10rem;
        box-sizing: border-box;
        position: relative;
        li {
            position: absolute;
            width: 119rem/$f;
            text-align: center;
            opacity: 0;
            height: 100px;
            line-height: 100px;
            border-radius: 6px;
            transition: all 0.3s ease-out;
        }
        .p0 {
            transform:translate3d(6.8rem,0,0) scale(1);
            opacity: 1; 
            z-index: 22;
            background: #c77083;
        }
        .p1 {
            transform:translate3d(13.6rem,0,0) scale(0.8);
            opacity: .7;
            filter: grayscale(100%);
            z-index: 11;
            background: #c77083;
        }
        .p2 {
            transform:translate3d(0,0,0) scale(0.8);
            opacity: .7;
            filter: grayscale(30%);
            z-index: 11;
            background: #c77083;
        }
   }
    .isLeft .p2 {
        opacity: 0;

    }
    .isRight .p1 {
        opacity: 0;
    }

</style>


<template>
    <div>
        <div class="v_swpiper_bk">
            <div class="v_swiper">
                <ul class="ver_ul">
                    <li v-for="(v,i) in dataList" :key="i">{{v}}</li>
                    <li class="ver_li">{{dataList[0]}}</li>
                </ul>
            </div>
        </div>
        <div class="swiper_2">
            <ul class="slide">
                <li v-for="(v,i) in dataList" :key="i">{{v}}</li>
                <li class="sli_li">{{dataList[0]}}</li>
            </ul>
        </div>
    </div>
    
</template>
<script>
export default {
    data: _=> ({
        dataList: [
            '我的老家就住在这个屯',
            // '2222222222',
            // '3333333333',
            // '444444444',
            // '555555555',
            '66666666666',
            '77777777777'
        ],
        ulLen: 0,
        liHeight: '',
        timer1: null,
        timer2: null
       
    }),
    mounted() {
        this.setInt1()
        this.setInt2()
    },
    methods: {
        setInt1() {
            var that = this,
                liHeight = document.querySelector('.ver_ul li').clientHeight,
                ulScroll = document.querySelector('.v_swiper');

            that.liHeight = liHeight
            that.timer1 = setInterval(function(){
                if (that.ulLen == that.dataList.length) {
                    $(ulScroll).animate({scrollTop: that.dataList.length * liHeight},200)
                    clearInterval(that.timer1)
                    setTimeout(() => {
                        that.setInt1()
                        that.ulLen = 0
                        $(ulScroll).animate({scrollTop: 0},0)
                    },200)
                } else {
                    that.ulLen ++
                    $(ulScroll).animate({scrollTop: that.ulLen * liHeight},1200)
                }
            },1000)
        },
        setInt2() {
            var that = this,
                swiper = document.querySelector('.swiper_2'),
                slide = document.querySelector('.swiper_2 .slide'),
                lastLi = document.querySelector('.sli_li'),
                swi2W = swiper.clientWidth;

            function Marquee() {
                if (lastLi.offsetLeft - swiper.scrollLeft <= 0)
                    swiper.scrollLeft = 0
                else {
                    swiper.scrollLeft++
                }
            }
            that.timer2 = setInterval(Marquee,20)
            
        }
        
    }
}
</script>
<style lang="scss" scoped>
    * {
        list-style: none;
        margin: 0;
        padding: 0;
    }
    .v_swpiper_bk {
        width: 300px;
        overflow: hidden;
    }
    .v_swiper {
        width: 100%;
        height: 50px;
        overflow-y: scroll;
        overflow-x: hidden;
        margin: 100px auto;
        background: #f5f5f5;
        position: relative;
    }
    .v_swiper ul {
        width: 300px;
    }
    .v_swiper li {
        width: 300px;
        height: 50px;
        line-height: 50px;
        padding: 0 10px;
        box-sizing: border-box;
        white-space:nowrap; 
        text-overflow:ellipsis;
        overflow:hidden;
    }

    .swiper_2 {
        width: 300px;
        margin-top: 60px;
        overflow: hidden;
    }
    .swiper_2 ul {
        display: flex;
        flex-wrap: nowrap;
    }
    .swiper_2 ul li {
        padding-right: 300px;
        white-space:nowrap; 
    }
    .swiper_2::-webkit-scrollbar {/*滚动条整体样式*/
        opacity: 0
    }
    .v_swiper::-webkit-scrollbar {/*滚动条整体样式*/
        opacity: 0
    }

</style>


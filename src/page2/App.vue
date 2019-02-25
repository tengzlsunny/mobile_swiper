<template>
    <div class="v_swpiper_bk">
        <div class="v_swiper">
            <ul class="ver_ul">
                <li v-for="(v,i) in dataList" :key="i">{{v}}</li>
                <li class="ver_li">{{dataList[0]}}</li>
            </ul>
        </div>
    </div>
    
</template>
<script>
export default {
    data: _=> ({
        dataList: [
            '1111111111',
            '2222222222',
            '3333333333'
        ],
        ulLen: 0,
        liHeight: '',
        timer: null
       
    }),
    mounted() {
        this.setInt()
    },
    methods: {
        setInt() {
            var that = this,
                liHeight = document.querySelector('.ver_ul li').clientHeight,
                ulScroll = document.querySelector('.v_swiper');

            that.liHeight = liHeight
            that.timer = setInterval(function(){
                if (that.ulLen == that.dataList.length) {
                    clearInterval(that.timer)
                    $(ulScroll).animate({scrollTop: that.dataList.length * liHeight},500)
                    setTimeout(() => {
                        that.ulLen = 0
                        $(ulScroll).animate({scrollTop: 0},0)
                        that.setInt()
                    },500)
                } else {
                    that.ulLen ++
                    $(ulScroll).animate({scrollTop: that.ulLen * liHeight},1000)
                    // ulScroll.scrollTop = that.ulLen * liHeight
                    // $('.ver_ul').animate({scrollTop: that.ulLen * liHeight},500)
                }
            },1000)
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
        width: 110%;
        height: 50px;
        overflow-y: scroll;
        margin: 100px auto;
        background: #f5f5f5;
        position: relative;
    }
    ul {
        width: 300px;
    }
    li {
        width: 300px;
        height: 50px;
        line-height: 50px;
        padding: 0 10px;
        box-sizing: border-box;
    }

</style>


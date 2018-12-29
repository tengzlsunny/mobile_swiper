<template>
    <div class="v_swiper">
        <ul>
            <li v-for="(v,i) in dataList" :key="i">{{v}}</li>
        </ul>
    </div>
</template>
<script>
import $ from 'jquery'
export default {
    data: _=> ({
        dataList: [
            '1111111111',
            '2222222222',
            '3333333333',
            '4444444444',
            '5555555555',
            '6666666666',
            '7777777777',
            '9999999999',
            '8888888888',
            '0000000000',
            '1212121212',
            '2323232323',
            '3443434344',
            '5656565656',
            '6767676767',
            '7878787878',
            '8989898989',
            '9090909090',
        ],
        ulPlace: 0,
        ulLen: 0
    }),
    mounted() {
        var that = this,
            liHeight = $('.v_swiper li').height();
            
        setInterval(function(){
            if (that.ulLen >= that.dataList.length - 1 ) {
                that.ulPlace = 0
                that.ulLen = 0
            } else {
                that.ulLen ++
                that.ulPlace += liHeight
            }
            let temp = - that.ulPlace + 'px'
            $('.v_swiper ul').animate({'top': - that.ulPlace},1000)
        },1000)
    }
}
</script>
<style lang="scss" scoped>
    * {
        list-style: none;
        margin: 0;
        padding: 0;
    }
    .v_swiper {
        width: 300px;
        height: 50px;
        overflow: hidden;
        margin: 100px auto;
        background: #f5f5f5;
        position: relative;
    }
    ul {
        width: 300px;
        position: absolute;
        top: 0;
    }
    li {
        width: 300px;
        height: 50px;
        line-height: 50px;
        padding: 0 10px;
        box-sizing: border-box;

    }
</style>


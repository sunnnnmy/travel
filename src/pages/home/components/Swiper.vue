<template>
    <div class="wrapper">
        <swiper  :options="swiperOptions">
            <swiper-slide v-for ="item of swiperList" :key ="item.id">
                <img class="swiper-img" :src="item.imgUrl" alt="">
            </swiper-slide>
            
            
            <div class="swiper-pagination" slot="pagination"></div>
            </swiper>
    </div>
</template>

<script>
    export default{
        name:"HomeSwiper",
        data:function(){
            return {
                swiperOptions:{
                    pagination:'.swiper-pagination',
                    loop:true
                },
                swiperList:[{
                    id:'0001',
                    imgUrl:'https://imgs.qunarzz.com/piao/fusion/1505/27/301e8692d285a3.jpg'
                },
                {
                    id:'0002',
                    imgUrl:'	https://imgs.qunarzz.com/p/tts4/2009/84/7dbcb77f05290402.jpg_640x360_ed1aed91.jpg'
                },
            ]
            }
        }
    }
</script>

<style lang="stylus" scoped>
    .wrapper >>> .swiper-pagination-bullet-active{
        background: red !important;
    }    
    .wrapper{
        overflow: hidden;
        width: 100%;
        height: 0;
        padding-bottom: 31.25%;
        background: eee;
    }
        .swiper-img{
            width: 100%;
            height: 2rem;
        }
    
</style>
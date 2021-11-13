<template>
    <div>
      <home-header ></home-header>
      <home-swiper :list="swiperList"></home-swiper>
      <home-icons :list ="iconList"></home-icons>
      <home-recommend :list="recommendList"></home-recommend>
      <home-weekend :list="weekendList"></home-weekend>
    </div>
</template>

<script>
    import HomeHeader from './components/Header'
    import HomeSwiper from './components/Swiper'
    import HomeIcons from './components/Icons'
    import HomeRecommend from './components/Recommend'
    import HomeWeekend from './components/Weekend'
    import axios from 'axios'
    import {mapState} from 'vuex'
    export default{
        name:'Home',
        components:{
            HomeHeader, 
            HomeSwiper,
            HomeIcons,
            HomeRecommend,
            HomeWeekend
        },
        computed:{
            ...mapState(['city'])
        },
        data(){
            return{
                lastCity:'',
                swiperList:[],
                iconList:[],
                recommendList:[],
                weekendList:[]
            }
        },
        // 完成Ajax的获取 生命周期函数
        mounted(){
            this.lastCity =this.city
            this.getHomeInfo()
        },
        methods:{
            getHomeInfo(){
                axios.get('/api/index.json?city='+this.city).then(this.getHomeInfoSucc);// 返回结果是一个promise对象 所以then
            },
            getHomeInfoSucc(res){
                res = res.data
                if(res.ret && res.data){
                    const data = res.data
                    this.swiperList = data.swiperList;
                    this.iconList = data.iconList;
                    this.recommendList = data.recommendList;
                    this.weekendList = data.weekendList;

                }
                console.log(res);
            }

        },
        activated(){
            if (this.lastCity !== this.city) {
                this.lastCity = this.city
                this.getHomeInfo()

            }
        }
    }
</script>


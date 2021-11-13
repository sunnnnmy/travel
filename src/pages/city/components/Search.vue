<template>
    <div>
        <div class="search">
            <input v-model="keyword" type="text" placeholder="输入城市名或拼音" class="search-input">
        </div>

        <div class="search-content" ref="search" v-show="keyword">
            <ul>
                <li v-for="item of list" class="search-item border-bottom"  :key="item.id" @click="handleCityClick(item.name)">
                    {{item.name}}
                </li>

                <li class="search-item border-bottom" v-show="hasList">没有找到匹配数据</li>
            </ul>
        </div>
    </div>
</template>

<script>
    import Bscroll from 'better-scroll'
    import{mapMutations}from 'vuex'
    export default{
        name:'CitySearch',
        data(){
            return{
                keyword:'',
                list:[],
                timer:null
            }
           
        },
        mounted(){
            this.scroll = new Bscroll(this.$refs.search);
        },
        computed:   {
            hasList(){
                return !this.list.length
            }
        },
        props:{
                cities:Object
            }, 
         methods:{
            handleCityClick(city){
                this.changeCity(city)
                this.$router.push('/')
            },
            ...mapMutations(['changeCity'])
            },
        watch:{
            keyword(){
                if (this.timer) {
                    clearTimeout(this.timer)
                }
                this.timer = setTimeout(()=>{
                    const result = [];
                    for (let i in this.cities) {
                        this.cities[i].forEach((value)=>{
                            if (value.spell.indexOf(this.keyword)>-1 ||value.name.indexOf(this.keyword)>-1){
                                result.push(value);
                            } 
                        })
                    }
                
                    this.list = result;
                },100)
            }
        }    
    }
</script>

<style lang="stylus" scoped>
     @import '~styles/varibles.styl';
    .search{
        height: .72rem;
        background: $bgColor;
        padding: 0 .1rem;
    }
      .search-input{
          box-sizing: border-box;
          height: .62rem;
          line-height: .62rem;
          width: 100%;
          padding: 0 .1rem;
          text-align: center;
          border-radius: .06rem;
          color: #666;
      }
    .search-content{
        position: absolute;
        top: 1.58rem;
        left: 0;
        right: 0;
        bottom: 0;
        overflow: hidden;
        background: #eee;
        z-index:  1;
        
    }  
        .search-item{
            line-height: .62rem;
            padding: .2rem;
            color: #666;
            background: #fff;
        }
</style>
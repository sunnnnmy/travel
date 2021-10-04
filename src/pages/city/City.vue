<template>
    <div>
        <city-header></city-header>
        <city-search></city-search>
<<<<<<< HEAD
        <city-list :cities="cities" :hot="hotCities"></city-list>
        <city-alphabet :cities="cities"></city-alphabet>
=======
        <city-list :cities="cities" :hot="hotCities" :letter="letter"></city-list>
        <city-alphabet :cities="cities" @change="handleLetterChange"></city-alphabet>
>>>>>>> city-components
    </div>
</template>

<script>
    import CityHeader from './components/Head.vue'
    import CitySearch from './components/Search.vue'
    import CityList from './components/List.vue'
    import CityAlphabet from './components/Alphabet.vue'
    import axios from 'axios'
    export default{
        name:"City",
        components:{
            CityHeader,
            CitySearch,
            CityList,
            CityAlphabet
        },
        data(){
            return{
                cities:{},
<<<<<<< HEAD
                hotCities:[]
=======
                hotCities:[],
                letter:""
>>>>>>> city-components
            }
        },
        methods:{
            getCityInfo(){
                axios.get('/api/city.json').then(this.handleGetCityInfoSucc)
            },
            handleGetCityInfoSucc(res){
                res = res.data;
                if(res.ret && res.data){
                    const data = res.data;
                    this.cities = data.cities;
                    this.hotCities = data.hotCities;
                }
<<<<<<< HEAD
=======
            },
            handleLetterChange(letter){
                this.letter = letter;
>>>>>>> city-components
            }
        },
        mounted(){
            this.getCityInfo()
        }
    }
</script>

<style lang="stylus" scoped></style>
<template>
    <center><h1 style="margin-bottom: 1cm; margin-top: 1cm; background-color: cyan ;" >Surah Al-Qur'an</h1></center>
    <div>
        <!--bikin list looping api-->
        <li v-for = "item in ListSurah">
            <!--pembuka gutter-->
            <center>
                <div class="container px-4" style="margin-top:0.25cm;">
    <div class="row gx-5">
    <div class="col">
    <div class="p-3 border bg-light"><h1> 
        <p>{{ item.id }} . {{ item.name_complex }} </p> 
        {{ item.name_arabic }} <br>
        <p>Tempat Turunnya Wahyu : {{ item.revelation_place }}</p>
        

    </h1>
            <!-- bikin div pembuka button -->
            <div class="btn-group" role="group" aria-label="Basic outlined example">
                <button type="button" class="btn btn-outline-primary">
                    <router-Link :to="{ name : 'surah', params : {id:item.id} }" >BACA</router-Link>
                </button>
            </div>
            <!--penutup div button--> 
    </div>
    </div>
    </div>
    </div>
            <!--penutup gutter-->
            </center>
                   
        </li>
        <!--penutup li-->
    </div>
</template>
<script>
import axios from 'axios';
import {ref} from "vue";
export default { 
    data () {
        return {
            ListSurah : ref ([])
        }
    },
    mounted(){
        this.getListSurah()
    },
    methods:{
        getListSurah(){
            axios.get('https://api.quran.com/api/v4/chapters?language=id')
            .then ((respons) =>{
                console.log(respons)
                this.ListSurah = respons.data.chapters
            }) .catch((err) => {
                console.log('errornya'+err)
            })
        }
    }

}

</script>
<style>
li{
    list-style: none;
}
</style>
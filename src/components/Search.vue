<template>
    <div class="section container">
        <img src="@/assets/a.gif" alt="logo" class="logotipo">

        <input type="text" v-model="searchTherm" class="input is-info input is-rounded input is-hovered input is-medium" placeholder="¿Qué Gif vamos a buscar?">
        <button class="button is-success is-focused is-medium" @click='getGifs'>¡Busquemos!</button>

        <div class="gif-container">
            <img :src="gif" v-for="gif in gifs" :key="gif.id" @click="showModal">
        </div>

        <button class="button is-success is-focused is-medium" @click='getMoreGifts' v-show="gifs.length<100 && gifs.length>9"> ¡Más! </button>

        <Modal v-show="isModalVisible" @close="closeModal"/>
    </div>
</template>


<script>
import Modal from '@/components/Modal.vue';

export default {

components: {
        Modal
    },

    data() {
        return {
                play: false,
                apiKey: 'vXdCFDPiGB1BuKQaJSSXOBnu2tBsOIhF',
                searchEndpoint: 'https://api.giphy.com/v1/gifs/search?',
                limit: 10,
                searchTherm: '',
                gifs: [],
                isModalVisible: false
        }
                
            },
            methods: {
                getGifs(){
                    let url = `${this.searchEndpoint}&api_key=${this.apiKey}&q=${this.searchTherm}&limit=${this.limit}&offset=${this.offset}`

                    fetch(url)
                    .then(response=> response.json())
                    .then(json => this.buildGifs(json))
                    .catch(err => console.log(err))
                },

                buildGifs(json){
                    this.gifs = json.data
                    .map(gif => gif.id)
                    .map(gifId => {
                        return `https://media.giphy.com/media/${gifId}/giphy.gif`
                    })
                },

                getMoreGifts(){
                    let url = `${this.searchEndpoint}&api_key=${this.apiKey}&q=${this.searchTherm}&limit=${this.limit +=10}&offset=${this.offset}`

                    fetch(url)
                    .then(response=> response.json())
                    .then(json => this.buildGifs(json))
                    .catch(err => console.log(err))
                },

                showModal(){
                    this.isModalVisible = true;
                },

                closeModal(){
                    this.isModalVisible = false;
                },
    
            }
}
</script>

<style>
*{
    background: #FFF8DE;
}
button{
    margin: 1rem;
}

.logotipo{
    margin-top: none;
    margin-bottom: 2rem;
}

.gif-container{
    width: 100%;
    column-count: 3;
}

@media (max-width: 767px) { 
    .gif-container {
        columns:2;
    }

}

@media (max-width: 480px) {
    .gif-container {
        columns: 1;
    }
}
</style>
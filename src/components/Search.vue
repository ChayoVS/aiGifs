<template>
    <div class="section container">
        <img src="@/assets/a.gif" alt="logo" class="logotipo">

        <input type="text" v-model="searchTherm" class="input is-info input is-rounded input is-hovered input is-medium" placeholder="¿Qué Gif vamos a buscar?">
        <button class="button is-success is-focused is-medium" @click=getGifs()>¡Busquemos!</button>

        <div class="gif-container">
            <img :src="gif" v-for="gif in gifs" :key="gif.id" @click=clickRev()>
        </div>

        <button class="button is-success is-focused is-medium" @click=getMoreGifts() v-show="gifs.length<100 && gifs.length>9"> ¡Hay más! </button>
    </div>
</template>


<script>
export default {
    data() {
        return {
                apiKey: 'vXdCFDPiGB1BuKQaJSSXOBnu2tBsOIhF',
                searchEndpoint: 'http://api.giphy.com/v1/gifs/search?',
                limit: 10,
                searchTherm: '',
                gifs: []
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

                clickRev(){
                    console.log('hola');
                }

            }
}
</script>

<style>
*{
    background: #FFF8DE
}
button{
    margin: 1rem;
}

.logotipo{
    margin-bottom: 2rem;
}


</style>
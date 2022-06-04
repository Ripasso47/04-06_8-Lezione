<template>
    <div class="container">
        <div class="principale">
            <h1 id="titolo">Nome: {{immagini[current].nome}}</h1>
            <img :src="immagini[current].img" alt="">
            <!-- <button class="left" @click="current == 0 ? current = 3 : current--">-</button>
            <button class="right" @click="current == 3 ? current = 0 : current++">+</button> -->
            <button class="left" @click="cliccato('-')">-</button>
            <button class="right" @click="cliccato('+')">+</button>
        </div>
        <div class="cont-immagini">
            <div class="immagine" v-for="immagine, index in immagini" :key="index">
                <img :src="immagine.img" alt="" @click="cliccato(index)" :class="current == index ? 'selected' : '' ">
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Carousel',
    data() {
        return {
            immagini: [
                {
                    "nome" : "Lago",
                    "img" : require("../../assets/img/01.jpg"),
                    "title" :"uomo sul lago"
                },
                {
                    "nome" : "Spagna",
                    "img" : require("../../assets/img/02.jpg"),
                    "title" : "Case belle"
                },
                {
                    "nome" : "Londra",
                    "img" : require("../../assets/img/03.jpg"),
                    "title" : "Orologio"
                },
                {
                    "nome" : "Svizzera",
                    "img" : require("../../assets/img/04.jpg"),
                    "title" : "Palazzi"
                }
            ],
            current: 0,
            action: '',
            indice: 0,
        }
    },
    props: {
        risposta: String
    },
    watch: {
        current(){
            if(this.current < 0)this.current = 3;
            else if(this.current > 3)this.current = 0;
        },
        risposta(){
            if(this.risposta == '1'){
                if(this.action != ''){
                    if(this.action == '+')this.current++;
                    else this.current--;
                    this.action = '';
                }
                else {
                    this.current = this.indice;
                }
                this.$emit('gozero', '0');
            }
        }
    },
    methods: {
        cliccato(value){
            if(value == '+' || value == '-'){
                this.action = value;
            }
            else {
                this.indice = value;
            }
            this.$emit('clicked', '1');
        }
    }
}
</script>

<style scoped>
.container{
    width: 80%;
    margin: 0 auto;
}

.principale{
    width: 100%;
    height: 500px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
}

.left{
    position: absolute;
    left: 0;
    top: 50%;
}

.right{
    position: absolute;
    right: 0;
    top: 50%;
}

.principale img{
    width: 70%;
    height: 100%;
}

.cont-immagini{
    display: flex;
    margin-top: 20px;
}

.cont-immagini .immagine{
    width: 30%;
    margin: 0 5px;
}

.immagine img{
    width: 100%;
    height: 100%;
}

.selected{
    border: 3px solid red;
}
</style>
<template>
    <div class="blocca" :class="domanda == '1' ? 'visible' : '' ">
        <div class="container">
            <div class="popup">
                <h1>Domanda</h1>
                <h4>{{domande[appoggio].domanda}}</h4>
                <button class="si" @click="risposta('si')">Si</button>
                <button class="no" @click="risposta('no')">No</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: 'Domande',
    data() {
        return {
            domande: [
                {
                    "domanda" : "La torre eiffel è alta 300m ?",
                    "risposta" : "si",
                },
                {
                    "domanda" : "Si vedono i 2 Leocorni ?",
                    "risposta" : "no",
                },
                {
                    "domanda" : "Ad Alessandro piace il sushi ?",
                    "risposta" : "si",
                },
                {
                    "domanda" : "La terra è piatta ?",
                    "risposta" : "no",
                }
            ],
            appoggio : 0
        }
    },
    props: {
        domanda: String
    },
    watch: {
        domanda(){
            if(this.domanda == '1'){
                this.appoggio = Math.floor((Math.random() * 3 )+ 1);
            }
        }
    },
    methods: {
        risposta(ris){
            if(this.domande[this.appoggio].risposta == ris){
                this.$emit('risposta', '1');
            }
            else {
                this.$emit('risposta', '0');
            }
        }
    }
}
</script>

<style lang="scss" scoped>
.blocca{
    display: none;
    position: absolute;
    top: -60px;
    left: 0;
    margin: 0;
    width: 100%;
    height: 100vh;

    .container{
        width: 600px;
        height: 400px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: cadetblue;
        border: 1px solid blue;
        padding: 30px;

        .popup{
            text-align: center;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);

            h1{
                margin: 10px;
            }

            h4{
                margin: 40px;
            }

            .si, .no{
                padding: 20px;
                margin: 20px;
                border: none;
                cursor: pointer;

                &:hover{
                    scale: 1.1;
                }

                &:active{
                    border: 2px solid black;
                }
            }

            .si{
                background-color: lime;
            }

            .no{
                background-color: red;
            }
        }
    }
}

.visible{
    display: block;
}
</style>
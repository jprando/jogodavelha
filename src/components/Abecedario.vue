<template>
    <div class="abecedario">
        <button
            v-for="letra in letras"
            :key="letra"
            :disabled="letraJaJogada(letra)"
            @click="escolherLetra(letra)">
            {{ letra }}
        </button>
    </div>
</template>

<script>
export default {
    data() {
        return {
            letras: null,
            letrasJogadas: []
        }
    },
    props: {
        palavra: {
            type:String,
            required: true
        }
    },
    watch:{
        palavra(newVal, oldVal) {
            if(newVal != oldVal)
            {
                this.letrasJogadas.splice(0)
            }
        }
    },
    methods: {
        escolherLetra(letra) {
            this.letrasJogadas.push(letra)
            this.$emit('letra', letra)
        },
        letraJaJogada(letra) {
            return this.letrasJogadas.indexOf(letra) > -1
        }
    },
    mounted() {
        const gerarLetra = (_, i) => String.fromCharCode('A'.charCodeAt(0)+i)
        this.letras = Array(26).fill().map(gerarLetra)
    }
}
</script>

<style>
.abecedario {
    padding-top: 10px;
    padding-bottom: 10px
}
</style>


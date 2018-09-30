<template>
    <div class="dica" @click="exibirDica=!exibirDica && !!dica">
        <div>
            <span>DICA</span>
        </div>
        <div v-show="exibirDica">
            <span>{{ dica }}</span>
        </div>
        <div v-show="!exibirDica">
            <span>???</span>
        </div>
    </div>

</template>

<script>
export default {
    name: 'Dica',
    props:{
        dica:{
            type: String,
            required: false,
            default: null
        }
    },
    data() {
        return {
            exibirDica: false
        }
    },
    watch:{
        dica(){
            this.exibirDica = false
        }
    }
}
</script>

<template>
    <div class="letreiro palavra">
        <div class="letras">
            <span class="letra"
                v-for="(letra, index) in exibirLetras"
                :key="index">{{ letra }}</span>
        </div>
        <div class="grupo">
            {{ grupo }}
        </div>
    </div>
</template>

<script>
export default {
    name: 'Letreiro',
    props: {
        grupo: {
            type: String,
            required: true
        },
        dica: {
            type: String,
            required: false
        },
        palavra: {
            type: String,
            required: true
        },
        letra: {
            type: String,
            required: false,
            default: null
        }
    },
    data() {
        return {
            exibirDica: false,
            listaLetras: []
        }
    },
    watch:{
        letra(val) {
            if(val)
            {
                this.letra = val.toUpperCase()
                if(this.letra && !this.temNaLista(this.letra))
                {
                    this.listaLetras.push(this.letra)
                }
            }
        },
        palavra(val, oldVal) {
            if(val)
            {
                if(val.toUpperCase() !== oldVal.toUpperCase())
                {
                  this.listaLetras.splice(0)
                }
                this.palavra = val.toUpperCase()
            }
        }
    },
    computed: {
        exibirLetras() {
            const exibeLetra = (c) => this.temNaLista(c) ? c : '.'
            return [...this.palavra].map(exibeLetra)
        }
    },
    methods: {
        temNaLista(c) {
            return this.listaLetras.indexOf(c) > -1
        }
    },
    mounted() {
        this.palavra = this.palavra.toUpperCase();
    }
}
</script>

<style>
.letras {
    padding-bottom: 20px;
    padding-top: 20px;
}
.letra {
    /* padding-right: 10px; */
    margin: 0px;
    padding: 0px;
    display: inline-block;
    height: 40px;
    width: 50px;
    padding-top: 5px;
    margin-left: 10px;
    margin-right: 10px;
    border-bottom: 1px solid black;
    font-size: 30pt;
    text-align: center;
}
.grupo {
    font-size: 30px;
    text-transform: uppercase;
}
.dica {
  cursor: pointer;
  background-color: cornsilk;
  min-height: 50px;
  padding-top: 10px;
  font-size: 18px
}
</style>

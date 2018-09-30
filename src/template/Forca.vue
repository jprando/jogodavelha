<template>
    <div>
        <menu-jogo @reiniciar="iniciarJogo" />
        <div v-if="!HaUmVencedor">
            <abecedario @letra="jogar" v-if="!fimJogo" :palavra="partida.palavra"/>
            <div v-else class="fimJogo"> VOCE PERDEU </div>
        </div>
        <div class="venceu" v-else>
            VOCE GANHOU
        </div>
        <desenho
            :palavra="partida.palavra"
            :letra="letra"
            @fimJogo="fimJogo=true"
            @dica="exibirDica=true"/>
        <Letreiro
            :grupo="partida.grupo"
            :dica="exibirDica ? partida.dica : null"
            :palavra="partida.palavra" :letra="letra" />
        <Dica :dica="partida.dica" v-show="exibirDica"/>
    </div>
</template>

<script>
import ListaPalavras from "@/palavras";
import MenuJogo from "@/components/Menu";
import Abecedario from "@/components/Abecedario";
import Desenho from "@/components/Desenho";
import Letreiro from "@/components/Letreiro";
import Dica from "@/components/Dica";

export default {
  name: "Forca",
  components: { MenuJogo, Abecedario, Desenho, Letreiro, Dica },
  data() {
    return {
      letra: null,
      partida: { grupo: "", dica: "", palavra: "", palavraVencedora: "" },
      exibirDica : false,
      fimJogo: false,
      palavras : []
    };
  },
  computed: {
      HaUmVencedor() {
          if(this.letra){
            let palavraVencedora = [...this.partida.palavraVencedora]
            palavraVencedora = palavraVencedora
                .map(i => i == this.letra ? '': i)
                .filter(i => i != '' && i != ' ')
            this.partida.palavraVencedora = palavraVencedora.join('')
            return this.partida.palavraVencedora === ''
          } else return false
      }
  },
  methods: {
    jogar(letra) {
      this.letra = letra;
    },
    escolherPalavra() {
        let palavraAnterior = this.partida.palavra

        do {
            let idx = Math.floor(Math.random() * this.palavras.length)
            this.partida = this.palavras[idx]
            this.partida.palavraVencedora = this.partida.palavra
        } while(palavraAnterior === this.partida.palavra)
    },
    iniciarJogo() {
        this.fimJogo = false
        this.letra = null
        this.exibirDica = false
        this.escolherPalavra()
    }
  },
  mounted() {
      this.palavras = ListaPalavras.map(i => {
          i.palavra = i.palavra.toUpperCase()
          return i
      })
      this.iniciarJogo()
    }
}
</script>

<style>
.menu {
  height: 40px;
  background-color: beige;
}
.abecedario {
  background-color: azure;
}
.desenho {
  height: 300px;
  background-color: antiquewhite;
}
.palavra {
  padding-bottom: 10px;
  background-color: aliceblue;
}
.fimJogo {
    padding-top:30px;
    padding-bottom:30px;
    font-size: 40px;
    color: red
}
.venceu {
    padding-top:30px;
    padding-bottom:30px;
    font-size: 40px;
    color: green
}
</style>

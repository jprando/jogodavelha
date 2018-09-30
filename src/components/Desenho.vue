<template>
    <div class="desenho">
        <div style="height:15px">
            <span v-show="ultimaLetra">
                ultima letra {{ ultimaLetra }}
            </span>
        </div>
        <div>
            <div style="padding-left:90px">
                <svg xmlns="http://www.w3.org/2000/svg" height="400px">
                    <g id="svgCabeca" v-show="posicao > 0">
                        <ellipse
                        style="stroke-width:1;fill:#ffffff;stroke:#000000;stroke-opacity:1;stroke-miterlimit:4;stroke-dasharray:none"
                        ry="37.797619"
                        rx="39.6875"
                        cy="47.535713"
                        cx="103.94346"
                        id="path3713" />
                    </g>
                    <g id="svgOlhoEsquerdo" v-show="posicao > 6">
                    <circle
                        r="7.9375"
                        cy="37.330357"
                        cx="87.3125"
                        id="path4562"
                        style="fill:#ffffff;stroke:#000000;stroke-width:1;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
                    </g>
                    <g id="svgOlhoDireito" v-show="posicao > 7">
                    <circle
                        r="7.9375"
                        cy="37.330338"
                        cx="118.38227"
                        id="path4562-3"
                        style="fill:#ffffff;stroke:#000000;stroke-width:1;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
                    </g>
                    <g id="svgNariz" v-show="posicao > 8">
                    <path
                        inkscape:connector-curvature="0"
                        id="path4581"
                        d="m 102.05357,39.976189 c 0,0 -24.190477,21.166666 0,19.654763"
                        style="fill:none;stroke:#000000;stroke-width:1;stroke-linecap:butt;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;stroke-dasharray:none" />
                    </g>
                    <g id="svgBoca" v-show="posicao > 9">
                    <path
                        inkscape:connector-curvature="0"
                        id="path4583"
                        d="m 87.671741,72.673795 c 0,0 14.958979,-11.518974 28.767269,0"
                        style="fill:none;stroke:#000000;stroke-width:0.87928796;stroke-linecap:butt;stroke-linejoin:miter;stroke-miterlimit:4;stroke-dasharray:none;stroke-opacity:1" />
                    </g>
                    <g id="svgCorpo" v-show="posicao > 1">
                    <path
                        inkscape:connector-curvature="0"
                        id="path4524"
                        d="m 102.05357,84.577379 c 0,141.363091 0,141.363091 0,141.363091"
                        style="fill:none;stroke:#000000;stroke-width:1;stroke-linecap:butt;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;stroke-dasharray:none" />
                    </g>
                    <g id="svgBracoDireito" v-show="posicao > 2">
                    <path
                        inkscape:connector-curvature="0"
                        id="path4534"
                        d="m 101.29762,116.32738 77.86309,36.28571"
                        style="fill:none;stroke:#000000;stroke-width:1;stroke-linecap:butt;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;stroke-dasharray:none" />
                    </g>
                    <g id="svgBracoEsquerdo" v-show="posicao > 3">
                    <path
                        inkscape:connector-curvature="0"
                        id="path4536"
                        d="M 101.29762,116.32738 40.821427,154.125"
                        style="fill:none;stroke:#000000;stroke-width:1;stroke-linecap:butt;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;stroke-dasharray:none" />
                    </g>
                    <g id="svgPernaDireita" v-show="posicao > 4">
                    <path
                        inkscape:connector-curvature="0"
                        id="path4554"
                        d="m 102.05357,225.94047 58.96429,48.38096"
                        style="fill:none;stroke:#000000;stroke-width:1;stroke-linecap:butt;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;stroke-dasharray:none" />
                    </g>
                    <g id="svgPernaEsquerda" v-show="posicao > 5">
                    <path
                        inkscape:connector-curvature="0"
                        id="path4552"
                        d="M 102.05357,225.94047 43.845239,279.61309"
                        style="fill:none;stroke:#000000;stroke-width:1;stroke-linecap:butt;stroke-linejoin:miter;stroke-opacity:1;stroke-miterlimit:4;stroke-dasharray:none" />
                    </g>
                </svg>
            </div>
        </div>
    </div>
</template>

<script>
export default {
  name: "Desenho",
  data() {
      return {
          posicao : 0,
          ultimaLetra: null
      }
  },
  props:{
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
  watch: {
      letra(val) {
          if(val){
              this.ultimaLetra = val
              let naoTem = [...this.palavra].indexOf(val) == -1
              if(naoTem){
                  this.proximo()
              }
          }
      },
      palavra(newVal, oldVal) {
          if(newVal != oldVal){
              this.ultimaLetra = null
              this.posicao = 0
          }
      }
  },
  methods: {
      proximo() {
          this.posicao = this.posicao == 11 ? 11 : ++this.posicao
          if(this.posicao >= 4) this.$emit('dica')
          if(this.posicao == 11) this.$emit('fimJogo')
      }
  }
}
</script>

<style>
.des {
    background-color: white
}
</style>

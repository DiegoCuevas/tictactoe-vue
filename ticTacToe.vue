<template>
  <div id="app">
    <div class="status">Next player: {{ gameWord }}</div>
    <button @click.prevent="reload()">Reset</button>
    <template v-for="row in 3">
      <div class="row" :key="row">
        <button v-for="button in 3"
          :id="diferentKey(button, row)" class="square" style="width:40px;height:40px;" 
          :key="diferentKey(button,row)"
          @click.prevent="turnUp(diferentKey(button, row))" 
        >{{"-"}}</button>
      </div>
    </template>
  </div>
</template>

<script>
  export default {
    name: "App",
    data() {
      return {
        result: {"1": 1, "2": 2, "3":3, "4":4, "5":5, "6":6,"7":7, "8":8, "9":9},
        gameWord: 'X'
      };
    },
    methods:{
      reload(){
        window.location.reload(true)
      },
      diferentKey(button,row){
        if(row == 2){return button + row + 1 + ""}
        if(row == 3){return button + row + 3 + ""}
        return button + ""
      },
      turnUp(n){
        var button = document.getElementById(n);
        button.childNodes[0].nodeValue = this.gameWord 
        button.setAttribute('disabled', true)
        this.result[n] = this.gameWord
        this.gameWord = this.gameWord === "X" ? "O" : "X"
        this.checkMove(n)
      },
      checkMove(){
        if(this.result["1"] === this.result["2"] && this.result["2"] === this.result["3"]){alert("win " + this.result["3"])}
        if(this.result["4"] === this.result["5"] && this.result["5"] === this.result["6"]){alert("win " + this.result["6"])}
        if(this.result["7"] === this.result["8"] && this.result["8"] === this.result["9"]){alert("win " + this.result["9"])}
        if(this.result["1"] === this.result["5"] && this.result["5"] === this.result["9"]){alert("win " + this.result["9"])}
        if(this.result["3"] === this.result["5"] && this.result["5"] === this.result["7"]){alert("win " + this.result["7"])}
        if(this.result["1"] === this.result["4"] && this.result["4"] === this.result["7"]){alert("win " + this.result["7"])}
        if(this.result["2"] === this.result["5"] && this.result["5"] === this.result["8"]){alert("win " + this.result["8"])}
        if(this.result["3"] === this.result["6"] && this.result["6"] === this.result["9"]){alert("win " + this.result["9"])}
        return ""
      }
    }
  };
</script>
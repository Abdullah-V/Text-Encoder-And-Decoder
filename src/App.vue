<template>
  <div id="root">



    <div id="toolbar">

      <div id="tools">
        <b style="fontSize:20px;"><i>Secret Key: </i></b>
        <input type="range"  v-model="secretKey" min="-100" max="100">
        <input type="number" v-model="secretKey" min="-100" max="100">
        <button @click="encode">Encode</button>
        <button @click="decode">Decode</button>
        <button @click="copyOutput">Copy Output</button>
        <button @click="copyInput">Copy Input</button>
        <button @click="clear">Clear All</button>
      </div>

    </div>



<textarea id="input" v-model="input" placeholder="INPUT"  cols="30" rows="10"></textarea>
<textarea id="output" v-model="output" placeholder="OUTPUT"  cols="30" rows="10"></textarea>



  </div>
</template>



<script>

export default {
  data(){
    return {
      secretKey:31,
      input:'',
      output:'',
      herfler:"qwertyuiopasdfghjklzxcvbnmQWERTYUIOPASDFGHJKLZXCVBNM "
    }
  },
  methods:{
    clear(){
      this.input = ""
      this.output = ""
      document.getElementById("input").focus()
    },
    copyInput(){
      var copyText = document.getElementById("input")
      copyText.select()
      copyText.setSelectionRange(0, 99999)
      document.execCommand("copy")
      alert("Output text is copied: " + copyText.value);
    },

    copyOutput(){
      var copyText = document.getElementById("output")
      copyText.select()
      copyText.setSelectionRange(0, 99999)
      document.execCommand("copy")
      alert("Output text is copied: " + copyText.value);
    },
    decode(){
      if(this.secretKey < 0){
        this.secretKey *= -1
      }
      this.output = ""
      var input = this.input.trim()
      for(var i of input){
        if(this.herfler.includes(i)){
          var mykey = Number(this.herfler.indexOf(i)) - Number(this.secretKey)
          while(mykey < 0){
            mykey += 53
          }
          this.output += this.herfler[mykey]
        }
        else{
          this.output += i
        }
      }

    },
    encode(){
      if(this.secretKey < 0){
        this.secretKey *= -1
      }
      this.output = ""
      var input = this.input.trim()
      for(var i of input){
        if(this.herfler.includes(i)){
          var mykey = Number(this.herfler.indexOf(i)) + Number(this.secretKey)
          while(mykey >= 53){
            mykey -= 53
          }
          this.output += this.herfler[mykey]
        }
        else{
          this.output += i
        }
      }
    }
  }
}
</script>



<style>


::selection{
  color: rgb(255, 255, 255);
  background-color:rgb(0, 0, 0) ;
}
textarea{
  resize: none;
  width: 90%;
  height: 38%;
  position: absolute;
  transform: translate(-50%,-50%);
  border:2px solid black;
  outline: none;
}



#input{
  top:35%;
  left:50%;
  background-color: #252830;
  font-size: 21px;
}

#output{
  top:75%;
  left:50%;
  background-color: #252830;
  font-size: 21px;
}


#toolbar{
  position: absolute;
  left: 50%;
  top: 6%;
  width: 100%;
  height: 13%;
  transform: translate(-50%,-50%);
  background-color:#252830;
}


#toolbar input{
  margin: 5px 10px;
  outline: none;
}


#tools button{
  margin: 5px 10px;
  width: 100px;
  height: 30px;
  border-top: 5px solid #cfad16;
  outline: none;
  background-color: #131417;
  color: white;
  /* border-bottom:1px solid black;
  border-left: 1px solid black;
  border-right:1px solid black; */
}


#tools{
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%,-50%);
  display: inline-block;
}


body{
  background-color:#131417;
  box-sizing: border-box;
}




input[type='range'] {
  overflow: hidden;
  width: 80px;
  -webkit-appearance: none;
  background-color: #9a905d;
  outline: none;
}

input[type='range']::-webkit-slider-runnable-track {
  height: 10px;
  -webkit-appearance: none;
  color: #cfad16;
  margin-top: -1px;
}

input[type='range']::-webkit-slider-thumb {
  width: 10px;
  -webkit-appearance: none;
  height: 10px;
  cursor: ew-resize;
  background: #434343;
  box-shadow: -80px 0 0 80px #cfad16;
}

</style>

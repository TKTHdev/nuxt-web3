<template>
  <div>
    <p> <input
      type="text" v-model="inputNumber" placeholder="input number"
    >
      <button @click="setNumber()"
      >
        Set Number to contract
      </button>
    </p>
    <p> <button
      @click="getNumber()" >
      Get Number from contract </button> Number:{{number}}
    </p>
    </div>
</template>
<script>
export default {
  data(){
    return{
      number: 0,
      inputNumber: 0
    }
  },
  methods: {
    getNumber:async function(){
      let ret= await this.$contract.methods.get().call()
      this.number=ret
    },
    setNumber: async function(){
      let accounts=await this.$web3.eth.getAccounts()
      let account= accounts[0]
      let ret= await this.$contract.methods.set(this.inputNumber).send({from: account})
    },
  },
}
</script>

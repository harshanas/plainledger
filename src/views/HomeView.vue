<template>
  <main>
    <TheWelcome />
  </main>
</template>

<script setup>
import TheWelcome from '@/components/TheWelcome.vue'

import { ethers } from "ethers"
import axios from "axios"
</script>

<script>
export default {
  mounted(){
    console.log(this.message)
    // this.getTransactions();
  },

  data() {
    return {
      message: 'Hello World!'
    }
  },

  methods:{
    async getTransactions(){
      const address = "0xb54B0b46e6c5A588BfB99b0f805ed144269d3161";
      const API_KEY = "65WT27W1952MN5HEB4INMDU8CZBP39B84D";

      const provider = new ethers.providers.Web3Provider(window.ethereum);
      
      const url = `https://api.polygonscan.com/api?module=account&action=txlist&address=${address}&startblock=0&endblock=99999999&sort=asc&apikey=${API_KEY}`
     

      const accounts = await provider.listAccounts();
     
      const transactions = await axios.get(url);

      for (let transaction of transactions.data.result){
        console.log(`${transaction.from} has sent ${transaction.value} to ${transaction.to}`)
      }


    }
  }
}
</script>
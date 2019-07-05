<template>
  <div>
    <p>{{data}}</p>
    <div>
      <h2>SAVE</h2>
      <label for="">KEY</label>
      <input type="text" v-model="key_inp">
      <label for="">Value</label>
      <input type="text" v-model="val_inp">
      <button @click="save">SAVE</button>
    </div>

    <div>
      <label for="">KEY</label>
      <input type="text" v-model="load_key_inp">
      <button @click="load">LOAD</button>
    </div>

    <div>{{items}}</div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

interface SampleData {
  name: string,
  age: Number
}
interface KVP {
  key: string,
  val: string 
}

const TEST_KEY: string = "TEST"

@Component
export default class HelloWorld extends Vue {
  
  private data: SampleData = {name:"", age: 0}

  private items: KVP[] = []

  private load_key_inp: string = ""
  private key_inp: string = ""
  private val_inp: string = ""

  created() {
    console.log(navigator);
    
    let a = localStorage.getItem(TEST_KEY);
    if (a != null) {
      console.log("FROM LS");
      
      this.data = JSON.parse(a);
    } else {
      setTimeout(() => {
        this.data = {name:"test", age: 101};
        localStorage.setItem(TEST_KEY, JSON.stringify(this.data));
      }, 1000);
    }
  }

  save() {
    let kvp: KVP = { key: this.key_inp, val: this.val_inp }
    localStorage.setItem(kvp.key, JSON.stringify(kvp));
    this.key_inp = "";
    this.val_inp = "";
  }

  load() {
    let a = localStorage.getItem(this.load_key_inp);
    if (a != null) {
      this.items.push(JSON.parse(a));
    }
  }



}
</script>
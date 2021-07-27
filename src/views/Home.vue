<template>
  <div class="home">
    <p class="greetText">{{greetText}}</p>
    <p>挨拶した回数 : {{count}}回</p>
    <p v-if="isRegulars">いつもありがとうございます</p>
    <p>
      <MyButton class="btn" :greet="greetText" @click="onMyButtonClick">挨拶する</MyButton>
    </p>
    <p>
      <ResetButton class="resetBtn" v-model="greetText"></ResetButton>
    </p>
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";
import MyButton from "/src/components/MyButton.vue";
import ResetButton from "/src/components/ResetButton.vue";

@Component({
  components: {
    ResetButton,
    MyButton
  }
})
export default class Home extends Vue {
  private count: number = 0;
  public greetText: string = "Hello";
  public get isRegulars(): boolean {
    return this.count >= 5;
  }
  @Watch("count")
  public countChanged() {
    if (this.count === 5) {
      alert("常連になりました");
    }
  }
  public onMyButtonClick(count: number) {
    this.count = count;
    this.greetText = "こんにちは";
  }
}
</script>

<style>
.greetText {
  margin: 4rem;
  font-size: 2rem;
  font-weight: bold;
}

.btn {
  width: 6rem;
  margin: 1rem;
  padding: 0.5rem;
  display: inline-block;
  overflow: hidden;
  letter-spacing: 2px;
  color: #fff;
  background: #2f84e6;
  outline: none;
  border: none;
  border-radius: 0.5rem;
  font-weight: bold;
  font-size: 0.9rem;
  cursor: pointer;
}

.resetBtn {
  width: 6rem;
  padding: 0.7rem;
  display: inline-block;
  overflow: hidden;
  letter-spacing: 2px;
  color: #fff;
  background: #e69d2f;
  outline: none;
  border: none;
  border-radius: 0.5rem;
  font-weight: bold;
  font-size: 0.9rem;
  cursor: pointer;
}
</style>


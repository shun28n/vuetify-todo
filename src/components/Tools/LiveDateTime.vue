<template>
  <div class="text-subtitle-1 ml-4">
    {{ date }}
  </div>
</template>

<script>
import { format } from "date-fns"; // dayjsもおすすめ
export default {
  data() {
    return {
      date: "",
    };
  },
  methods: {
    getDate() {
      this.date = format(new Date(), "MMMM d, H:mm:ss");
      setTimeout(this.getDate, 1000); // 1秒後にgetDateを実行し、ループさせる
    },
  },
  mounted() {
    // コンポーネントのindex.htmlへのマウント時にgetDateメソッドを呼び出す。
    this.getDate();
  },
};
</script>

<style>
</style>
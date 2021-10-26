<template>
  <div>
    <div class="loading" v-if="!load">
      <h1>Loading</h1>
    </div>
    <div class="" v-else>
      <h1>{{ test.Test }} {{ test.l }}</h1>
      <h2 v-for="(tests, i) in test.Test" :key="i">
        {{ tests }}
      </h2>
      <button @click="readFromFirestore">Run the test</button>
    </div>
    <h3>{{ inf.f }}</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      load: false,
      test: [],
      inf: ""
    };
  },
  methods: {
    async readFromFirestore() {
      let info = this.$fire.firestore.collection("testing");

      const messageRef = info.doc("3Aihd3yc5EOYpNIqvVyJ");
      const secondMessageRef = info.doc("el");
      try {
        const snapshot = await messageRef.get();
        const snapshotnd = await secondMessageRef.get();
        const doc = snapshot.data();
        const docnd = snapshotnd.data();
        this.test = doc;
        this.inf = docnd;
      } catch (e) {
        alert(e);
      }
      this.load = true;
    }
  },
  mounted() {
    this.readFromFirestore();
  }
};
</script>

<style lang="scss" scoped></style>

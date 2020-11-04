<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <span @click.stop="toggleShowOptions">Click me now</span>

    <div v-if="show" class="details" ref="details" tabindex="0">
      Lorem ipsum dolor sit amet, consectetur adipisicing elit. Accusamus
      similique alias error eligendi, qui nam tenetur accusantium labore illum
      mollitia eum! Sequi consequatur cupiditate molestiae facere. Dolorum vel
      repellat ut voluptatibus, voluptas labore. Illum dolorum a at corporis
      laudantium? Explicabo earum necessitatibus, amet itaque accusantium,
      voluptatibus quisquam voluptate provident blanditiis natus aspernatur esse
      modi quo! Eaque rem provident recusandae pariatur!
    </div>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data: () => ({
    show: false,
  }),
  props: {
    msg: String,
  },

  methods: {
    toggleShowOptions() {
      this.show = !this.show;

      this.$nextTick(() => {
        if (this.show) {
          this.$refs.details.focus();
        }
      });
    },

    handleBlur(event) {
      if (this.show) {
        if (this.$refs.details) {
          this.$refs.details.focus();
          if (event.target === this.$refs.details) {
            return;
          } else {
            this.show = false;
          }
        }
      }
    },
  },

  mounted() {
    document.addEventListener("click", (event) => this.handleBlur(event));
  },

  destroyed() {
    document.removeEventListener("click", this.handleBlur);
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
.details {
  margin: 30px 0;
}
span {
  margin: 20px 0;
  padding: 20px;
  background: teal;
  color: #fff;
  cursor: pointer;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>

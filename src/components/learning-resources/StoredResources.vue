<template>
  <div>
    <ul>
      <learning-resource
        v-for="res in resources"
        :key="res.id"
        :id="res.id"
        :title="res.title"
        :description="res.description"
        :link="res.link"
      ></learning-resource>
    </ul>
    <div v-if="showGradient" class="gradient"></div>
  </div>
</template>

<script>
import LearningResource from './LearningResource.vue';

export default {
  inject: ['resources'],
  data() {
    return {
      showGradient: true,
    };
  },
  components: {
    LearningResource,
  },
  methods: {
    handeScroll() {
      if (
        window.innerHeight + window.pageYOffset >=
        document.body.offsetHeight
      ) {
        console.log(this.showGradient);
        this.showGradient = false;
      } else {
        this.showGradient = true;
      }
    },
  },
  mounted() {
    window.addEventListener('scroll', this.handeScroll);
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
.gradient {
  position: fixed;
  bottom: 0px;
  width: 100%;
  height: 8rem;
  background-color: rgba(255, 255, 255, 0.712);
  filter: blur(10px);
  pointer-events: none;
}
</style>

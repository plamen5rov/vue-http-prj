<template>
  <section>
    <base-card>
      <h2>Submitted Experiences</h2>
      <div>
        <base-button @click="loadExperiences"
          >Load Submitted Experiences</base-button
        >
      </div>
      <ul>
        <survey-result
          v-for="result in results"
          :key="result.id"
          :name="result.name"
          :rating="result.rating"
        ></survey-result>
      </ul>
    </base-card>
  </section>
</template>

<script>
import SurveyResult from './SurveyResult.vue';

export default {
  components: {
    SurveyResult,
  },
  data() {
    return {
      results: [],
    };
  },
  methods: {
    loadExperiences() {
      fetch(
        'https://vue-http-demo-a8e94-default-rtdb.europe-west1.firebasedatabase.app/surveys.json'
      )
        .then((response) => response.json())
        .then((data) => {
          this.results = [];
          for (const key in data) {
            const result = {
              id: key,
              name: data[key].name,
              rating: data[key].rating,
            };
            this.results.push(result);
          }
        });
      // console.log(this.results);
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>

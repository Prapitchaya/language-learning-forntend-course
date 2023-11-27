<template>
  <div>
    <h2>Course Listings</h2>
    <div>
      <div v-for="course in courses" :key="course.id" class="course-card">
        <h3>{{ course.title }}</h3>
        <p>{{ course.description }}</p>
        <p>Price: {{ course.pricing }}</p>
        <p>Language: {{ course.language }}</p>
        <p>Level: {{ course.proficiency_level }}</p>
        <router-link :to="{ name: 'course-detail', params: { id: course.id } }">
          View Details
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      courses: [],
    };
  },
  mounted() {
    // Fetch course list from your API using Axios
    axios.get('http://your-api-base-url/api/courses') // Replace with your actual API base URL
      .then(response => {
        console.log('API Response:', response.data); // Debugging statement
        this.courses = response.data;
      })
      .catch(error => {
        console.error('Error fetching course list:', error);
      });
  },
};
</script>

<style scoped>
.course-card {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
}
</style>

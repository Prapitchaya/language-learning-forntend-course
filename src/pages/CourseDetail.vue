<template>
  <div v-if="course">
    <h2>{{ course.title }}</h2>
    <p>{{ course.description }}</p>
    <p>Syllabus: {{ course.syllabus }}</p>
    <p>Price: {{ course.pricing }}</p>

    <h3>Lesson Plans</h3>
    <ul>
      <li v-for="lessonPlan in course.lessonPlans" :key="lessonPlan.id">{{ lessonPlan.title }}</li>
    </ul>

    <h3>Sample Lessons</h3>
    <ul>
      <li v-for="lesson in course.sampleLessons" :key="lesson.id">{{ lesson.title }}</li>
    </ul>

    <!-- Link to navigate back to the course list -->
    <router-link :to="{ name: 'course-list' }">Back to Course List</router-link>
  </div>
  <div v-else>
    <p>Loading...</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      course: null,
    };
  },
  mounted() {
    // Fetch course details based on courseId from the route parameters
    const courseId = this.$route.params.id;

    // Fetch course details from your API
    axios.get(`/api/courses/${courseId}`)
      .then(response => {
        this.course = response.data;
      })
      .catch(error => {
        console.error('Error fetching course details:', error);
      });
  },
};
</script>

<style scoped>
/* Add your styles here */
</style>

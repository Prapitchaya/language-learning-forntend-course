<template>
  <q-page class="course-list-page q-pa-md">
    <div v-if="courses.length > 0">
      <h2 class="q-mb-md text-h6">Course Listing</h2>
      <q-list bordered>
        <q-item v-for="course in courses" :key="course.course_id">
          <q-item-section>
            <q-item-label>
              <h4 class="text-h6 q-mb-sm">{{ course.title }}</h4>
              <p class="q-mb-md">{{ course.description }}</p>
            </q-item-label>
          </q-item-section>
          <q-item-section side top>
            <q-item-label>
              <div class="q-mb-xs">
                <strong>Language:</strong> {{ course.language }}
              </div>
              <div class="q-mb-xs">
                <strong>Proficiency Level:</strong>
                {{ course.proficiency_level }}
              </div>
              <div class="q-mb-xs">
                <strong>Instructor:</strong> {{ course.instructor_name }}
              </div>
              <div class="text-primary">
                <strong>Pricing:</strong> ${{ course.pricing }}
              </div>
            </q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </div>
    <div v-else>
      <q-spinner-square size="80px" color="primary" />
      <div class="q-mt-md text-h6">No courses available</div>
    </div>
  </q-page>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      courses: [],
    };
  },
  methods: {
    async fetchCourses() {
      try {
        // const response = await axios.get("http://localhost:3000/api/courses");
        const response = await axios.get(
          "https://language-learning-backend-rosy.vercel.app/api/courses"
        );
        this.courses = response.data;
      } catch (error) {
        console.error("Error fetching courses", error);
      }
    },
  },
  async created() {
    await this.fetchCourses();
  },
};
</script>

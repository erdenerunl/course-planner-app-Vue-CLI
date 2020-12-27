<template>
  <div>
    <header>Course Planner with Vue CLI</header>
    <add-course-section 
    :courseData="courseData" 
    @addEvent="addEvent" 
    :isEmpty="isEmpty" />

    <div class="card card-light mt-20">
      <h3>My Course List</h3>
      <course-list :courseList="courseList"/>
    </div>

  </div>
</template>

<script>
import axios from "axios";
import AddCourseSection from "./components/AddCourseSection.vue";
import CourseList from "./components/CourseList.vue";

export default {
  name: "App",
  components: {
    AddCourseSection,
    CourseList,
  },
  data() {
    return {
      courseData : {
        title : null,
        checked: false
      },
      courseList: [],
      isEmpty: false,
    };
  },
  created() {
    axios.get("http://localhost:3000/courses").then((r) => {
      this.courseList = r.data;
    });
  },
  methods: {
    clearData() {
      this.courseData = {
        title: null,
        checked: false,
      };
    },
    addEvent(courseItem) {
      if (courseItem.title.length > 0) {
        this.courseList.push({ id: this.courseList.length + 1, ...courseItem });
        this.clearData();
      } else {
        setTimeout(() => {
          this.isEmpty = false;
        }, 2000);
        this.isEmpty = true;
      }
    },
  },
};
</script>

<style>
</style>

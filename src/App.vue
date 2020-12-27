<template>
  <div>
    <header>Course Planner with Vue CLI</header>
    <add-course-section :courseData="courseData" @addEvent="addEvent" :isEmpty="isEmpty" />

    <div class="card card-light mt-20">
      
      <course-list :courseList="courseList" @bgChangeEvent="bgChangeEvent" @deleteEvent="deleteEvent" />
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
      courseData: {
        title: "",
        checked: false,
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
        title: "",
        checked: false,
      };
    },
    addEvent(responseItem) {
      if (this.courseData.title.length > 0) {
        axios
          .post("http://localhost:3000/courses", responseItem)
          .then((response) => {
            this.courseList.push({ id: this.courseList.length + 1, ...response.data });
            this.clearData();
          })
          .catch((e) => alert(e));
      } else {
        setTimeout(() => {
          return (this.isEmpty = false);
        }, 2000);
        return (this.isEmpty = true);
      }
    },
    bgChangeEvent(checkedCourse){
      const uptadeID = checkedCourse.id
      const matched = this.courseList.findIndex(c => c.id === checkedCourse.id);

      axios.patch(`http://localhost:3000/courses/${uptadeID}` , this.courseList[matched])
    },
    deleteEvent(courseID){
      const matched = this.courseList.findIndex(c => c.id === courseID);
      axios.delete(`http://localhost:3000/courses/${courseID}` , this.courseList[matched] )

      this.courseList = this.courseList.filter(c => c.id !== courseID)
    }
  },
  
};
</script>

<style>
</style>

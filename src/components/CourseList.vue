<template>
  <div class="card card-light mt-20">
    <h3>My Course List</h3>
    <!-- <input type="text" class="w-100 m-5" v-model="searchCourse" placeholder="Kurs Ara..." 
    v-if="courses.length > 0" /> -->
    <div>
      <div class="notification-box">
        <small v-if="courseList.length > 0">
          You have <span class="ct1"> {{ control1 }} </span> courses to watch.
        </small>
        <small v-else> There is no course to watch...</small>
        <small v-if="courseList.length > 0" >
          <span class="ct2 ml-5"> {{ control2 }} </span> courses have been completed.
        </small>
      </div>
    </div>
    <ul class="list mt-20">
      <li class="course-item list-item" v-for="(course, index) in courseList" :key="course.id" :class="backgroundChange(course)">
          <button @click="deleteEvent(course.id)" class=" btn-warning btn-sm" >X</button>
        <span>{{ index + 1 }}. {{ course.title }} </span>
        <input type="checkbox" v-model="course.checked" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  props: ["courseList"],
  methods: {
    backgroundChange(checkedCourse) {
      this.$emit("bg-change-event", checkedCourse);
      return {
        "bg-danger": checkedCourse.checked === false,
        "bg-success": checkedCourse.checked === true,
      };
    },
    deleteEvent(courseID){
        this.$emit('delete-event' , courseID)
    }
  },
  computed: {
    control1() {
      return this.courseList.filter((x) => !x.checked).length;
    },
    control2() {
      return this.courseList.filter((v) => v.checked).length;
    },
  },
};
</script>

<style lang="css" scoped>
.list-item {
  height: 50px;
}
.ct1 {
  font-weight: 600;
  color: #c64b4b;
}
.ct2 {
  font-weight: 600;
  color: #6dc454;
}
</style>


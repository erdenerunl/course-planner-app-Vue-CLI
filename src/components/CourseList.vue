<template>
  <div>
    <!-- <input type="text" class="w-100 m-5" v-model="searchCourse" placeholder="Kurs Ara..." 
    v-if="courses.length > 0" /> -->
    <ul class="list mt-20">
      <li class="course-item list-item" v-for="course in courseList" :key="course.id" 
      :class="backgroundChange(course)">
        <span>{{ course.id }}. {{ course.title }} </span>
        <input type="checkbox" v-model="course.checked" />
      </li>
    </ul>
  </div>
</template>

<script>
export default {
    props : ["courseList"],
    methods : {
        backgroundChange(checkedCourse){
            this.$emit('bg-change-event', checkedCourse)
            return {
                "bg-danger" : checkedCourse.checked === false,
                "bg-success" : checkedCourse.checked === true,      
        }
            }
    }
}





</script>


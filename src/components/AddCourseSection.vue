<template>
  <div class="container">
    <div class="course--planner-app--container">
      <div class="card">
        <div class="user--action--container">
          <div class="form-group">
            <label>Course Name</label>
            <input type="text" v-model="courseData.title" placeholder="Add course..." />
            <span class="bg-danger alert" v-if="isEmpty">You must add something !!</span>
          </div>
          <button class="btn-primary btn-sm" @click="addCourse()">Add Course</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>

import axios from 'axios';
export default {
  props : ["courses", "isEmpty" ,"courseData"],
  data(){
    return {
      
      
    }
  },
  methods : {
    addCourse(){
      this.$emit('add-event', this.courseData)
    }
  }
  
};
</script>


<style scoped>
</style>

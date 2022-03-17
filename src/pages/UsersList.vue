<template>
  <div>
    <button @click="confirmInput">Confirm</button>
    <button @click="saveChanges">Save Changes</button>
    <ul>
      <user-item v-for="user in users" :key="user.id" :name="user.fullName" :role="user.role"></user-item>
    </ul>
  </div>
</template>

<script>
import UserItem from '../components/users/UserItem.vue';

export default {
  components: {
    UserItem,
  },
  inject: ['users'],
  data(){
    return {
      isSavedChanges: false,
    };
  },
  methods: {
    confirmInput() {
      // do something
      this.$router.push('/teams');
    },
    saveChanges(){
      this.isSavedChanges = true;
    },
  },
  beforeRouteEnter(to, from, next){
    console.log('UsersList component beforeEnter');
    console.log(to, from);
    next();
  },
  beforeRouteLeave(to, from, next){
    console.log('UsersList component beforeRouteLeave');
    console.log(to, from);
    if(!this.isSavedChanges){
      const userLeaving = confirm('Are you sure to leave before saving the changes?');
      next(userLeaving);
    } else {
      next();
    }
  },
  unmounted(){
    console.log('Unmounted');
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 2rem auto;
  max-width: 20rem;
  padding: 0;
}
</style>
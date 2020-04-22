<template>
    <div>
      <select @change="handleSelectChange">
          <option v-for="(breed, index) in breeds" :key="index">{{breed}}</option>
      </select>
    </div>
</template>

<script>
export default {
    name: 'SelectBreed',
    props: {
        breeds: Array,
        onBreedSelection: Function
    },
    data: function () {
        return{
            currentBreed: '',
        }
    },
    methods: {
        handleSelectChange(e){
            this.currentBreed = e.target.value;
            this.onBreedSelection(this.currentBreed);
        }
    },
}
</script>

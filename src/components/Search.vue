<template>
  <div class="container">
    <input
      class="form-control"
      type="text"
      v-model="title" 
      @keyup.enter="apply"
      placeholder="Search for Movies & Series" />
    <div class="selects">
      <select
        v-for="filter in filters"
        v-model="$data[filter.name]"
        :key="filter.name"
        class="form-select">
        <option
          v-if="filter.name === 'year'"
          value="">
          All Years
        </option>
        <option
          v-for="item in filter.items"
          :key="item">
          {{ item }}
        </option>
      </select>
    </div>
    <button
      class="btn btn-primary"
      @click="apply">
      Apply
    </button>
  </div>
</template>

<script>

export default {
  data(){
    return{
      title:'',
      type:'movie',
      number:10,
      year: '',
      filters : [
        {
          name:'type',
          items:['movie','series','episode']
        },
        {
          name:'number',
          items:[ 10, 20, 30]
        },
        {
          name:'year',
          items: (function(){
            const years = [];
            const thisYear = new Date().getFullYear();
            for (let i = thisYear; i >= 1985; i--) {
              years.push(i);
            }
            return years;
          })()
        }
      ]
    }
  },
  methods:{
    apply(){
                  //movie : module의 이름 
      this.$store.dispatch('movie/serachMovies', {
        title : this.title,
        type : this.type,
        number : this.number,
        year : this.year,
      })
    }
  }
}
</script>

<style lang="scss" scoped>
.container{
 display:flex; 
 > * {
   margin-right: 10px;
   font-size: 15px;
   &:last-child{
     margin-right: 0px;
   }
 }
  .selects {
    display: flex;
    > * {
      margin-right: 10px;
      &:last-child{
        margin-right: 0px;
      }
    }
    select{
      width:120px;
    }
  }
  .btn {
    width:120px;
    height: 50px;
    font-weight: 700;
    flex-shrink: 0;
  }

  @include media-breakpoint-down(lg){
    display: block;
    input{
      margin-right: 0;
      maring-bottom:10px;
    }
    .selects{
      margin-right: 0;
      margin-bottom: 10px;
      select{
        width: 100%;
      }
    }
    .btn{
      width: 100%;
    }
  }
}
</style>
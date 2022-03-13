<template>
  <div class="text-center pt-25">
    <h2 class="text-3xl font-bold">{{ text }}</h2>
    <div class="text-2xl mt-4 mb-10">
      {{ dataDate }}
    </div>
  </div>
</template>

<script>
import moment from 'moment'

export default {
    name : 'DataTitle',
    props : ['text', 'dataDate'],
    computed : {
timestamp : function(){
    return moment(this.dataDate).format('MMM Do YYYY, h:mm:ss a')
}
    }
};
</script>

<style>
</style>
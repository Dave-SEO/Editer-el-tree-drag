<template>
  <div class="hello">
    <tinymce></tinymce>
    <eltree></eltree>
  </div>
</template>

<script>
import tinymce from '@/components/Tinymce'
import eltree from '@/components/eltree'
export default {
  name: 'HelloWorld',
  data () {
    return {
    }
  },
  components: {
    tinymce,
    eltree
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>

<template>
  <div>
    <FormSearch />
    <Navbar />
    <Carousel />
  </div>
</template>

<script>
import FormSearch from '@/components/FormSearch'
import Navbar from '@/components/Navbar'
import Carousel from '@/components/Carousel'

export default {
  components: { FormSearch, Navbar, Carousel }
}

</script>

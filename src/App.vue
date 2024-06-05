<template>
  <div>
    <Header />
    <div class="filter-wrapper">
      <FilterPanel @update:name="name = $event" @update:status="status = $event"/>
    </div>
    <CardsList :name="name" :status="status" />
    <Footer/>
  </div>
</template>

<script>
import { ref } from 'vue'
import Header from "./components/Header.vue";
import FilterPanel from './components/FilterPanel.vue'
import CardsList from './components/CardsList.vue'
import Footer from './components/Footer.vue'

export default {
  setup() {
    const name = ref('')
    const status = ref('')

    return {
      name,
      status
    }
  },
  components: {
    Header,
    FilterPanel,
    CardsList,
    Footer
  }
}
</script>

<style scoped>
.filter-wrapper {
  position: absolute;
  top: 50%; 
  left: 50%;
  transform: translate(-50%, -50%);
  z-index: 2; 
  width: 50%; 
}
</style>

<template>
  <div>
    <NavBar/>

    <b-img src="~/assets/restaurant.jpg"  alt="Responsive image" style="max-height:700px; width: 100%;"></b-img>
    <b-row class="centered">
      <b-col>
        <h1  style="color: white;"> Search Restaurants</h1>
        <b-button  to="/restaurants" variant="success">Search Now</b-button>
      </b-col>
      <!-- <h1 class="centered" style="color: white;"> Search Restaurants</h1> -->
    </b-row>

  </div>
</template>


<script>
import NavBar from '@/components/NavBar'
export default {
  name: 'IndexPage',
  components:{
    NavBar,
  }

}
</script>

<style>
.centered {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}

</style>
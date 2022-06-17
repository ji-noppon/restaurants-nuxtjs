<template>
    <div>
      <NavBar/>
      <b-container fluid="md" class="py-2">

         <b-form-row>
            <b-col cols="4"></b-col>
            <b-col cols="5">
               <b-form inline >
                  <b-form-group label-align="center" label="Restaurants" label-size="lg"  >
                     <b-form-input type ="text"  placeholder="ระบุสถานที่" v-model="form.place"></b-form-input>
                     <b-button variant="success" v-on:click="search()">Search</b-button>
                  </b-form-group>  
               </b-form>
            </b-col>
            <b-col cols="3"></b-col>
         </b-form-row>

         <b-table class = "mt-3" :items="items" :fields="fields">

         </b-table>
      </b-container>   
    </div>
</template>

<script>
    export default {
      data(){
         return{
            form:{
               place:"Bang sue"
            },

            fields: [
               {
                  key: 'name',
                  sortable: true
               },
               {
                  key: 'location',
                  sortable: false
               },
               {
                  key: 'status',
                  sortable: true,
               }
            ],

            items: [
               /* { isActive: true, status: 40, name: 'Dickerson', location: 'Macdonald' }, */
            ],
         }
      },

      async asyncData({$axios}) {
      //console.log(process.env.Text_ENV);
         let url="location=Bang sue"
         let res = encodeURI(url)
         const restaurants = await $axios.$get(`http://127.0.0.1:8000/place?${res}`);
         let items =[]
         for (let i = 0; i < restaurants.results.length; i++) {
            let open  =""   
            if(restaurants.results[i].opening_hours){
               open = restaurants.results[i].opening_hours.open_now ? "เปิด":"ปิด"
            }else{
               open = "ไม่ได้ระบุ"
            }
            items.push({name:    restaurants.results[i].name,
                        location:restaurants.results[i].vicinity,
                        status:  open,
                     })
         }
         return {items };
      },

      methods: {
         search(){
            let url="location="+this.form.place
            let res = encodeURI(url)
            console.log(url);

            this.$axios.get(`http://127.0.0.1:8000/place?${res}`).then(response => {
               console.log( response.data.results)

               let restaurants = response.data           
               this.items=[]

               for (let i = 0; i < restaurants.results.length; i++) {
                  let open  =""   
                  if(restaurants.results[i].opening_hours){
                     open = restaurants.results[i].opening_hours.open_now ? "เปิด":"ปิด"
                  }else{
                     open = "ไม่ได้ระบุ"
                  }
                  this.items.push({name:    restaurants.results[i].name,
                              location:restaurants.results[i].vicinity,
                              status:  open,
                           })
               }
            })
         },
      },
}

</script>


<style scoped>  /* scoped = edit style place file only  */

</style>
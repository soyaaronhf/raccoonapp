<template>
<div>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-lg-4 py-4">
        <img src="./assets/logo.png" alt="Raccoon" class="w-100">
      </div>
    </div>
    <div class="row justify-content-center">
      <div class="col-12">
        <h2 class="text-center mb-3 mb-lg-5">{{question}}</h2>
      </div>
      <div v-if="id_feeling" class="col-12">
        <h2 class="text-center mb-3 mb-lg-5">{{id_feeling}}</h2>
      </div>
      <div class="col-lg-6 pb-4">
        <my-table @openModal="openModal" :id_feeling.sync="id_feeling" :feelings="feelings"></my-table>
      </div>
    </div>
  </div>
  <transition name="bounce">
    <my-modal @selectAndClose="selectAndClose" @openModal="openModal" :feeling_data="feeling" v-if="open_modal"></my-modal>
  </transition>
  <transition name="fade">
    <div v-if="open_modal" class="overlay"></div>
  </transition>
</div>
</template>

<script>
import myTable from './components/table.vue'
import myModal from './components/modal.vue'

export default {
  data () {
    return {
      question:'¿En la escala de raccoon cómo te sientes hoy?',
      id_feeling:false,
      feelings:false,
      feeling:false,
      open_modal:false,
    }
  },
  methods:{
    getData(){
            this.$http.get('http://54.196.43.91:3000/raccoon/feelings/').then(response => {
                this.feelings = response.body.feelings;
            }, response => {
              console.log('error getting data');
            });
        },
    openModal(feeling){
      if(feeling){
        this.feeling=feeling;
        this.open_modal=true;
        document.querySelector("body").classList.add('modal-open');
      }else{
        this.open_modal=false;
        document.querySelector("body").classList.remove('modal-open');
      }
    },
    selectAndClose(id_feeling){
      this.id_feeling=id_feeling;
      this.open_modal=false;
      document.querySelector("body").classList.remove('modal-open');
    }
  },
  components:{
    myTable,
    myModal
  },
  created(){
    this.getData();
  }
}
</script>

<style lang="scss">
h2{
  font-family: 'Fira Sans', sans-serif;
  font-size: 40px;
  font-weight: 700;
}
.btn,th,td{
  font-family: 'Montserrat', sans-serif;
}
.table td, .table th{
  vertical-align: middle;
}
.btn-danger{
  background-color: #E11C4C;
  padding: .25rem 1rem;
  border:1px solid #E11C4C;
}
.btn-danger:hover{
    color: #E11C4C;
    background-color: #FFFFFF;
}
.overlay{
  background: rgba(0, 0, 0, .4);
  position: fixed;
  top: 0;
  right: 0;
  left: 0;
  bottom: 0;
}
.bounce-enter-active {
  animation: bounce-in .4s;
}
.bounce-leave-active {
  animation: bounce-in .4s reverse;
}
@keyframes bounce-in {
  0% {
    opacity: 0;
    transform: scale(0);
  }
  50% {
    opacity: 1;
    transform: scale(1.1);
  }
  100% {
    transform: scale(1);
  }
}
.fade-enter-active {
  animation: fade-in .3s;
}
.fade-leave-active {
  animation: fade-in .3s reverse;
}
@keyframes fade-in {
  from{
    opacity: 0;
  }
  to{
    opacity: 1;
  }
}
</style>

<template>
    <div class="mymodal">
        <div class="container">
            <div class="row">
                <div class="col-12 px-0">
                    <img class="w-100" :src="feeling_data.imgUrl" alt="">
                </div>
                <div class="col-12 py-3">
                    <h4 class="mb-3">{{feeling_data.desc}}</h4>
                    <button @click="$emit('openModal')" class="btn btn-danger btn-sm mr-2">Cerrar</button>
                    <button @click="$emit('selectAndClose', feeling_data.id)" class="btn btn-danger btn-sm">Justo así</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props:['feeling_data']
}
</script>

<style lang="scss" scoped>
.mymodal{
    position: fixed;
    top: 50px;
    z-index: 2;
    width: 100%;
    max-width: 350px;
    min-width: 300px;
    overflow: hidden;
    background: #fff;
    margin: 0 auto;
    left: 0;
    right: 0;
    border-radius: 5px;
    box-shadow: rgba(0, 0, 0, 0.1) 0px 5px 10px;
}
</style>

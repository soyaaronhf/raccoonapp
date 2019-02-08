<template>
    <table class="table table-striped">
        <thead>
            <tr>
            <th scope="col">#</th>
            <th scope="col">Me siento...</th>
            <th scope="col">Acciones</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="feeling of feelings" :key="feeling.id">
                <th scope="row">{{feeling.id}}</th>
                <td>{{feeling.desc}}</td>
                <td>
                    <button @click="$emit('openModal',feeling)" class="btn btn-danger btn-sm mr-2">Detalle</button>
                    <button @click="$emit('update:id_feeling', feeling.id)" class="btn btn-danger btn-sm">Elegir</button>
                </td>
            </tr>
        </tbody>
    </table>
</template>

<script>
export default {
    data(){
        return{
        }
    },
    methods:{
    },
    props:['id_feeling','feelings'],
}
</script>
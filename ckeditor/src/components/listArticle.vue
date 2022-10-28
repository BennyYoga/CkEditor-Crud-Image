<template>
    <div class="card" v-for="data in editorData" :key="data.id">
        <span>
            <br>
            <h4>{{data.title}}</h4>
            <p v-html="data.body"></p>
            <span>{{dateConversion(data.date)}}</span>
            <button @click="getID(data.id)"> Edit </button>
            <button> Delete </button>
            <hr>
        </span>
    </div>
</template>

<script>
export default {
    name: 'listArticle',
    props: {
        editorData: Array
    },
    data(){
        return{
            idData : ""
        }
    }, 
    methods: {
        dateConversion : function(date) {
            const data = date;
            var print = new Date(data);
            print = print.toString().substring(0, 25)
            return print;
        },
        getID(data){
            this.$emit('get-data-ID',data)
            this.idData = null;
        }
    }
}
</script>
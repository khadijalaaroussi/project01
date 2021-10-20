<template>
    <div class="container">
        <form @submit.prevent="submit">
            <div>
                <label for="title">Title</label>
                <input type="text" V-model="form.title">
             </div>
             <div>
                 <label for="body">Body</label>
                 <input type="text" V-model="form.body">
             </div>
             <input type="submit" value="submit">
        </form>
    <div>
    <table>
        <tr>
            <th>title</th>
            <th>body</th>
           </tr>
</div>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        name:'ExampleComponent',
        data:()=>({
            form:{
                title:null,
                body:null,
            },
           posts:null,
        }),
        methods:{
            Submit(){
             axios.post('http://localhost:8000/api/posts',this.form).then(res=>{
                 console.log("res from api",res.data)

             }) .catch(err=>{
                 console.log("error",err.response)
             })
            },
            get(){
                axios.get('http://localhost:8000/api/posts').then(res=>{
                    this.posts=res.data

                }).catch(err=>{ console.log("error",err.response)

                })

            }

        },
        update(id){
            axios.put('http://localhost:8000/api/posts'+id,this.form).then(res=>{
                console.log("res",res.data)
            }).catch(err=>{ console.log("error",err.response)
            })
        },
        delete(id){
            axios.delete('http://localhost:8000/api/posts'+id).then(res=>{
                console.log('deleted',res.data)
                this.get();
            })
        },
        created(){
            this.get();
        },

         mounted() {
            console.log('Component mounted.')
        }
    }
</script>

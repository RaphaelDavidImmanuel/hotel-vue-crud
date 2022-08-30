<template> 
    <div class="container mt-5"> 
        <div class="row"> 
            <div class="col-md-12"> 
                <div class="card border-0 rounded shadow"> 
                    <div class="card-body"> 
                        <h4>TAMBAH KAMAR</h4> 
                        <hr> 
 
                        <form @submit.prevent="store"> 
                            <div class="form-group"> 
                                <label for="kamar" class="font-weight-bold">NO KAMAR</label> 
                                <input type="text" class="form-control" v-model="kamar.no_kamar" placeholder="Masukkan No kamar"> 
                                <!-- validation --> 
                                <div v-if="validation.no_kamar" class="mt-2 alert alert-danger"> 
                                    {{ validation.no_kamar[0] }} 
                                </div> 
                            </div> 
                            <div class="form-group"> 
                                <label for="kamar" class="font-weight-bold">HARGA</label> 
                                <input type="text" class="form-control" v-model="kamar.harga" placeholder="Masukkan Harga"> 
                                <!-- validation --> 
                                <div v-if="validation.harga" class="mt-2 alert alert-danger"> 
                                    {{ validation.harga[0] }} 
                                </div> 
                            </div> 

                            <div class="form-group"> 
                                <label for="kamar" class="font-weight-bold">KAPASITAS</label> 
                                <input type="text" class="form-control" v-model="kamar.kapasitas" placeholder="Kapasitas kamar"> 
                                <!-- validation --> 
                                <div v-if="validation.kapasitas" class="mt-2 alert alert-danger"> 
                                    {{ validation.kapasitas[0] }} 
                                </div> 
                            </div> 

                            <div class="form-group"> 
                                <label for="kamar" class="font-weight-bold">TIPE</label> 
                                <input type="text" class="form-control" v-model="kamar.tipe" placeholder="Tipe kamar"> 
                                <!-- validation --> 
                                <div v-if="validation.tipe" class="mt-2 alert alert-danger"> 
                                    {{ validation.tipe[0] }} 
                                </div> 
                            </div> 
                           
                            <button type="submit" class="btn btn-primary">SIMPAN</button> 
                        </form>                         
 
                    </div> 
                </div> 
            </div> 
        </div> 
    </div> 
</template> 
 
<script> 
import { reactive, ref } from 'vue' 
import { useRouter } from 'vue-router' 
import axios from 'axios' 
 
export default { 
 
    setup() { 
 
        //state posts 
        const kamar = reactive({ 
            no_kamar:"", 
            harga:"",
            kapasitas:"",
            tipe:"",
        }) 
 
        //state validation 
        const validation = ref([]) 
 
        //vue router 
        const router = useRouter() 
 
        //method store 
        function store() { 
 
            let no_kamar = kamar.no_kamar 
            let harga = kamar.harga 
            let kapasitas = kamar.kapasitas
            let tipe = kamar.tipe
 
            axios.post('http://127.0.0.1:8000/api/kamar', { 
                no_kamar: no_kamar,
                harga: harga,
                kapasitas: kapasitas,
                tipe: tipe,

            }).then(() => { 
 
                //redirect ke post index 
                router.push({ 
                    name: 'kamar.index' 
                }) 
 
            }).catch(error => { 
                //assign state validation with error  
                validation.value = error.response.data 
            }) 
 
        } 
 
        //return 
        return { 
            kamar, 
            validation, 
            router, 
            store 
        } 
 
    } 
 
} 
</script> 
 
<style> 
    body{ 
        background: lightgray; 
    } 
</style>
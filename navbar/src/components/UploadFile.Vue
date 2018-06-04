<template>
<div class="container">
    <b-form-group id="fieldset1">
        <b-form-file v-model="file" :state="Boolean(file)" placeholder="Choose a file..." v-on:change="handleFileUpload()"></b-form-file>
        <div class="mt-3">Selected file: {{ file && file.name }}</div>
        <div><b-button variant="success" @click="submitFile()">Upload</b-button></div>
        <p>{{ msg }}</p>
     </b-form-group>
    </div>
</template>

<script>
import axios from 'axios'
export default {
  data () {
    return {
      file: null,
      msg: ''
    }
  },
  methods:{
    submitFile(){
        let formData = new FormData()
        formData.append('file',this.file)
        axios.post('http://192.168.0.124:3000/upload',
        formData,{
            headers: {
                'Content-Type': 'multipart/form-data'
            }
        }).then(function(){
            alert("SUCCESS!!")
            console.log('SUCCESS!!')
        }).catch(function(){
            console.log('FAILURE!!')
        })
    },
    handleFileUpload(){
        this.file = this.$refs.file.files[0]
    }
  }
}
</script>

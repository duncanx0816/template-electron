<template lang="pug">
div
    div.error-message
    section.add-new-link
        form.new-link-form
            input.new-link-url(type="url",size="60",placeholder="URL",@keyup="validURL",v-model="url",required)
            input.new-link-submit(type="submit",value="Submit",:disabled="!isValid" @click.prevent="submit")
    section.links
    section.controls
        button.clear-storage(disabled) Clear Storage
</template>

<script>
const axios = require('axios')
export default {
    data(){
        return {
            url:null,
            isValid:false
        }
    },
    mounted(){
        axios.get('http://www.baidu.com').then(res=>{
            console.log(res)
        })
    },
    methods:{
        validURL(){
            this.isValid= !this.url || this.url.slice(0,3)=='www' || this.url.slice(0,4)=='http'
        },
        submit(){
            console.log(this.url)
            const proxyurl = "https://cors-anywhere.herokuapp.com/"
            fetch(this.url,{headers:{'Access-Control-Allow-Origin': '*'}})  .then(res=>{
                console.log(res)
                console.log(res.text())
                // const parser=new DOMParser()
                // const nodes=parser.parseFromString(res.text(),"text/html")
                // const title=nodes.querySelector("title").innerText
                // console.log(title)
            })
        }
    }
}
</script>

<style lang="stylus">
.ceshi
    background-color:gray
</style>
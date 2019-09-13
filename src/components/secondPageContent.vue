<template>
    <div>
        <div id="backgrnd">
            <h1>Find all the weirdest image on our website...</h1>
            <div id="positionSearchBar">
                <div class="searchbar">
                    <input v-model="search" @keyup.enter="searchImage" type="text" placeholder="Looking for an image with specific tag? just type it here and hit enter...">
    
                </div>
                <div class="uploadfile" style="display: flex; justify-content: center;margin-top:3vh;">
                    <h4 >Upload your image here</h4>
                    <form action="" enctype="multipart/form-data">
                        <input type="text" v-model="imagetitle" placeholder="Image title">
                        <input
                            type="file"
                            ref="image"
                            accept="image/*"
                            v-on:change="handleimage"
                            required>
                        <button id="uploadbtn" @click.prevent="registerimage" type="submit">Upload</button>
                        <!-- <input v-on:change="registerimage" accept="image/png, image/jpeg" type="file" > -->
                    </form>
                </div>
                
            </div>
            <img  src="../img/room-GkWrEPTyDRs-unsplash.jpg" alt="orang depan komputer">
        </div>
        <div class="allimage">
            <div v-for="(image, index) in images" :key="index" class="image">
                <a @click.prevent="showbiggerimage(image.url, image.title, image._id)" href=""><img v-bind:src="image.url" alt=""></a>
            </div>
            
        </div>
        <a @click.prevent="closepoppingimage" v-if="showimage === true" href="" >
            <div id="cancelfront">

            </div>
        </a>
        <div v-if="showimage === true" id="poppingimage">
            <div class="closeButton grid-item">
                <a style="color: black;" @click.prevent="closepoppingimage" href=""><i class="far fa-times-circle fa-2x"></i></a>
            </div>
            <div class="wrapperpopping">
                <div class="image">
                    <img v-bind:src="url" alt="">
                </div>
                <div id="itemdescription">
                    <div style="display: flex; flex-direction: column; justify-content: center;">
                        <h1>{{title}}</h1>
                        <div>
                            <a href="" @click.prevent="likethis()">like this.</a>               
                        </div>
                        <div id="sharecolumn">
                            <a v-bind:href="link" data-action="share/whatsapp/share">Share via Whatsapp</a>
                        </div>
                       
                    </div>
                </div>
            </div>
             
        </div>
    </div>
</template>

<script>
export default {
    props: ['images'],
    data: function(){
        return {
            imagetitle: "",
            search: "",
            showimage: false,
            url: "",
            title: "",
            filepath: "",
            _id: null,
            image: null,
            link: "whatsapp://send?text="
        }
    },
    props:['images'],
    methods: {
    
        registerimage(){
            document.getElementById('uploadbtn').innerHTML = "Loading..."
            let formData = new FormData()
            formData.append('title', this.imagetitle)
            formData.append('image', this.image)
            this.$emit('registerimage', formData)
            this.imagetitle = ""
        },
        handleimage(){
   
            let reader = new FileReader()
            reader.readAsDataURL(this.$refs.image.files[0])
            this.image = this.$refs.image.files[0]
        },
        likethis(){
            this.showimage = false;
            this.$emit('likethis', this._id)
        },
        showbiggerimage(url, title, _id){
            this.url = url
            this.title = title
            this._id = _id
            this.link += url
            this.showimage = true
        },
        closepoppingimage(){
            this.link = "whatsapp://send?text="
            this.showimage = false
        },
        searchImage(){
            this.$emit('searchimage', this.search)
        }
    }
}
</script>

<style scoped>
    #itemdescription a{
        text-decoration: none;
        font-family: 'Roboto', sans-serif;
        color: black
    }
    #itemdescription a:hover {
        border-bottom: 1px solid black;
    }
    #sharecolumn {
        display: flex;
        justify-content: space-evenly;
    }
    #itemdescription {
        display: flex;
        justify-content: center;
    }
    #cancelfront {
        background: black;
        position: fixed;
        z-index: 2;
        top: 0;
        left: 0px;
        height: 100%;
        opacity: 0.3;
        width: 100vw;
    }

    .closeButton{
        position: relative;
        top: 5px;
        left: 5px;
    }
    #poppingimage{
        position: fixed;
        z-index: 4;
        font-family: 'Roboto', sans-serif; 
        top: 15%;
        left: 26%;
        width: 50vw;
        height: 70vh;
        border-radius: 10px;
        background-color: white;
        box-shadow: 5px 5px 10px grey;
    }
    #poppingimage .image{
        height: 40vh;
        display: flex;
        justify-content: center;
    }
    #poppingimage img {
        height: 100%;
        object-fit: scale-down;
    }
    #backgrnd img{
        width: 100vw;
        position: absolute;
        z-index: -1;
    }
    #backgrnd{
        position: relative;
        height: 60vh;
        overflow: hidden;
    }
    #backgrnd h1{
        font-family: 'Roboto', sans-serif; 
        position: absolute;
        z-index: 0;
        left: 5%;
        top: 5%;
        color: white;
        text-shadow: 5px 5px 5px black
    }
    .uploadfile{
   
        color:white; 
        font-family: 'Roboto', sans-serif;
        
        text-shadow: 5px 5px 5px black
    }
    .uploadfile h4{
        margin-right: 1vw;
        margin-top: 0px; 
        margin-bottom: 0px; 
    }
    #positionSearchBar{
        left: 25%;
        top: 40%;
        position: absolute;
        z-index: 0;
    }
    input:focus{
        border-radius: 15px;
        border: 2px solid grey;
    }
    .allimage{
        display: grid;
        grid-template-columns:  1fr 1fr 1fr ;
        margin-top: 10%;
        margin-left: 5%;
        margin-right: 5%;
        grid-gap: 1rem;
        align-items: start;
        justify-items: center;
    }
    .allimage .image img{
        border-radius: 5px;
        box-shadow: 5px 5px 10px grey;
        width: 100%
    }
    .allimage .image{
        object-fit: contain
    }
    
    .searchbar input{
        font-family: 'Roboto', sans-serif; 
        height: 5vh;
        outline: 0px; 
        width: 50vw;
        border-radius: 15px;
        padding-left: 3%;
        padding-right: 3%;
        font-size: 1rem;
        border: 0px;
        background-color: #F5F5F5
    }
    
    
</style>
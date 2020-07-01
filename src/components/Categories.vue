<template>
    <div class="categories-wrapper">
        <ul>
            <li @click="showCategory(item.id)" class="category-list" v-for="(item, id) in categoryList" :key="id"> {{ item.name | captalize }} </li>
        </ul>        
    </div>
</template>

<script>
import axios from 'axios'

export default {

    name: "Categories",
    data() {
        return {
            // isHover: false,
            urlNoCategory: "https://newsapi.org/v2/sources?country=in&apiKey=e11cc1ccc525413bb847716b1f210c33",
            categories: [],
            category: '',
            categoryList: [ 
                {
                    "id": 0,
                    "name": "all"
                },
                {
                    "id": 1,
                    "name": "business"
                },
                {
                    "id": 2,
                    "name": "general"
                },
                {
                    "id": 3,
                    "name": "health"
                },
                {
                    "id": 4,
                    "name": "science"
                },
                {
                    "id": 5,
                    "name": "sports"
                },
                {
                    "id": 6,
                    "name": "technology"
                }
            ]
        }
    },
    methods: {

        async getCategoriesNews() {
            let config = {
                headers: {
                    'Accept': 'application/json'
                }
            }

            if(this.category === 'all'){
                try {
                    const categories = await axios.get(this.urlNoCategory, config)
                    console.log(categories.data.sources)   

                } catch (err) {
                    console.log(err)
                }
            }
            else{
                let urlCategory= "https://newsapi.org/v2/sources?country=in&category="+ this.category +"&apiKey=e11cc1ccc525413bb847716b1f210c33"
                try {
                    const categories = await axios.get(urlCategory, config)
                    console.log(categories.data.sources)   
                } catch (err) {
                    console.log(err)
                }
            }

            
        },

        showCategory(id){
            
            if(id === 0){
                this.category = 'all'
                return this.getCategoriesNews()
            }

            else {
                this.categoryList.forEach(el => {
                    if (el.id == id) {
                        this.category = el.name
                        // console.log(this.category)
                        // console.log(this.urlCategory)
                        this.getCategoriesNews()
                    }
                });
            }
        }

    },
    mounted(){
        this.getCategoriesNews()
    },

    filters: {
        captalize(value){
            if(!value){
                return ''
            }
            return value[0].toUpperCase()+value.slice(1)
            
        }
    }
    
}
</script>

<style scoped>

    .categories-wrapper{
        min-height: 50px;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    ul{
        padding: 0;
    }

    .category-list{
        cursor: pointer;
        list-style: none;
        display: inline-flex;
        border-radius: 5px;
        color: #fff;
        padding: 3px 15px;
    }

    .category-list:nth-child(1){
        margin-right: 30px;
        background: crimson;
    }

    .category-list:nth-child(2){
        margin-right: 30px;
        background: #eb790e;
    }

    .category-list:nth-child(3){
        margin-right: 30px;
        background: #080bb4;
    }

    .category-list:nth-child(4){
        margin-right: 30px;
        background: #71b800;
    }

    .category-list:nth-child(5){
        margin-right: 30px;
        background: #a70a92;
    }

    .category-list:nth-child(6){
        margin-right: 30px;
        background: #088b04;
    }

    .category-list:nth-child(7){
        background: #f04f05;
    }

    /* .category-list:hover{
        
    } */

    .categories-wrapper ul a:hover{
        box-shadow: 0, 0, 12, rgba(0, 0, 0, 0.7);
    }

</style>
<script>
import articles from '../db/articles.json';

export default {
    data() {
        return {
            singleArticle: {}
        }
    },
    methods: {
        getSingleArticle() {
            const articleId = this.$route.params.id;

            //ciclo sull'array di articoli per trovare quello che corrisponde all'id passato
            for (let i = 0; i < articles.length; i++) {
                let article = articles[i];

                if (article.id == articleId) {
                    this.singleArticle = article;
                    break;
                }
            }
        },
        getImagePath(img) {
            return new URL(`../assets/${img}`, import.meta.url).href;
        }
    },
    mounted() {
        this.getSingleArticle();
    }
}

</script>

<template>
    <div class="container-fluid ms-2 mt-4 pe-5">
        <div class="d-flex justify-content-end mb-3">
            <router-link :to="{ name: 'articles' }" class="btn btn-outline-warning rounded-pill">
                <i class="fa-solid fa-arrow-left" style="margin-right: 8px;"></i> Torna indietro
            </router-link>
        </div>
        <h2>{{ singleArticle.title }}</h2>
        <p>{{ singleArticle.description }}</p>
        <div class="w-50 my-container-img">
            <img :src="getImagePath(singleArticle.img)" class="img-fluid" alt="cover-article">
        </div>
        <div v-for="point in singleArticle.article_points" class="mt-4">

            <div v-if="Array.isArray(point.body)">
                <h4 class="text-info-emphasis">
                    <span class="d-inline-block me-3">{{ point.id }}.</span>
                    <span>{{ point.title }}</span>
                </h4>
                <div v-for="subcap in point.body">
                    <i class="fa-regular fa-circle fa-2xs text-danger-emphasis"></i>
                    <h5 class="d-inline-block ms-2 mb-1">{{ subcap.titolo }}</h5>
                    <p class="desc">{{ subcap.desc }}</p>
                </div>
            </div>

            <div v-else>
                <h4 class="text-info-emphasis">
                    <span class="d-inline-block me-3">{{ point.id }}.</span>
                    <span>{{ point.title }}</span>
                </h4>
                <p>
                    {{ point.body }}
                </p>
            </div>

        </div>
        <div class="mt-5">
            <h4>Conclusioni</h4>
            <p>{{ singleArticle.conclusione }}</p>
        </div>
    </div>
</template>

<style scoped>
.my-container-img {
    margin-bottom: 45px;
}

.desc {
    margin-left: calc(10px + 0.5rem);
}
</style>
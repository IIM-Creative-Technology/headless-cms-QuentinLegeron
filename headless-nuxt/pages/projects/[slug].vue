<template>
    <div v-if="project" class="project-details">
        <nuxt-link to="/" class="retour">Retour</nuxt-link>
        <h1>{{project.title}}</h1>
        <div class="project-type">{{ project.type }}</div>
        <div class="project-description">{{ project.description }}</div>
        <img class="project-img" :src='`${project.img.url}`' :alt="`${ project.img.name }`">
        <div v-if="project.technologies.lenght > 0">
            <span>Technologies :</span>
            <ul class="technology-list">
                <li v-for="technology in project.technologies" :key="technology.id" class="technology-item">
                    {{ technology.name }}
                    <img :src='`${technology.image.url}`' :alt="`${ technology.image.name }`">
                </li>
            </ul>
        </div>
        <a :href="project.link" class="project-link" target="_blank">Lien du projet</a>
    </div>
</template>

<script setup>

const { findOne } = useStrapi()
const route = useRoute()
const project = ref()

onMounted(async () => {
    project.value = await findOne(`projects?filters[slug]=${route.params.slug}&populate=deep`)
    project.value = project.value.data[0]
})

</script>

<style scoped>
    .retour {
        color: #0077cc;
        text-decoration: none;
        text-align: left;
        font-size: 16px;
        margin-bottom: 20px;
    }

    .project-details {
        display: flex;
        flex-direction: column;
        align-items: center;
        text-align: center;
        padding: 20px;
        background-color: #f5f5f5;
        border-radius: 10px;
        box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.3);
    }

    .project-details .retour {
        align-self: flex-start;
        margin: 0;
    }

    .project-details h1 {
        font-size: 30px;
        margin-bottom: 20px;
    }

    .project-type {
        font-size: 20px;
        margin-bottom: 10px;
    }

    .project-description {
        font-size: 16px;
        margin-bottom: 20px;
    }

    .project-img {
        width: 100%;
        max-width: 550px;
        margin-bottom: 20px;
        border-radius: 10px;
        box-shadow: 0px 2px 6px rgba(0, 0, 0, 0.3);
    }

    .technology-list {
        list-style: none;
        margin: 0;
        padding: 0;
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        margin-bottom: 20px;
    }

    .technology-item {
        margin: 10px;
        display: flex;
        align-items: center;
        font-size: 14px;
    }

    .technology-item img {
        width: 30px;
        margin-left: 5px;
    }

    .project-link {
        font-size: 16px;
        color: #0077cc;
        text-decoration: none;
    }

    .project-link:hover {
        text-decoration: underline;
    }
</style>
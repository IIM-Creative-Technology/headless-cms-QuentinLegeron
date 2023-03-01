<template>
    <div v-if="project">
        <nuxt-link to="/">
            Retour
        </nuxt-link>
        <br>
        titre : {{project.title}}
        <br>
        type : {{ project.type }}
        <br>
        <div>
            description : {{ project.description }}
        </div>
        <br>
        <img style="width: 100px;" :src='`${project.img.url}`' :alt="`${ project.img.name }`">
        <br>
        <span>Technologies :</span>
        <ul>
            <li v-for="technology in project.technologies" :key="technology.id">
                {{ technology.name }}
                <img style="width: 50px;" :src='`${technology.image.url}`' :alt="`${ technology.image.name }`">
            </li>
        </ul>
        <br>
        <nuxt-link :to="project.link" target="_blank">Lien du projet</nuxt-link>
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

<style scoped></style>
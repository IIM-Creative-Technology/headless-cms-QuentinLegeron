<template>
    <div v-if="projects">
        <h1>Quentin Legeron</h1>
        <div class="description">
            <p>Je suis un développeur web junior, passionné par le développement web et la gestion de projet.</p>
            <p>Je suis actuellement en formation de chef de projet digital à l'IIM (Institut de l'Internet et du Multimedia).</p>
            <p>Je suis en alternance chez <a href="https://vpwhite.com/" target="_blank">VP&White</a> en tant que développeur web fullstack et PO (Product Owner).</p>
        </div>
        <div v-if="types" class="filter">
            <button @click="filterProjects('all')">Tous les projets</button>
            <button v-for="projectType in types" :key="projectType" @click="filterProjects(projectType)">
                {{ projectType }}
            </button>
        </div>
        <ul>
            <nuxt-link :to="`/projects/${project.slug}`" v-for="project in filteredProjects" :key="project.id">
                <li>
                    <img class="project-img" :src='`${project.img.url}`' :alt="`${ project.img.name }`">
                    {{ project.title }}
                </li>
            </nuxt-link>
        </ul>
    </div>
</template>

<script setup>

    const { find } = useStrapi()
    const projects = ref()
    const types = ref([])
    const activeFilter = ref('all')

    const filterProjects = (type) => {
        activeFilter.value = type
    }

    const filteredProjects = computed(() => {
        if (activeFilter.value === 'all') {
            return projects.value.data
        } else {
            return projects.value.data.filter(project => project.type === activeFilter.value)
        }
    })

    onMounted(async () => {
        projects.value = await find('projects', { populate: 'deep'})
        types.value = new Set(projects.value.data.map(project => project.type))
    })

</script>

<style scoped>
    h1 {
        font-size: 32px;
        font-weight: bold;
        text-align: center;
        margin-bottom: 30px;
    }

    .description {
        margin-bottom: 30px;
        display: flex;
        flex-direction: column;
    }

    .filter {
        display: flex;
        align-items: center;
        justify-content: center;
        margin-bottom: 30px;
    }

    button {
        padding: 10px 20px;
        margin-right: 10px;
        font-size: 16px;
        font-weight: bold;
        border-radius: 5px;
        border: none;
        color: white;
        background-color: #0077cc;
        cursor: pointer;
        transition: background-color 0.3s ease;
    }

    button:hover {
        background-color: #005fa3;
    }

    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }

    li {
        font-size: 20px;
        margin-bottom: 10px;
        padding: 10px;
        background-color: white;
        border-radius: 5px;
        box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.1);
        transition: box-shadow 0.3s ease;
        cursor: pointer;
        text-align: center;
    }

    li .project-img {
        width: 100%;
        height: 200px;
        object-fit: cover;
        margin-bottom: 10px;
    }

    li:hover {
        box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.2);
    }

    a {
        text-decoration: none;
        color: #333;
    }
</style>
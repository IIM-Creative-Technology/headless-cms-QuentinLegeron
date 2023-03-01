<template>
    <div v-if="projects">
        <h1>Hello word</h1>
        <div v-if="types">
            <button @click="filterProjects('all')">Tous les projets</button>
            <button v-for="projectType in types" :key="projectType" @click="filterProjects(projectType)">
                {{ projectType }}
            </button>
        </div>
        <ul>
            <nuxt-link :to="`/projects/${project.slug}`" v-for="project in filteredProjects" :key="project.id">
                <li>
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

</style>
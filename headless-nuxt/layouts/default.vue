<template>
    <main role="main">
        <nav v-if="projects">
            <nuxt-link to="/">Home</nuxt-link>
            <!-- <nuxt-link :to="`/projects/${project.slug}`" v-for="project in projects.data" :key="project.id">
                    {{ project.title }}
            </nuxt-link> -->
        </nav>
        <slot/>
    </main>
</template>

<script setup>

    // const { find } = useStrapi()
    // const projects = ref()

    // onMounted(async () => {
    //     projects.value = await find('projects', { populate: 'deep'})
    // })

</script>
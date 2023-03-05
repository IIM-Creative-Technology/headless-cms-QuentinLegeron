<template>
    <main role="main">
        <slot/>
    </main>
</template>

<style scoped>

    main {
        max-width: 800px;
        margin: 0 auto;
        padding: 20px;
        font-family: Arial, sans-serif;
        background-color: #f5f5f5;
    }

    nav {
        display: flex;
        margin-bottom: 20px;
    }

    nav a {
        color: #0077cc;
        text-decoration: none;
        font-size: 16px;
        margin-left: 20px;
    }

    nav a:hover {
        text-decoration: underline;
    }
</style>
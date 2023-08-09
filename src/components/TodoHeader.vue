<script setup lang="ts">
</script>

<template>
    <header>
        <nav class="container">
            <div class="branding">
                <img src="./../assets/vue-ts.png" alt="logo" />
                <h1><slot name="app-name"></slot></h1>
            </div>
            <ul class="nav-routes">
                <RouterLink to="/">Home</RouterLink>
                <RouterLink to="/about">About</RouterLink>
            </ul>
        </nav>
    </header>
</template>

<style lang="scss" scoped>
nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background: #f4f4f4;

    .branding {
        display: flex;
        align-items: center;

        img {
            width: 100%;
            max-width: 120px;
        }

        h1 {
            margin-left: 1rem;
            line-height: 1;
        }
    }

    .nav-routes {
        list-style: none;

        a {
            text-decoration: none;
            color: black;
            margin-left: 1rem;
        }
    }
}
</style>
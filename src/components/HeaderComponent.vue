<script setup>
import logo from "@assets/logo.png";
import NavComponent from "@components/NavComponent.vue";



</script>

<template>
    <header>
        <div id="logo">
            <img :src="logo" alt="no" />
        </div>

        
        <NavComponent/>
    </header>
</template>

<style scoped>
header {
    padding: 1rem 1rem 2rem;
    display: flex;
    flex-direction:row;
    justify-content: space-between;
}




#logo img {
    height: 30px;
    width: auto;
    margin: 10px;
}

</style>


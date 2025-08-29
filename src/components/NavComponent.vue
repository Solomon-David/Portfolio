<script setup>
    import {ref} from "vue";

    const mobile = ref(visualViewport.width < 500);
    
    

    let open = ref(false);

    const toggleMenu = () => {
        open.value = !open.value;
    }

</script>

<template>
    <div id="navcomponent">            
        <div id="menu" v-if="mobile">
            <button @click="toggleMenu">
              <span v-if="!open"><img src="@assets/menu.svg" alt="hamburger menu to open navigation bar"/> </span>
              <span v-if="open"><img src="@assets/Close.svg" alt="X shaped button to close navigation bar"/></span>
            </button>
        </div>

        <Transition name="slide">
        <nav v-show="open || !mobile">
            <a href="#hero">Home</a>
            <a href="#">About</a>
            <a href="#">Skills</a>
            <a href="#">Projects</a>
            <a href="#">Experience</a>
            <a href="#">Contact</a>
        </nav>
        </Transition>
    </div>

</template>

<style scoped>
    #navcomponent {
        display: flex;
        flex-direction: column;
        align-items: end;
        flex-basis: 40vw;
        flex-grow: 5;
        flex-shring: 1;
    }

    #menu button {
        background:none;
        border:none;
        cursor:pointer;
        padding:0.1rem;
    }

    #menu button img{
        width: 2rem;
        aspect-ratio: 1/1;
    }

    nav {
        display: flex;
        flex-direction: column;
        gap: 1.5rem;
        align-items: right;
        
    }

    nav a {
        text-align: right;
        text-decoration: none;
        line-height: 1rem;
        font-weight: var(--semibold);
    }

    nav a:hover {
        text-decoration: underline;
        text-decoration-thickness: 3px;
        text-underline-offset: 10px;
        text-decoration-color: var(--color);
    }
 

    .slide-enter-from, .slide-leave-to {
        transform-origin: top;
        transform: scaleY(0%);
        opacity: 0;
    }

    .slide-leave-from, .slide-enter-to {
        transform-origin: top;
        opacity: 1;
        transform: scaleY(100%);
    }

    .slide-enter-active, .slide-leave-active {
        transition: all 0.3s ease;
    }

@media (min-width: 500px) {
    #navcomponent {
        flex-direction: row;
        align-items: center;
        justify-content: center;
        align-self: center;
    }

    nav{
        flex-direction: row;
        gap: 2rem;
        align-items: center;
    }
}
</style>
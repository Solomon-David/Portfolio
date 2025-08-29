<script setup>
    import { ref, onMounted, Transition } from 'vue';
    const props = defineProps({
        options: {
            type: Array,
            required: true,
        },
        fixed: {
            type:String,
        }
    });

        
        const option = ref(props.options[0]);
        const index = ref(0);
        setInterval(() => {
            index.value = (index.value + 1) % props.options.length;
            option.value = props.options[index.value];
        }, 2000);

</script>

<template>
    <div class="changing-text">
        <h1>
            <Transition name="change" >
                <span :key="option" >{{ option }}</span> 
                
            </Transition>
            <br>
            {{ fixed }}
        </h1>
    </div>
</template>

<style >
        .change-enter-from, .change-leave-to{
            opacity: 0;
        }

        .change-enter-to, .change-leave-from{
            opacity: 1;
        }

        .change-enter-active, .change-leave-active{
            transition: opacity 0.3s ease;
            position:absolute;
        }

        h1{
            font-size: 48px;
            font-weight: 700;
            line-height: 1;
        }

        h1 span {
            text-transform: capitalize;
            color: var(--accent);
        }
</style>


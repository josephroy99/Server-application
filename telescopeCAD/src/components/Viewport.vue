<template>
    <svg class="viewport">
        <Element v-for="element in elements" :ElementProperties="element"/>
    </svg>
</template>

<script>
    import Element from './Element.vue';

    export default {
        name: 'Viewport',
        props: {
            elements: {
                type: Array
            }
        },
        components: {
            Element
        },
    }
</script>

<style scoped>
    .viewport {
        height: 100%;
        width: 100%;
    }
</style>
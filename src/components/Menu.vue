<template>
    <div class="menu">
        <button @click="reiniciar"> Reiniciar </button>
    </div>
</template>

<script>
export default {
    name: 'Menu',
    methods: {
        reiniciar() {
            this.$emit('reiniciar')
        }
    }
}
</script>

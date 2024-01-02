<!-- src/components/AppHeader.vue -->
<template>
    <div class="app-header">
        <h1>메모 애플리케이션</h1>
    </div>
</template>

<script>
export default {
    name: 'AppHeader'
};
</script>

<style lang="scss" scope>
    .app-header {
        overflow: hidden;
        padding: rem(50) 0 rem(25);
        h1 {
            float: left;
            font-size: rem(24);
            text-align: center;
        }
    }
</style>

<template>
    <div id="app">
        <app-header/>
        <memo-manage/>
    </div>
</template>

<script>
import AppHeader from './components/AppHeader';
import MemoManage from './components/MemoManage';

export default {
    name: 'app',
    components: {
        AppHeader,
        MemoManage
    }
};
</script>

<style lang="scss">
    #app {
        width: rem(560);
        margin: 0 auto;
    }
</style>

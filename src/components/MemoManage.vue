<template>
    <div class="memo-app">
        <memo-form @addMemo="addMemo"/>
        <ul class="memo-list">
            <memo-state v-for="memo in memos" :key="memo.id" :memo="memo" @deleteMemo="deleteMemo" @updateMemo="updateMemo"/>
        </ul>
    </div>
</template>

<script>
import MemoForm from './MemoForm';
import MemoState from './MemoState';

export default {
    name: 'MemoManage',
    components: {
        MemoForm,
        MemoState
    },
    data () {
        return {
            memos: []
        };
    },
    created () {
        this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
    },
    methods: {
        addMemo (payload) {
            this.memos.push(payload);
            this.storeMemo();
        },
        storeMemo () {
            const memosToString = JSON.stringify(this.memos);
            localStorage.setItem('memos', memosToString);
        },
        deleteMemo (id) {
            const targetIndex = this.memos.findIndex(v => v.id === id);
            this.memos.splice(targetIndex, 1);

            this.storeMemo();
        },
        updateMemo (payload) {
            const { id, content } = payload;
            const targetIndex = this.memos.findIndex(v => v.id === id);
            const targetMemo = this.memos[targetIndex];
            this.memos.splice(targetIndex, 1, { ...targetMemo, content });
            this.storeMemo();
        }
    }
};
</script>

<style lang="scss" scoped>
.memo-app {
    .memo-list {
        padding: rem(20) 0;
        margin: 0;
    }
}
</style>

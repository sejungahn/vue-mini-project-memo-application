<template>
    <div class="memo-app">
        <memo-form @addMemo="addMemo"/>
        <ul class="memo-list">
            <memo-state v-for="memo in memos" :key="memo.id" :memo="memo" @deleteMemo="deleteMemo" @updateMemo="updateMemo"/>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';
import MemoForm from './MemoForm';
import MemoState from './MemoState';

const memoAPICore = axios.create({
    baseURL: 'http://localhost:8000/api/memos'
});

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
        // this.memos = localStorage.memos ? JSON.parse(localStorage.memos) : [];
        memoAPICore.get('/')
            .then(res => {
                this.memos = res.data;
            });
    },
    methods: {
        addMemo (payload) {
            memoAPICore.post('/', payload)
                .then(res => {
                    this.memos.push(res.data);
                });
            // this.memos.push(payload);
            // this.storeMemo();
        },
        // storeMemo () {
        //     const memosToString = JSON.stringify(this.memos);
        //     localStorage.setItem('memos', memosToString);
        // },
        deleteMemo (id) {
            const targetIndex = this.memos.findIndex(v => v.id === id);
            // 삭제 대상과 일치하는 id 값을 delete 메소드와 함께 요청
            memoAPICore.delete(`/${id}`)
                .then(() => {
                    // 요청 후 MemoManagement 컴포넌트의 memos 데이터에서 삭제
                    this.memos.splice(targetIndex, 1);
                });
            // this.memos.splice(targetIndex, 1);
            // this.storeMemo();
        },
        updateMemo (payload) {
            const { id, content } = payload;
            const targetIndex = this.memos.findIndex(v => v.id === id);
            const targetMemo = this.memos[targetIndex];
            memoAPICore.put(`/${id}`, { content })
                .then(() => {
                    this.memos.splice(targetIndex, 1, { ...targetMemo, content });
                });
            // this.memos.splice(targetIndex, 1, { ...targetMemo, content });
            // this.storeMemo();
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

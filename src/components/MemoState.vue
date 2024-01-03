<template>
    <li class="memo-item">
        <strong>{{ memo.title }}</strong>
        <p @dblclick="handleDblClick">
            <span v-if="!isEditing">
                {{ memo.content }}
            </span>
            <input v-else type="text" ref="content" :value="memo.content" @blur="handleBlur" @keydown.enter="updateMemo"/>
        </p>
        <button type="button" @click="deleteMemo">
            <i class="fas fa-times"></i>
        </button>
    </li>
</template>
<script>
export default {
    name: 'MemoState',
    props: {
        memo: {
            type: Object
        }
    },
    beforeUpdate () {
        console.log('beforeUpdate =>', this.$refs.content);
    },
    updated () {
        console.log('updated =>', this.$refs.content);
    },
    data () {
        return {
            isEditing: false
        };
    },
    methods: {
        deleteMemo () {
            const id = this.memo.id;
            this.$emit('deleteMemo', id);
        },
        handleDblClick () {
            this.isEditing = true;
            console.log('handleDblClick =>', this.$refs.content);
            this.$nextTick(() => {
                this.$refs.content.focus();
            });
        },
        updateMemo (e) {
            const id = this.memo.id;
            const content = e.target.value.trim();
            if (content.length <= 0) {
                return false;
            }
            this.$emit('updateMemo', { id, content });
            this.isEditing = false;
        },
        handleBlur () {
            this.isEditing = false;
        }
    }

};
</script>
<style lang="scss" scoped>
.memo-item {
    overflow: hidden;
    position: relative;
    margin-bottom: rem(20);
    padding: rem(25);
    box-shadow: 0 4px 10px -4px rgba(0,0,0,.2);
    background-color: $white;
    button {
        position: absolute;
        right: 20px;
        top: 20px;
        background: none;
        font-size: rem(20);
        color: #e5e5e5;
        cursor: pointer;
    }
    strong {
        display: block;
        margin-bottom: rem(15);
        font: {
            size: rem(18);
            weight: normal;
        }
        word-break: break-all;
    }
    p {
        font-size: rem(14);
        line-height: rem(24);
        color: #666;
        input[type="text"] {
            width: 100%;
            font-size: inherit;
            border: 1px solid #999;
            box-sizing: border-box;
        }
    }
}
</style>

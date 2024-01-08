<template>
    <div class="memo-form">
        <form @submit.prevent="addMemo">
            <fieldset>
                <div>
                    <input class="memo-form__title-form" type="text" v-model="title" placeholder="메모의 제목을 입력해주세요." />
                    <textarea class="memo-form__content-form" v-model="content" placeholder="메모의 내용을 입력해주세요." />
                    <button type="reset"><i class="fas fa-sync-alt"></i></button>
                </div>
                <button type="submit">등록하기</button>
            </fieldset>
        </form>
    </div>
</template>
<script>
export default {
    name: 'MemoForm',
    data () {
        return {
            title: '',
            content: ''
        };
    },
    methods: {
        resetFields () {
            this.title = '';
            this.content = '';
        },
        addMemo () {
            const { title, content } = this; // 비구조화 할당
            // const id = new Date().getTime();

            const isEmpty = title.length <= 0 || content.length <= 0;
            if (isEmpty) {
                return false;
            }

            // this.$emit('addMemo', { id, title, content });
            this.resetFields();
        }
    }
};
</script>
<style lang="scss" scoped>
.memo-form {
    margin-bottom: rem(25);
    padding-bottom: rem(40);
    border-bottom: 1px solid $grey;
    form {
        fieldset {
            &::after {
                content: '';
                display: block;
                clear: both;
            }
            div {
                position: relative;
                padding: rem(25);
                margin-bottom: rem(20);
                box-shadow: 0 4px 10px -4px rgba(0,0,0,.2);
                background-color: $white;
                button[type="reset"] {
                    position: absolute;
                    right: 20px;
                    bottom: 20px;
                    font-size: rem(16);
                    background: none;
                    cursor: pointer;
                }
            }
            button[type="submit"] {
                float: right;
                width: rem(100);
                padding: rem(15) 0;
                border-radius: 4px;
                background-color: #ff5a00;
                color: $white;
                font-size: rem(16);
                cursor: pointer;
            }
        }
    }
    &__title-form {
        width: 100%;
        margin-bottom: rem(15);
        font-size: rem(18);
        line-height: rem(26);
        &:focus {
            outline: none;
        }
    }
    &__content-form {
        width: 100%;
        height: 65px;
        font-size: rem(14);
        line-height: rem(22);
        vertical-align: top;
    }
}
</style>

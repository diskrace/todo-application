<template>
    <div>
        <!-- 아래 버튼 클릭하면 데이터 모두 삭제하도록 구현해 보시오 -->
        <button v-on:click="clearAllItems">clear all</button>
    </div>
</template>

<script>
export default {
    methods: {
        clearAllItems: function() {
            this.$emit("clearall");
        }
    }

}
</script>

<style>

</style>

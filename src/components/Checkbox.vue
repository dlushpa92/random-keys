<template>
    <div class="checkbox">
        <label for="">{{ labelName }}</label>
        <input type="checkbox">
    </div>
</template>

<script>
    export default {
        props: {
            labelName: String,
            condition: Boolean

        }
    }
</script>

<style lang="scss" scoped>

</style>
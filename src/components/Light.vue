<template>
    <div :class="color"></div>
</template>

<script>
export default {
    props: ['color']
}
</script>

<style>
.green, .red, .yellow{
    width: inherit;
    height: inherit;
    border-radius: inherit;
}
.green{
    background-color: green;
}
.red{
    background-color: red;
}
.yellow{
    background-color: yellow;
}
</style>
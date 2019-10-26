<template>
    <nb-container>
        <nb-content class="body-container">
            <text>Settings Screen</text>
        </nb-content>
    </nb-container>
</template>

<script>
export default {
    props: {
        navigation: {
            type: Object
        },
  },
}
</script>

<style>
    .body-container{
        padding: 10px;
    }
</style>

<template>
    <div class="heroImage"></div>
</template>

<script>
export default {
  name: 'HeroImage',
};
</script>

<style lang="scss" scoped>
    .heroImage{
        background-image: url('../images/back.jpg');
    position: fixed;
    top: 0;
    z-index: -1;
    width: 100%;
    height: 100%;
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 20% 0%;
    }

    .heroImage::after{
        content: '';
        position: absolute;
        top: 0;
        left: 0;
        z-index: 1;
        width: 100%;
        height: 100vh;
        background-color: rgba(0,0,0,.3);
    }
</style>

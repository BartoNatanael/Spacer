<template>
    <div class="claimWrapper">
        <h1 class='claim'>SPACER</h1>
        <p class="subclaim">
            Begin your journey throught our amazing galaxy,
            and discover places you never heard about of.
        </p>
        <p class="subclaim">
            Type anything space-related to start.
        </p>
    </div>
</template>

<script>
export default {
  name: 'Claim',
};
</script>

<style lang="scss" scoped>
    .claimWrapper{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
    }
    .claim{
        font-size: 50px;
        margin: 0;
        -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
        @media(min-width: 768px){
            font-size: 80px;
        }
        @media(min-width: 1024px){
            font-size: 100px;
            padding: 0 20%;
        }
    }

    .subclaim{
        font-size: 23px;
        margin: 15px 0 0 0;
        @media(min-width: 768px){
            width: 500px;
        }
    }
</style>

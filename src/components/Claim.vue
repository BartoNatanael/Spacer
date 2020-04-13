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
        align-items: center
    }
    .claim{
        font-size: 50px;
        margin: 0;
    }
    .subclaim{
        font-size: 23px;
        margin: 15px 0 0 0;
    }
</style>

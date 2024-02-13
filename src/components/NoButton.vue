<script setup>
    const props = defineProps({
        racoonSpeech: null
    });
</script>


<template>
    <div class="no-container">
        <button class="negative"><slot /></button>
        <div class="image-container" v-if="racoonSpeech !== null">
            <img src="/racoon.jpg"/>
            <span>{{racoonSpeech}}</span>
        </div>
    </div>
</template>


<style scoped>
    .no-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        transition: all 0.5s ease-in-out;
    }

    button {
        padding: 20px;
        border: none;
        border-radius: 20px;
        font-size: 20px;
        transition: all 0.25s ease-in-out;
        z-index: 2;
        align-self: stretch;
        flex: 1;
    }
    .negative {
        background: #FA0026;
    }
    button:hover {
        background: black;
        color: white;
        cursor: pointer;
    }

    .image-container {
        display: relative;
        margin: -40px 0;
    }

    img {
        height: 150px;
        border-radius: 20px;
    }
    span {
        position: absolute;
        top: 65px;
        right: 150px;
        left: -300px;
        background: #f9f9f9;
        padding: 10px;
        border-radius: 20px;
        border: 1px solid black;
        box-shadow: rgba(0,0,0,0.5) 5px 5px 5px;
        text-align: center;
    }

    @media (max-width: 742px) {
        span {
            top: 150px;
            left: -75px;
            right: -75px;
        }
    }
</style>
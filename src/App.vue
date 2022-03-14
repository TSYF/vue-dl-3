<template>
    <div
        class="character-card"
        v-for="(character, index) in charArr"
        :key="index"
    >
        <div class="character-card__container">
            <img class="character-card__img" :src="character.image" alt="" />
            <strong class="character-card__text"> {{ character.name }} </strong>
        </div>
    </div>
</template>

<script>
export default {
    data() {
        return {
            backgroundImg: `https://rickandmortypod.com/wp-content/uploads/2018/11/cropped-RM_page-header_background1-3.png`,
            charArr: undefined,
        };
    },
    methods: {
        async create() {
            try {
                const res = await fetch(
                    `https://rickandmortyapi.com/api/character`
                );
                const json = await res.json();

                if (!res.ok) return this.catch("Fuck");

                this.charArr = json.results;
            } catch (err) {
                console.error(err);
            }
        },
    },
    mounted() {
        window.addEventListener("DOMContentLoaded", (e) => {
            this.create();
            document.body.style.background = `no-repeat url(${this.backgroundImg})`;
            document.body.style.backgroundSize = "cover";
        });
    },
};
</script>

<style lang="scss" scoped>
// $backgroundImg: 'https://rickandmortypod.com/wp-content/uploads/2018/11/cropped-RM_page-header_background1-3.png';
//
// .body {
// background: no-repeat url($backgroundImg);
// background-size: cover;
// }

.character-card {


    & + & {
        margin-top: 1rem;
    }

    &__container {
        border: solid green 1px;
		display: flex;
		align-items: center;
		width: fit-content;
		padding: .5em 3em 1em .5em;
		border-radius: 1em;
    }

    &__img {
        max-height: 8em;
        border: solid green 2px;
        border-radius: 50%;
        margin-right: 1rem;
    }

    &__text {
        color: green;
    }
}
</style>

<script>
import LangFlag from 'vue-lang-code-flags';

export default {
    methods: {
        ConvertVote(vote) {
            const convertedVote = Math.ceil((vote / 10) * 5);
            return convertedVote;
        },
    },

    components: {
        LangFlag,
    },

    props: {
        DataMovies: Object,
    },
};
</script>

<template>
    <div class="card_movies">
        <img v-if="DataMovies.poster_path" :src="`http://image.tmdb.org/t/p/w342${DataMovies.poster_path}`"
            :alt="DataMovies.poster_path">
        <img v-else src="../assets/img/fallback-image.png" alt="">
        <div class="text">
            <div class="title">
                <span>TITOLO: </span>
                {{ DataMovies.title }}
            </div>
            <div class="original_title" v-show="DataMovies.original_title !== DataMovies.title">
                <span>TITOLO ORIGINALE: </span>
                {{ DataMovies.original_title }}
            </div>
            <div class="language">
                <span>LINGUA ORIGINALE: </span>
                <lang-flag :iso="DataMovies.original_language" />
            </div>
            <div class="vote">
                <span>VOTO: </span>
                <font-awesome-icon class="star" v-for="star in ConvertVote(DataMovies.vote_average)" :key="star"
                    :icon="['fas', 'star']" />
                <template v-for="star in 5 - ConvertVote(DataMovies.vote_average)">
                    <font-awesome-icon class="star" :key="star" :icon="['far', 'star']"
                        v-if="ConvertVote(DataMovies.vote_average) < 5" />
                </template>
            </div>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.card_movies {
    border: 1px solid black;
    color: darkorange;
    padding: 0.5rem;
    margin: .5rem 1rem;
}

.text {
    width: 342px;
}

.star {
    color: yellow;
}
</style>
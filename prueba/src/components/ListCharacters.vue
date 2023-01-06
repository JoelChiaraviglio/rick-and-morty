<template>

    <section>
        <div class="characters">
            <!--el v-for seria un foreach-->
            <div class="characters_item" v-for="character in characters" :key="character.id">
                <!--Mostrame la info que necesitemos, en este caso el namo de los personajes que estan dentros de la list de Characters-->
                <!--{{ character.name}}-->
                <CardCharacter :character="character" />
            </div>
        </div>
    </section>
</template>

<script>

    import { onMounted, computed } from 'vue'
    import { useStore } from 'vuex'

    import CardCharacter from '@/components/CardCharacter'
    export default {
        components: {
            CardCharacter
        },
        setup() {
            const store = useStore()
            const characters = computed(() => {
                return store.state.charactersFilter
            })
            onMounted(() => {
                store.dispatch('getCharacters')
            })

            return {
                characters
            }
        }
    }
</script>

<style lang="scss">
    .characters {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 3rem;
        margin: 3rem 0;
    }
</style>
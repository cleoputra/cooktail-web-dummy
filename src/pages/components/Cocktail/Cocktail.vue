<template>
<v-card>
    <v-container fluid grid-list-lg>
        <v-card-title>
                    <div>
                        <h2 class="title">{{cocktail.strDrink}}</h2>
                        <img :src="cocktail.strDrinkThumb" class='cocktail__image'></img>
                        <br/>
                        <b>Cocktail Receipt</b>
                        <ul>
                            <li v-for="ingredient in cocktail.ingredients" :key="ingredient">
                                {{ingredient}}
                            </li>
                        </ul>
                        <b>How to Make It?</b>
                        <br/>
                        {{cocktail.strInstructions}}
                        
                    </div>
                <v-spacer></v-spacer>
        </v-card-title>
        <v-card-text v-show="instructions">
            <div></div>
        </v-card-text>
    </v-container>
</v-card>
</template>

<script>
export default {
    name: "",
    props: ['cocktail'],
    data: function() {
        return {
            instructions: false
        }
    },
    methods: {
        toogleInstructions() {
            this.instructions = !this.instructions
        }
    }
}
</script>

<style scoped>
.cocktail__image{
    height: 150px;
}

</style>
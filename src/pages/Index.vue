<template>
  <div>
    <div class="page-header clear-filter" filter-color="orange">
      <parallax
        class="page-header-image" 
        style="background-image:url('img/cooktail.jpg')"
      >
      </parallax>
      <div class="container">
        <div class="content-center brand">
          <img class="n-logo" src="img/now-logo.png" alt="" />
          <h1 class="h1-seo">Cooktails.</h1>
          <h3>Drinks well with others.</h3>
        </div>
        <h6 class="category category-absolute">
          Coded by
Cleoputraa.
        </h6>
      </div>
    </div>
  <div class="section">
    <div class="container">
      <h3 class="title">Recommendations of The Day</h3>
      <div id="typography">
        <div class="row">
          <div class="col-md-12">
            <div class="typography-line">
              <blockquote>
                <p class="blockquote blockquote-primary">
                  <v-flex xs12 :key="cocktail.idDrink" v-for="cocktail in cocktails">
                      <cocktail :cocktail="cocktail" class='mb-2'>
                      </cocktail>
                  </v-flex>
                  <v-flex xs12 v-show="isLoading" key='loading'>
                      <skeleton-card class='skeleton-card--opacity' :hasHeader="false" :isHorizontal="true"> </skeleton-card>
                  </v-flex>

                </p>
                  <a
                    primary @click="getMore()"
                    class="btn btn-primary btn-round btn-lg center"> Get More</a>
              </blockquote>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

    <carousel-section></carousel-section>
    <div class="section">
      <div class="container text-center">
        <div class="row justify-content-md-center">
          <div class="col-md-12 col-lg-8">
            <h2 class="title">Completed Task</h2>
            <h5 class="description">
              Build Website Dummy for Gank Global Examination for Junior Frontend Engineer. Task Done: Using API Cooktails, 
              menus (up to date every you refresh your page), Using Axioss to fetch data, Show the receipts of all cooktails, Mobile Responsive 
              Application, and load less than 5 second. Very first time using Vue.js to build a website. Thankyou for the opportunity. 
            </h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Parallax } from '@/components';
import BasicElements from './components/BasicElementsSection';
import Navigation from './components/Navigation';
import TabsSection from './components/Tabs';
import ProgressPagination from './components/ProgressPagination';
import Notifications from './components/Notifications';
import Typography from './components/Typography';
import JavascriptComponents from './components/JavascriptComponents';
import CarouselSection from './components/CarouselSection';
import NucleoIconsSection from './components/NucleoIconsSection';
import SignupForm from './components/SignupForm';
import ExamplesSection from './components/ExamplesSection';
import DownloadSection from './components/DownloadSection';

import axios from 'axios'

import Cocktail from './components/Cocktail/Cocktail.vue'
import SkeletonCard from 'skeleton-card-vuejs'

const API_URL = 'https://www.thecocktaildb.com/api/json/v1/1/random.php'

export default {
  name: 'index',
  bodyClass: 'index-page',
    components: {
        Cocktail,
        SkeletonCard,
        Parallax,
        BasicElements,
        Navigation,
        TabsSection,
        ProgressPagination,
        Notifications,
        Typography,
        JavascriptComponents,
        CarouselSection,
        NucleoIconsSection,
        SignupForm,
        ExamplesSection,
        DownloadSection
    },
    mounted() {
        this.getMore()
    },
    data: function() {
        return {
            isLoading: false,
            cocktails: []
        }
    },
    methods: {
        getMore() {
            this.isLoading = true

            axios.get(API_URL)
                .then(({ data }) => {
                    var cocktail = data.drinks[0]
                    this.cocktails.push(cocktail)
                    cocktail.ingredients = this.createIngrediens(cocktail)
                    
                    this.isLoading = false
                    // scroll it to bottom
                    window.scrollTo(0,document.body.scrollHeight);

                })
                .catch(err => this.isLoading = false)
        },
        createIngrediens(cocktail) {
            var ingredients = []

            const ingredientKey = "strIngredient"
            const measureKey = "strMeasure"

            for (let i = 1; i < 6; i++) {

                let ingredientsString = ""
                ingredientsString += cocktail[measureKey + i]
                ingredientsString += cocktail[ingredientKey + i]
                // remove weird stuff
                ingredientsString = ingredientsString.replace(/\n/ig, '');
                ingredientsString = ingredientsString.trim()
                
                if (ingredientsString !== "") ingredients.push(ingredientsString)
            }

            return ingredients
        }
    }
}
</script>

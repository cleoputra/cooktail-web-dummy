<template>
  <div class="section" id="carousel">
    <div class="container">
      <div class="title">
      </div>
      <div class="row justify-content-center">
        <div class="col-8">
          <el-carousel height="500px">
            <el-carousel-item>
              <img class="d-block" src="img/c1.jpg" alt="First slide" />
              <div class="carousel-caption d-none d-md-block">
                <h5>Never too old to feel Amer</h5>
              </div>
            </el-carousel-item>
            <el-carousel-item>
              <img class="d-block" src="img/c3.jpg" alt="Second slide" />
              <div class="carousel-caption d-none d-md-block">
                <h5>Newcomers Cooktails from Bali</h5>
              </div>
            </el-carousel-item>
            <el-carousel-item>
              <img class="d-block" src="img/c2.jpg" alt="Third slide" />
              <div class="carousel-caption d-none d-md-block">
                <h5>Neverlasting Jack Daniels</h5>
              </div>
            </el-carousel-item>
          </el-carousel>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { Carousel, CarouselItem } from 'element-ui';

export default {
  components: {
    [Carousel.name]: Carousel,
    [CarouselItem.name]: CarouselItem
  }
};
</script>
<style></style>

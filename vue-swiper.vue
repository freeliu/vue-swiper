<template>
    <div class="swiper-container">
        <div class="swiper-wrapper">
            <div class="swiper-slide" v-for="(item,i) in items" :key="i">
                <a :title="item.title" :href="item.href" :data-clipboard-text="item.copyText">
                    <div class="swiper-slide-img-wraper" style="margin-bottom: 5px">
                        <img style="max-width: 100%" :src="item.src"/>
                    </div>
                    {{item.title}}}
                </a>

            </div>

        </div>
        <!-- Add Pagination -->
        <div class="swiper-pagination"></div>
        <!-- Add Arrows -->
        <!--<div class="swiper-button-next"></div>-->
        <!--<div class="swiper-button-prev"></div>-->
    </div>
</template>

<script>


    import Swiper from "swiper"
    import 'swiper/dist/css/swiper.min.css'

    export default {
        name: "vue-swiper",
        props: {
            items: {
                type: Array,
                required: true
            },
            autoplay: {
                type: Boolean
            },
            pagination: {
                type: Boolean
            },
            spaceBetween: {
                type: Number
            },
            slidesPerView: {
                type: Number
            },
            minHeight: {
                type: Number
            },
            imgWHRate: {
                type: Number
            },
            disableOnInteraction: {
                type: Boolean
            }
        },
        mounted() {
            let params = {}
            if (this.autoplay) {
                params.autoplay = {
                    delay: 2500,
                    disableOnInteraction: this.disableOnInteraction ? true : false,
                }
            }
            if (this.spaceBetween) {
                params.spaceBetween = this.spaceBetween
            }
            if (this.slidesPerView) {
                params.slidesPerView = this.slidesPerView
            }
            if (this.pagination) {
                params.pagination = {
                    el: '.swiper-pagination',
                    clickable: true,
                }
            }

            new Swiper('.swiper-container', params);

            if (this.minHeight) {
                for (let ele of document.getElementsByClassName("swiper-slide")) {
                    ele.style.minHeight = this.minHeight + 'px'
                }
            }
            if (this.imgWHRate) {
                for (let o of document.getElementsByClassName("swiper-slide-img-wraper")) {
                    o.style.height = o.clientWidth * this.imgWHRate + 'px'
                }
            }
        }
    }
</script>

<style scoped>
    /*.swiper-slide {*/
    /*min-height: 120px;*/
    /*}*/
    .swiper-slide-img-wraper {
        overflow-y: hidden;
    }

    .swiper-container {
        width: 100%;
        height: 100%;
    }

    .swiper-slide {
        text-align: center;
        /*font-size: 18px;*/
        /*background: #fff;*/
        /* Center slide text vertically */
        display: -webkit-box;
        display: -ms-flexbox;
        display: -webkit-flex;
        display: flex;
        -webkit-box-pack: center;
        -ms-flex-pack: center;
        -webkit-justify-content: center;
        justify-content: center;
        -webkit-box-align: center;
        -ms-flex-align: center;
        -webkit-align-items: center;
        align-items: center;
    }
</style>

<template>
    <div class="section py-[150px]">
        <div class="flex max-w-none justify-center mb-[50px]">
            <h2 class="!mt-0">{{ $t('carousel.title') }}</h2>
        </div>
        <div class="container mx-auto">
            <div class="glider-contain !w-[80%] !max-w-[800px]">
                <div class="glider">
                    <div v-for="num in [1, 2, 3, 4, 5]" :key="num">
                        <img
                            class="w-full"
                            :src="`./img/carousel-${
                                section.index[num - 1]
                            }.png`"
                            :alt="
                                $t(
                                    `carousel.${
                                        section.keys[num - 1]
                                    }.imageDesc`
                                )
                            "
                        />
                        <div class="max-w-none my-[20px]">
                            <h3>
                                <a
                                    :href="
                                        $t(
                                            `carousel.${
                                                section.keys[num - 1]
                                            }.link`
                                        )
                                    "
                                    target="_blank"
                                >
                                    {{
                                        $t(
                                            `carousel.${
                                                section.keys[num - 1]
                                            }.title`
                                        )
                                    }}
                                </a>
                            </h3>
                            <p>
                                {{
                                    $t(
                                        `carousel.${
                                            section.keys[num - 1]
                                        }.description`
                                    )
                                }}
                            </p>
                        </div>
                    </div>
                </div>
                <!--button aria-label="Previous" class="glider-prev">«</button-->
                <!--button aria-label="Next" class="glider-next">»</button-->
                <div role="tablist" class="dots"></div>
            </div>
        </div>
    </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

//@ts-ignore
import Glider from 'glider-js';

@Component
export default class CarouselV extends Vue {
    @Prop() section!: any;
    @Prop() index!: number;

    mounted() {
        new Glider(this.$el.querySelector('.glider'), {
            slidesToShow: 1,
            scrollLock: true,
            scrollLockDelay: 0,
            dots: '.dots',
            draggable: true
            /* arrows: {
                prev: '.glider-prev',
                next: '.glider-next'
            } */
        });
    }
}
</script>

<style lang="scss">
.glider-dot {
    @apply bg-green border border-solid border-gray-500 w-[20px] h-[20px] #{!important};
    &:focus {
        @apply border-black border-2 #{!important};
    }
    &.active {
        @apply saturate-200 border-2 #{!important};
    }
}

.glider {
    overflow-x: hidden;
}

.glider-slide {
    a {
        color: #0000ff !important;
        text-decoration: underline !important;
    }
}
</style>

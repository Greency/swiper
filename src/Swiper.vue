<template>
    <div class="swiper" v-on:touchstart='handleTouchStart' v-on:touchmove='handleTouchMove' v-on:touchend='handleTouchEnd'>
        <slot></slot>
        <div class="prev-btn" @click="handleChangeSwiper('prev')">上一页</div>
        <div class="next-btn" @click="handleChangeSwiper('next')">下一页</div>
    </div>
</template>
<script>
    export default{
        data(){
            return {
                currentSwiperIndex: 0
            }
        },
        mounted(){
            console.log('children: ', this.$children[0]);
            for(let i = 0, len = this.$children.length; i < len; i++){
                this.$children[i].$el.style = `transform: translate(${100 * i}%, 0px)`;
            }
        },
        methods: {
            handleTouchStart: function(e){
                console.log('touch start: ',e);
            },
            handleTouchMove: function(e) {
                console.log('touch move: ',e);
            },
            handleTouchEnd: function(e){
                console.log('touch end: ',e);
            },
            handleChangeSwiper: function(type){
                this.toggleSwiper(this.currentSwiperIndex + 1);
            },
            toggleSwiper: function(index){
                if(index > this.currentSwiperIndex){
                    for(let i = 0, len = this.$children.length; i < len; i++){
                        this.$children[i].$el.style = `transform: translate(${(i - index) * 100}%, 0px)`;
                    }
                }
                this.currentSwiperIndex = index;
            }
        }
    }
</script>
<style lang="stylus">
    .swiper
        position relative
        width 100%
        overflow hidden

    .swiper
        .prev-btn
            position absolute
            top 50px
            left 0
        
        .next-btn
            position absolute
            top 50px
            right 0
        
</style>

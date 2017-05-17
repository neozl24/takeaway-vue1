<template lang="html">
    <div class="cartcontrol">
        <div class="cart-decrease icon-remove_circle_outline" v-show="food.count>0" @click="decreaseCart" transition="move">
            <span class="inner icon-remove_circle_outline"></span>
        </div>
        <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
        <div class="cart-increase icon-add_circle" @click="increaseCart"></div>
    </div>
</template>

<script>
import Vue from 'vue';
export default {
    props: {
        food: {
            type: Object
        }
    },
    methods: {
        increaseCart(event) {
            if (!event._constructed) {
                // 如果没有_constructed这个属性，那么这个event就不是自己派发的，而是better-scroll组件派发的
                return;
            }
            if (!this.food.count) {
                Vue.set(this.food, 'count', 1);
            } else {
                this.food.count += 1;
            }
        },
        decreaseCart(event) {
            if (!event._constructed) {
                return;
            }
            if (this.food.count && this.food.count > 0) {
                this.food.count -= 1;
            }
        }
    }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
.cartcontrol
    font-size: 0
    .cart-decrease
        display: inline-block
        padding: 6px
        transition: all 0.2s linear
        &.move-transition
            opacity: 1
            transform: translate3d(0,0,0)
            .inner
                display: inline-block
                line-height: 24px
                font-size: 24px
                color: rgb(0,160,220)
                transition: all 0.2s linear
                transform: rotate(0)
        &.move-enter, &.move-leave
            opacity: 0
            transform: translate3d(24px,0,0)
            .inner
                transform: rotate(180deg)
    .cart-count
        display: inline-block
        vertical-align: top
        width: 12px
        padding-top: 6px
        line-height: 24px
        text-align: center
        font-size: 10px
        color: rgb(147, 153, 159)
    .cart-increase
        display: inline-block
        padding: 6px
        line-height: 24px
        font-size: 24px
        color: rgb(0,160,220)
</style>

<template>
    <view @touchstart="handleTouchStart" @touchend="handleTouchEnd">
        <slot></slot>
    </view>
</template>

<script>
export default {
    data() {
        return {
            startTime:0,
            startX:0,
            startY:0
        }
    },
    methods: {
        // 用户按下屏幕
        handleTouchStart(event){
            this.startTime = Date.now()
            this.startX = event.changedTouches[0].clientX
            this.startY = event.changedTouches[0].clientY
        },
        handleTouchEnd(event){
            const endTime = Date.now()
            const endX = event.changedTouches[0].clientX
            const endY = event.changedTouches[0].clientY

            //判断按下的时间
            if (endTime-this.startTime > 2000) {
                return
            }
            
            //滑动的方向
            let direction = ""

            //先判断用户滑动的距离是否合法  合法:再判断滑动的方向  距离加上绝对值
            if (Math.abs(endX - this.startX) > 10&&Math.abs(endY-this.startY)<10 ) {
                //滑动方向
                direction = endX - this.startX > 0 ? "right" : "left"
            }else{
                return
            }

            //用户做了合法的滑动操作
            console.log(direction);
            this.$emit('swiperAction',{direction})
        }
    },
};
</script>

<style scoped lang="scss">

</style>

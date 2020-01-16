<template>
    <div class="container">
    <!-- 通过Element-ui的走马灯组件el-carousel完成轮播图布局 -->
    <!-- 此处仍是使用静态页面，未使用后台 -->
    <el-carousel
    :interval="5000"
    arrow="always">
    <el-carousel-item
    v-for="(item, index) in banners"
    
    :key="index">
    <!-- 给轮播图相应样式避免缩小时缩小，以背景图形式 -->
    <div class="banner-image"
    :style="`background:url(${$axios.defaults.baseURL+item.url}) center center no-repeat;
    background-size:contain contain`">
    </div>
    </el-carousel-item>
    </el-carousel>
    </div>
</template>

<script>
export default {
    data(){
        return{
            //轮播图数据（网络图片）
            banners:[
                // {
                //     url:"http://157.122.54.189:9095/assets/images/th03.jfif"
                // },
                // {
                //     url: "http://157.122.54.189:9095/assets/images/th04.jfif", 
                // }
            ]
        }
    },
    mounted(){
        this.$axios({
            url: "/scenics/banners"
        }).then(res => {
            const {data} = res.data;
            this.banners = data;
        })
    },

}
</script>

<style scoped lang="less">
.container{
    min-width:1000px;
    margin:0 auto;
    position:relative;

    /deep/ .el-carousel__container{
        height:700px;
    }

    .banner-image{
        width:100%;
        height:100%;
    }
}
</style>
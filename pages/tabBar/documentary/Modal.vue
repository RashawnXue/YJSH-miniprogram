<template>
<div class="modal-mask"  @click.self="close">
<div class="modal-container">
<div class="modal-body" style="width: 375rpx; height: 66rpx; display: block; box-sizing: border-box">
<slot name="body" >
默认内容
</slot>
</div>
</div>
</div>
</template>
<script>
export default {
methods: {
close() {
this.$emit('changeshow', 'false');
},
nothing(){}
}
};
</script>
<style scoped>
.modal-mask {
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100%;
background-color: rgba(0, 0, 0, 0.5);
display: flex;
justify-content: center;
align-items: center;
z-index: 6;
}
.modal-container {
background-color: #fff;
border-radius: 5px;
width: 50%;
z-index: 7;
}
</style>
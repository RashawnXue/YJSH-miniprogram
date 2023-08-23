<template>
<div class="modal-mask" @click.self="close">
<div class="modal-container">
<div class="modal-header">
<slot name="header">
默认标题
</slot>
</div>
<div class="modal-body">
<slot name="body">
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
}
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
z-index: 4;
}
.modal-container {
background-color: #fff;
padding: 20px;
border-radius: 5px;
width: 50%;
}
</style>
<template>
    <div>
        <input type="file" ref="fileInput" multiple @change="loadFile" class="file-input">
        <div ref="content" class="file-content" @click="checkFile">
            <p v-if="!fileReader">Click here!</p>
            <img v-if="fileReader" :src="fileReader">
        </div>
    </div>
</template>

<script>
export default {
    name: "file-picker",
    data() {
        return {
            fileData: null,
            fileReader: null,
        };
    },
    methods: {
        checkFile: function() {
            const fileInput = this.$refs.fileInput;
            const clickEvent = new MouseEvent("click");
            fileInput.dispatchEvent(clickEvent);
            this.fileData = fileInput;
        },
        loadFile: function() {
            const fileReader = new FileReader();
            const file = this.fileData.files[0];
            if(file) {
                fileReader.readAsDataURL(file);
                this.fileReader = fileReader.result;
                fileReader.addEventListener('load', () => this.fileReader = fileReader.result);
            } else {
                this.fileReader = '';
            }
        },
    }
};
</script>

<style lang="scss" scoped>
@import "../../styles/mixins";

input.file-input {
    display: none;
}
div.file-content {
    @include flexbox($align: center, $justify: center);
    width: 200px;
    height: 200px;
    border: 1px solid black;
    border-radius: 50%;
    overflow: hidden;
    cursor: pointer;
    img {
        width: 100%;
       height: 100%;
    }
}
</style>

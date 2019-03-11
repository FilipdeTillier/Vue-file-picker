<template>
    <div>
        <input type="file" ref="fileInput" multiple @change="loadFile" class="file-input">
        <div ref="content" class="file-content" @click="checkFile">
            <p v-if="!fileReader">Click here!</p>
            <img v-if="load" :src="fileReader.result">
        </div>
        <div @click="check">Check</div>
    </div>
</template>

<script>
export default {
    name: "file-picker",
    data() {
        return {
            fileData: null,
            fileReader: null,
            load: false,
        };
    },
    methods: {
        checkFile: function() {
            const fileInput = this.$refs.fileInput;
            const clickEvent = new MouseEvent("click");
            fileInput.dispatchEvent(clickEvent);
            this.fileData = fileInput;
        },
        loadFile: async function() {
            const fileReader = new FileReader();
            await fileReader.readAsDataURL(this.fileData.files[0]);
            this.fileReader = await fileReader;
            this.load = true;
            // setTimeout(() => this.load = true, 10)
            
        },
        check: function() {
            console.log(this.fileReader.result);
            // this.fileReader = this.fileReader.result;
            // console.log(this.fileData.files[0]);
            // console.log(this.$refs.fileInput.value);
            // console.log("tutaj", this.fileReadre.result);
        }
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
    cursor: pointer;
}
</style>

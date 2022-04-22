<template>
    <div class="mt-4">
        <file-pond
        name="image"
        ref="pond"
        label-idle="Click to choose image, or drag here..."
        @init="filepondInitialized"
        accepted-file-types="image/*"
        />
<!--        :allow-browse="false"-->

    </div>
</template>
<script>
import vueFilePond, { setOptions } from 'vue-filepond';
import "filepond/dist/filepond.min.css";
import FilePondPluginFileValidateType from 'filepond-plugin-file-validate-type';

setOptions({
    server: {
        process: {
            url: './upload',
            headers: {
                'X-CSRF-TOKEN': document.head.querySelector('meta[name="csrf_token"]').content
            }
        }
    }
})

const FilePond = vueFilePond(FilePondPluginFileValidateType);

export default {
    data() {
        return {
        }
    },
    components: {
        // it is possible to change the component name
        // 'vue-filepond' : FilePond
        // Automatically goes to lowercase and adds - to capital letters except the first one
        FilePond,
    },
    methods: {
        filepondInitialized(){
            console.log('Filepond is ready!');
            console.log('Filepond object:', this.$refs.pond);
        }
    }
}
</script>

<template>
    <div id="app">
        <form v-on:submit.prevent="submit">
            <input type="text" v-model="dataEditor.title" placeholder="Judul">
            <ckeditor :editor="editor" v-model="editorData" :config="editorConfig"></ckeditor>
            <button type="submit">button Submit</button>
        </form>
        <button @click="checked">cek sini</button>

    </div>
</template>

<script>
import ClassicEditor from '@ckeditor/ckeditor5-build-classic';
// import UploadAdapter from "../adapter/uploadAdapter"


export default {
    name: 'app',
    props: {
        getId: String,
        propsDataEditor: Array,
    },
    mounted() {
    },
    data() {
        return {
            editor: ClassicEditor,
            editorData: "",
            editorConfig: {
                link: {
                    addTargetToExternalLinks: true,
                    defaultProtocol: 'http://localhost:8000'
                },
                ckfinder: {
                    // The URL that the images are uploaded to.
                    uploadUrl: 'http://localhost:8000/upload',
                    // Enable the XMLHttpRequest.withCredentials property.
                    withCredentials: true,
                }
            },
            dataEditor: {
                id: "1sdasdkjjkd",
                body: "",
                title: "",
                date: 1666345325369,
            }
        };
    },
    methods: {
        submit() {
            this.dataEditor.body = this.editorData;
            this.editorData = '';
            this.$emit('add-data-article', this.dataEditor)
            this.dataEditor = {
                id: "",
                body: "",
                title: "",
                date: ""
            }
        },
        checked() {
            this.editorData = this.propsDataEditor[0].title;
        },
        filtering() {
            if (this.getId != undefined) {
                const filtering = this.propsDataEditor
                filtering.forEach(element => {
                    if (element.id === this.id) {
                        return element.body
                    }
                });
            }
            else {
                return ""
            }
        }
    }
}
</script>

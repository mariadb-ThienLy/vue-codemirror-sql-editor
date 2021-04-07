<template>
    <textarea ref="txt" class="txt" v-model="queryData" />
</template>

<script>
import CodeMirror from 'codemirror'
import 'codemirror/lib/codemirror.css'
import './mariadb-style.scss'
import 'codemirror/addon/hint/show-hint.js'
// For prototyping purpose, using readymade sql hint parser
import 'codemirror/addon/hint/sql-hint.js'
export default {
    name: 'editor-view',
    props: {
        dist: { type: Object, require: true },
        queryData: { type: String, require: true },
    },
    data() {
        return {
            editor: null,
        }
    },

    mounted() {
        this.editor = CodeMirror.fromTextArea(this.$refs.txt, {
            tabSize: 4,
            mode: 'text/x-mariadb',
            theme: 'mariadb-style',
            lineNumbers: true,
            line: true,
            lineWrapping: true,
            hintOptions: {
                completeSingle: false,
                hint: CodeMirror.hint.sql,
                tables: this.dist,
            },
            extraKeys: { 'Ctrl-Space': 'autocomplete' },
        })

        this.editor.on('keypress', (editor) => {
            editor.showHint()
        })

        const self = this
        this.editor.on('change', function (cm) {
            self.$emit('on-change', cm.getValue())
        })
    },
}
</script>

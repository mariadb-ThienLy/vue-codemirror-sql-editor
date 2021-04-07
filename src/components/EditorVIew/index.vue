<template>
    <textarea ref="txt" class="txt" v-model="queryData" />
</template>

<script>
import CodeMirror from 'codemirror'
import { format } from 'sql-formatter'
import 'codemirror/lib/codemirror.css'
import './mariadb-style.scss'
import 'codemirror/addon/hint/show-hint.js'
import 'codemirror/addon/hint/sql-hint.js'
import 'codemirror/addon/search/search.js'
import 'codemirror/addon/search/matchesonscrollbar.js'
import 'codemirror/addon/search/matchesonscrollbar.css'
import 'codemirror/addon/search/match-highlighter.js'
import 'codemirror/addon/search/jump-to-line.js'
import 'codemirror/addon/dialog/dialog.js'
import 'codemirror/addon/dialog/dialog.css'

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
            hint: CodeMirror.hint.sql,
            hintOptions: {
                completeSingle: false,
                tables: this.dist,
            },
            extraKeys: { 'Ctrl-Space': 'autocomplete', 'Ctrl-Shift-I': this.autoFormatSelection },
        })

        this.editor.on('keypress', (editor) => editor.showHint())

        const self = this
        this.editor.on('change', (cm) => self.$emit('on-change', cm.getValue()))
    },
    methods: {
        mariadbFormatter(v) {
            return format(v, {
                language: 'mariadb',
                indent: '    ',
                uppercase: true,
                linesBetweenQueries: 1,
            })
        },
        autoFormatSelection() {
            let sqlcontent = ''
            sqlcontent = this.editor.getValue()
            sqlcontent = this.mariadbFormatter(sqlcontent)
            this.editor.getDoc().setValue(sqlcontent)
        },
    },
}
</script>

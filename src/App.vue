<template>
    <div id="app">
        <editor-view :dist="dist" />
    </div>
</template>

<script>
import EditorView from './components/EditorView.vue'

export default {
    name: 'App',
    components: {
        EditorView,
    },
    data() {
        return {
            dist: [
                { className: 'sql', text: 'SELECT' },
                { className: 'sql', text: 'FROM' },
                { className: 'sql', text: 'WHERE' },
                { className: 'sql', text: 'INNER' },
                { className: 'sql', text: 'JOIN' },
                { className: 'sql', text: 'UNION' },
                { className: 'sql', text: 'EXEC' },
                { className: 'sql', text: 'INSERT' },
                { className: 'sql', text: 'INTO' },
                { className: 'sql', text: 'VALUES' },
                { className: 'sql', text: 'UPDATE' },
                { className: 'sql', text: 'DELETE' },
                { className: 'sql', text: 'GROUP' },
                { className: 'sql', text: 'BY' },
                { className: 'sql', text: 'HAVING' },
                { className: 'sql', text: 'IS' },
                { className: 'sql', text: 'DISTINCT' },
                { className: 'sql', text: 'OUTER' },
                { className: 'sql', text: 'TOP' },
                { className: 'sql', text: 'EXISTS' },
                { className: 'sql', text: 'WHEN' },
                { className: 'sql', text: 'CASE' },
                { className: 'sql', text: 'CAST' },
                { className: 'sql', text: 'IN' },
                { className: 'sql', text: 'NULL' },
                { className: 'table', text: 'te_cash_exchange_new' },
                { className: 'table', text: 'ParamsAtos' },
                { className: 'table', text: 'te_client_transfers' },
                { className: 'column', text: 'status_cash' },
                { className: 'column', text: 'datet' },
                { className: 'column', text: 'ammount' },
                { className: 'column', text: 'cash_exchange_id_start' },
                { className: 'column', text: 'cash_exchange_id_end' },
                { className: 'pf', text: 'AddParamAtos' },
                { className: 'pf', text: 'verify_backoffice_user' },
                { className: 'pf', text: 'checkAllowOperation' },
                { className: 'pf', text: 'addMoneyIn_01' },
            ],
        }
    },
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
}
</style>

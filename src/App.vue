<template>
    <div id="app">
        <div class="row">
            <h1 class="title">Editor view using codemirror</h1>
        </div>
        <div class="row">
            <div class="table-col">
                <ul v-for="(cols, tableName) in dist" :key="tableName">
                    <li>
                        {{ tableName }}
                        <ul v-for="col in cols" :key="col">
                            <li>{{ col }}</li>
                        </ul>
                    </li>
                </ul>
            </div>
            <div class="editor-view">
                <editor-view :dist="dist" :queryData="queryData" @on-change="onEditorChange" />
            </div>
            <div class="query">
                <p>Query to sent via API</p>
                <code>
                    <pre>{{ queryData }}</pre>
                </code>
            </div>
        </div>
    </div>
</template>

<script>
import EditorView from './components/EditorVIew/index.vue'

export default {
    name: 'App',
    components: {
        EditorView,
    },
    data() {
        return {
            dist: {
                table1: ['col_A', 'col_B', 'col_C'],
                table2: ['other_columns1', 'other_columns2'],
            },
            queryData: `CREATE TABLE dbo.EmployeePhoto\n(\n    EmployeeId INT NOT NULL PRIMARY KEY,\n    Photo VARBINARY(MAX) FILESTREAM NULL,\n    MyRowGuidColumn UNIQUEIDENTIFIER NOT NULL ROWGUIDCOL\n                    UNIQUE DEFAULT NEWID()\n);\n\nGO\n\n/*\ntext_of_comment\n/* nested comment */\n*/\n\n-- line comment\n\nCREATE NONCLUSTERED INDEX IX_WorkOrder_ProductID\n    ON Production.WorkOrder(ProductID)\n    WITH (FILLFACTOR = 80,\n        PAD_INDEX = ON,\n        DROP_EXISTING = ON);\nGO\n\nWHILE (SELECT AVG(ListPrice) FROM Production.Product) < $300\nBEGIN\n   UPDATE Production.Product\n      SET ListPrice = ListPrice * 2\n   SELECT MAX(ListPrice) FROM Production.Product\n   IF (SELECT MAX(ListPrice) FROM Production.Product) > $500\n      BREAK\n   ELSE\n      CONTINUE\nEND\nPRINT 'Too much for the market to bear';\n\nMERGE INTO Sales.SalesReason AS [Target]\nUSING (VALUES ('Recommendation','Other'), ('Review', 'Marketing'), ('Internet', 'Promotion'))\n       AS [Source] ([NewName], NewReasonType)\nON [Target].[Name] = [Source].[NewName]\nWHEN MATCHED\nTHEN UPDATE SET ReasonType = [Source].NewReasonType\nWHEN NOT MATCHED BY TARGET\nTHEN INSERT ([Name], ReasonType) VALUES ([NewName], NewReasonType)\nOUTPUT $action INTO @SummaryOfChanges;\n\nSELECT ProductID, OrderQty, SUM(LineTotal) AS Total\nFROM Sales.SalesOrderDetail\nWHERE UnitPrice < $5.00\nGROUP BY ProductID, OrderQty\nORDER BY ProductID, OrderQty\nOPTION (HASH GROUP, FAST 10);\n`,
        }
    },

    methods: {
        onEditorChange(v) {
            this.queryData = v
        },
    },
}
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    width: 100%;
}
.title {
    text-align: center;
    margin-bottom: 30px;
}
.row {
    flex-wrap: nowrap;
    display: flex;
}
.table-col {
    flex: 0 0 20%;
    max-width: 20%;
}
.editor-view {
    flex: 0 0 50%;
    max-width: 50%;
    height: 50vh;
}
.query {
    padding-left: 20px;
    flex: 0 0 30%;
    max-width: 30%;
    height: 50vh;
}
</style>

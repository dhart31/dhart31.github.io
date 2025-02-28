---
title: "Querying a recipe database with DuckDB WASM"
---

<textarea id="query" rows="4" cols="50">SELECT 42 AS answer;</textarea>
<style>
    #query {
        background-color: black;
        color: white;
        font-family: monospace;
        border: 1px solid #555;
        padding: 10px;
        width: 100%;
        min-height: 100px;
        outline: none;
        caret-color: white; /* Blinking white cursor */
    }
</style>
<button id="run-btn">Run Query</button>

<!-- Table for query results -->
<table id="query-results" border="1" style="width:100%; border-collapse: collapse; margin-top: 10px;">
    <thead>
        <tr></tr>
    </thead>
    <tbody></tbody>
</table>

<script type="module">
    import * as duckdb from "https://cdn.jsdelivr.net/npm/@duckdb/duckdb-wasm@1.29.0/+esm";

    let dbInstance;

    async function setupDuckDB() {
        const JSDELIVR_BUNDLES = duckdb.getJsDelivrBundles();
        const bundle = await duckdb.selectBundle(JSDELIVR_BUNDLES);

        const worker_url = URL.createObjectURL(
            new Blob([`importScripts("${bundle.mainWorker}");`], { type: 'text/javascript' })
        );

        const worker = new Worker(worker_url);
        const logger = new duckdb.ConsoleLogger();
        const db = new duckdb.AsyncDuckDB(logger, worker);
        await db.instantiate(bundle.mainModule, bundle.pthreadWorker);
        URL.revokeObjectURL(worker_url);
        return db;
    }

    async function runQuery() {
        if (!dbInstance) {
            dbInstance = await setupDuckDB();
            const response = await fetch('/db-recipes.json');
            const data = new Uint8Array(await response.arrayBuffer());
            await dbInstance.registerFileBuffer('db-recipes.json', data);
        }

        const conn = await dbInstance.connect();

        const queryText = document.getElementById("query").value;

        try {
            const result = await conn.query(queryText);
            renderTable(result);
        } catch (error) {
            document.getElementById("query-results").innerHTML = `<tr><td>Error: ${error.message}</td></tr>`;
        }
    }

    function renderTable(result) {
        const rows = result.toArray();
        const columns = result.schema.fields.map(field => field.name);

        // Populate table headers
        const thead = document.querySelector("#query-results thead");
        thead.innerHTML = `<tr>${columns.map(col => `<th>${col}</th>`).join("")}</tr>`;

        // Populate table rows
        const tbody = document.querySelector("#query-results tbody");
        tbody.innerHTML = rows.map(row => 
            `<tr>${columns.map(col => `<td>${row[col]}</td>`).join("")}</tr>`
        ).join("");
    }

    document.getElementById("run-btn").addEventListener("click", runQuery);
</script>

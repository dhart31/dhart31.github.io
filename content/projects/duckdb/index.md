---
title: "DuckDB WASM Terminal"
summary: "Run SQL queries on Parquet files in your browser"
date: 2025-02-15
---
{{< rawhtml >}}
<style>
:root {
    --bg-primary: #1a1a1a;
    --bg-secondary: #2d2d2d;
    --bg-tertiary: #3a3a3a;
    --text-primary: #ffffff;
    --text-secondary: #b0b0b0;
    --accent: #00d4aa;
    --accent-hover: #00b894;
    --border: #555555;
    --error: #ff6b6b;
    --success: #51cf66;
    --warning: #ffd43b;
}

* {
    box-sizing: border-box;
}

body, html {
    margin: 0;
    padding: 0;
    overflow-x: hidden;
}

.container {
    margin: 0;
    padding: 0;
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
}

.section {
    margin: 0;
}

.section-title {
    font-size: 14px;
    font-weight: 500;
    margin: 0;
    padding: 10px 20px;
    color: var(--text-primary);
    background-color: var(--bg-secondary);
    border-bottom: 1px solid var(--border);
}

.info-box {
    background-color: rgba(0, 212, 170, 0.1);
    border-bottom: 1px solid var(--accent);
    padding: 10px 20px;
    color: var(--text-secondary);
    font-size: 13px;
}

.info-box code {
    background-color: var(--bg-tertiary);
    padding: 2px 6px;
    border-radius: 3px;
    font-family: monospace;
    font-size: 12px;
    color: var(--text-primary);
}

/* File Upload */
.file-upload-area {
    padding: 10px 20px;
    background-color: var(--bg-secondary);
    display: flex;
    align-items: center;
    gap: 15px;
    width: 100vw;
    margin-left: calc(50% - 50vw);
    margin-right: calc(50% - 50vw);
    flex-wrap: wrap;
}

#file-input {
    display: none;
}

.file-input-button {
    padding: 0px 5px;
    background-color: var(--accent);
    color: var(--bg-primary);
    border-radius: 6px;
    cursor: pointer;
    font-weight: 500;
    font-size: 13px;
    display: inline-block;
    transition: background-color 0.2s;
}

.file-input-button:hover {
    background-color: var(--accent-hover);
}

.uploaded-files {
    display: flex;
    gap: 10px;
    flex-wrap: wrap;
}

.uploaded-file {
    background-color: var(--bg-tertiary);
    padding: 6px 10px;
    border-radius: 4px;
    display: flex;
    align-items: center;
    gap: 10px;
    border: 1px solid var(--border);
}

.uploaded-file-name {
    font-family: monospace;
    font-size: 13px;
    color: var(--text-primary);
    font-weight: 500;
}

.uploaded-file-size {
    font-size: 12px;
    color: var(--text-secondary);
    margin-left: 10px;
}

.btn-small {
    padding: 4px 10px;
    font-size: 12px;
    background-color: var(--error);
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.btn-small:hover {
    background-color: #ff5252;
}

/* Terminal */
.terminal {
    background-color: #0d0d0d;
    padding: 20px;
    font-family: 'Monaco', 'Menlo', 'Ubuntu Mono', 'Consolas', monospace;
    font-size: 13px;
    height: calc(100vh - 120px);
    width: 100vw;
    margin-left: calc(50% - 50vw);
    margin-right: calc(50% - 50vw);
    overflow-y: auto;
    overflow-x: auto;
    color: #e0e0e0;
}

.terminal-output {
    white-space: pre;
    margin-bottom: 20px;
    line-height: 1.5;
}

.terminal-prompt {
    display: flex;
    align-items: flex-start;
    margin-bottom: 10px;
}

.terminal-prompt-symbol {
    color: var(--accent);
    margin-right: 8px;
    flex-shrink: 0;
}

#terminal-input {
    flex: 1;
    background: transparent;
    border: none;
    color: #e0e0e0;
    font-family: inherit;
    font-size: inherit;
    outline: none;
    resize: none;
    overflow: hidden;
    min-height: 20px;
}

.terminal-error {
    color: var(--error);
}

.terminal-success {
    color: var(--success);
}

.status-message {
    padding: 12px;
    border-radius: 6px;
    margin-bottom: 15px;
    font-size: 14px;
}

.status-loading {
    background-color: rgba(255, 212, 59, 0.1);
    border: 1px solid var(--warning);
    color: var(--warning);
}

.status-success {
    background-color: rgba(81, 207, 102, 0.1);
    border: 1px solid var(--success);
    color: var(--success);
}

.status-error {
    background-color: rgba(255, 107, 107, 0.1);
    border: 1px solid var(--error);
    color: var(--error);
}

.terminal::-webkit-scrollbar {
    width: 8px;
}

.terminal::-webkit-scrollbar-track {
    background: #0d0d0d;
}

.terminal::-webkit-scrollbar-thumb {
    background: var(--border);
    border-radius: 4px;
}

.export-buttons {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-left: auto;
}

.export-label {
    color: var(--text-secondary);
    font-size: 13px;
    font-weight: 500;
}

.export-button {
    background-color: var(--accent);
    color: #000;
    border: none;
    padding: 6px 14px;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 500;
    font-size: 13px;
    transition: background-color 0.2s;
}

.export-button:hover {
    background-color: var(--accent-hover);
}
</style>

<div class="container">
    <div class="info-box">
        <strong>Tip:</strong> Query files directly from URLs (requires CORS headers):
        <br><code>SELECT * FROM read_parquet('https://example.com/data.parquet')</code>
        <br><code>SELECT * FROM read_csv('https://example.com/data.csv')</code>
        <br><code>SELECT * FROM read_json('https://example.com/data.json')</code>
        <br>For S3 buckets with CORS headers, use DuckDB CLI: <code>SELECT * FROM read_parquet('s3://bucket-name/path/*.parquet')</code>
    </div>

    <div id="status"></div>

    <div class="section">
        <div class="file-upload-area">
            <button class="file-input-button" id="folder-button">
                Upload Folder
            </button>
            <label for="file-input" class="file-input-button">
                Upload File(s)
            </label>
            <input type="file" id="file-input" accept=".parquet,.csv,.json,.tsv,.txt" multiple />
            <input type="file" id="folder-input" webkitdirectory directory style="display: none;" />

            <div id="export-buttons" class="export-buttons" style="display: none;">
                <span class="export-label">Export last result:</span>
                <button class="export-button" onclick="exportCSV()">CSV</button>
                <button class="export-button" onclick="exportJSON()">JSON</button>
                <button class="export-button" onclick="exportParquet()">Parquet</button>
            </div>

            <div class="uploaded-files" id="uploaded-files"></div>
        </div>
    </div>

    <div class="section">
        <div class="terminal" id="terminal">
            <div id="terminal-history"></div>
            <div class="terminal-prompt">
                <span class="terminal-prompt-symbol">duckdb&gt;</span>
                <textarea id="terminal-input" rows="1" placeholder="Type SQL query and press Enter. Ctrl+L to clear."></textarea>
            </div>
        </div>
    </div>
</div>

<script type="module">
import * as duckdb from "https://cdn.jsdelivr.net/npm/@duckdb/duckdb-wasm@1.29.0/+esm";

let db = null;
let conn = null;
let uploadedFiles = [];
let queryHistory = [];
let historyIndex = -1;
let savedDirHandle = null;
let lastQueryResult = null;

async function initDuckDB() {
    try {
        updateStatus('loading', 'Initializing DuckDB WASM...');

        const JSDELIVR_BUNDLES = duckdb.getJsDelivrBundles();
        const bundle = await duckdb.selectBundle(JSDELIVR_BUNDLES);

        const worker_url = URL.createObjectURL(
            new Blob([`importScripts("${bundle.mainWorker}");`], { type: 'text/javascript' })
        );

        const worker = new Worker(worker_url);
        const logger = new duckdb.ConsoleLogger();
        db = new duckdb.AsyncDuckDB(logger, worker);
        await db.instantiate(bundle.mainModule, bundle.pthreadWorker);
        URL.revokeObjectURL(worker_url);

        conn = await db.connect();

        updateStatus('success', 'DuckDB initialized! Upload Parquet files and run SQL queries.');
        addTerminalOutput('DuckDB WASM ready. Type SQL queries below.\n', 'success');
    } catch (error) {
        updateStatus('error', `Failed to initialize: ${error.message}`);
        console.error('Initialization error:', error);
    }
}

async function handleFileUpload(event) {
    const files = event.target.files;

    for (const file of files) {
        try {
            updateStatus('loading', `Loading ${file.name}...`);

            const arrayBuffer = await file.arrayBuffer();
            const uint8Array = new Uint8Array(arrayBuffer);

            await db.registerFileBuffer(file.name, uint8Array);

            uploadedFiles.push({
                name: file.name,
                size: file.size
            });

            renderUploadedFiles();
            updateStatus('success', `Loaded ${file.name}`);
            addTerminalOutput(`-- File loaded: ${file.name}\n`, 'success');
        } catch (error) {
            updateStatus('error', `Failed to load ${file.name}: ${error.message}`);
            addTerminalOutput(`-- Error: ${error.message}\n`, 'error');
        }
    }
}

function renderUploadedFiles() {
    const container = document.getElementById('uploaded-files');

    if (uploadedFiles.length === 0) {
        container.innerHTML = '';
        return;
    }

    const html = uploadedFiles.map((file, index) => `
        <div class="uploaded-file">
            <div>
                <span class="uploaded-file-name">${file.name}</span>
                <span class="uploaded-file-size">(${(file.size / 1024 / 1024).toFixed(2)} MB)</span>
            </div>
            <button class="btn-small" onclick="removeFile(${index})">Remove</button>
        </div>
    `).join('');

    container.innerHTML = html;
}

window.removeFile = function(index) {
    uploadedFiles.splice(index, 1);
    renderUploadedFiles();
};

function updateStatus(type, message) {
    const statusDiv = document.getElementById('status');
    statusDiv.className = `status-message status-${type}`;
    statusDiv.textContent = message;

    if (type === 'success') {
        setTimeout(() => {
            statusDiv.className = '';
            statusDiv.textContent = '';
        }, 5000);
    }
}

function addTerminalOutput(text, type = '') {
    const history = document.getElementById('terminal-history');
    const output = document.createElement('div');
    output.className = `terminal-output ${type ? 'terminal-' + type : ''}`;
    output.textContent = text;
    history.appendChild(output);

    const terminal = document.getElementById('terminal');
    terminal.scrollTop = terminal.scrollHeight;
}

function clearTerminal() {
    const history = document.getElementById('terminal-history');
    history.innerHTML = '';
}

async function executeQuery(query) {
    if (!query.trim()) return;

    // Add to history
    queryHistory.push(query);
    historyIndex = queryHistory.length;

    addTerminalOutput(`duckdb> ${query}\n`);

    try {
        const result = await conn.query(query);
        const rows = result.toArray();
        const columns = result.schema.fields.map(f => f.name);

        // Store last result for export
        lastQueryResult = { rows, columns };

        // Format as table
        const output = formatTable(columns, rows);
        addTerminalOutput(output + '\n');

        // Show export buttons if there are results
        if (rows.length > 0) {
            showExportButtons();
        }
    } catch (error) {
        addTerminalOutput(`Error: ${error.message}\n`, 'error');
        hideExportButtons();
    }
}

function formatTable(columns, rows) {
    if (rows.length === 0) {
        return '(0 rows)';
    }

    // Calculate column widths
    const widths = columns.map((col, i) => {
        const maxContentWidth = Math.max(
            ...rows.map(row => String(row[col] ?? '').length)
        );
        return Math.max(col.length, maxContentWidth, 3);
    });

    // Header
    const header = columns.map((col, i) => col.padEnd(widths[i])).join(' | ');
    const separator = widths.map(w => '-'.repeat(w)).join('-+-');

    // Rows
    const dataRows = rows.map(row =>
        columns.map((col, i) =>
            String(row[col] ?? '').padEnd(widths[i])
        ).join(' | ')
    );

    return [header, separator, ...dataRows, `\n(${rows.length} rows)`].join('\n');
}

function showExportButtons() {
    document.getElementById('export-buttons').style.display = 'flex';
}

function hideExportButtons() {
    document.getElementById('export-buttons').style.display = 'none';
}

function downloadFile(content, filename, mimeType) {
    const blob = new Blob([content], { type: mimeType });
    const url = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = url;
    link.download = filename;
    link.click();
    URL.revokeObjectURL(url);
}

async function exportCSV() {
    if (!lastQueryResult) return;

    const { rows, columns } = lastQueryResult;

    // Header
    let csv = columns.join(',') + '\n';

    // Rows
    rows.forEach(row => {
        csv += columns.map(col => {
            const val = row[col];
            if (val === null || val === undefined) return '';
            const str = String(val);
            // Escape quotes and wrap in quotes if contains comma or quote
            if (str.includes(',') || str.includes('"') || str.includes('\n')) {
                return `"${str.replace(/"/g, '""')}"`;
            }
            return str;
        }).join(',') + '\n';
    });

    downloadFile(csv, `query_result_${Date.now()}.csv`, 'text/csv');
    addTerminalOutput('-- Exported to CSV\n', 'success');
}

async function exportJSON() {
    if (!lastQueryResult) return;

    const { rows } = lastQueryResult;
    const json = JSON.stringify(rows, null, 2);

    downloadFile(json, `query_result_${Date.now()}.json`, 'application/json');
    addTerminalOutput('-- Exported to JSON\n', 'success');
}

async function exportParquet() {
    if (!lastQueryResult) return;

    try {
        const { rows, columns } = lastQueryResult;
        const filename = `query_result_${Date.now()}.parquet`;

        // Register the result as a table in DuckDB
        await db.registerFileText('temp_data.json', JSON.stringify(rows));

        // Create table from JSON and export to parquet
        await conn.query(`COPY (SELECT * FROM read_json_auto('temp_data.json')) TO '${filename}' (FORMAT PARQUET)`);

        // Get the file and download
        const fileBuffer = await db.copyFileToBuffer(filename);
        const blob = new Blob([fileBuffer], { type: 'application/octet-stream' });
        const url = URL.createObjectURL(blob);
        const link = document.createElement('a');
        link.href = url;
        link.download = filename;
        link.click();
        URL.revokeObjectURL(url);

        // Cleanup
        await db.dropFile('temp_data.json');
        await db.dropFile(filename);

        addTerminalOutput('-- Exported to Parquet\n', 'success');
    } catch (error) {
        addTerminalOutput(`-- Export error: ${error.message}\n`, 'error');
    }
}

// Terminal input handling
const terminalInput = document.getElementById('terminal-input');

terminalInput.addEventListener('keydown', (e) => {
    if (e.key === 'Enter' && !e.shiftKey) {
        e.preventDefault();
        const query = terminalInput.value.trim();
        if (query) {
            executeQuery(query);
            terminalInput.value = '';
        }
    } else if (e.key === 'ArrowUp') {
        e.preventDefault();
        if (historyIndex > 0) {
            historyIndex--;
            terminalInput.value = queryHistory[historyIndex];
            // Move cursor to end
            setTimeout(() => {
                terminalInput.selectionStart = terminalInput.selectionEnd = terminalInput.value.length;
            }, 0);
        }
    } else if (e.key === 'ArrowDown') {
        e.preventDefault();
        if (historyIndex < queryHistory.length - 1) {
            historyIndex++;
            terminalInput.value = queryHistory[historyIndex];
            // Move cursor to end
            setTimeout(() => {
                terminalInput.selectionStart = terminalInput.selectionEnd = terminalInput.value.length;
            }, 0);
        } else if (historyIndex === queryHistory.length - 1) {
            historyIndex = queryHistory.length;
            terminalInput.value = '';
        }
    } else if (e.ctrlKey && e.key === 'l') {
        e.preventDefault();
        clearTerminal();
    }
});

// Auto-resize textarea
terminalInput.addEventListener('input', () => {
    terminalInput.style.height = 'auto';
    terminalInput.style.height = terminalInput.scrollHeight + 'px';
});

async function loadFromFolder(dirHandle) {
    updateStatus('loading', 'Scanning folder for Parquet files...');

    const parquetFiles = [];
    const validExtensions = ['.parquet', '.csv', '.json', '.tsv', '.txt'];

    for await (const entry of dirHandle.values()) {
        if (entry.kind === 'file') {
            const hasValidExt = validExtensions.some(ext => entry.name.toLowerCase().endsWith(ext));
            if (hasValidExt) {
                parquetFiles.push(entry);
            }
        }
    }

    if (parquetFiles.length === 0) {
        updateStatus('error', 'No data files found in folder (.parquet, .csv, .json, .tsv, .txt)');
        return;
    }

    updateStatus('loading', `Found ${parquetFiles.length} data files. Loading...`);

    for (const fileHandle of parquetFiles) {
        const file = await fileHandle.getFile();
        const arrayBuffer = await file.arrayBuffer();
        const uint8Array = new Uint8Array(arrayBuffer);

        await db.registerFileBuffer(file.name, uint8Array);

        uploadedFiles.push({
            name: file.name,
            size: file.size
        });

        addTerminalOutput(`-- File loaded: ${file.name}\n`, 'success');
    }

    renderUploadedFiles();
    updateStatus('success', `Loaded ${parquetFiles.length} data files from folder`);
}

async function handleFolderSelect() {
    try {
        // Check if File System Access API is supported (Chrome/Edge)
        if ('showDirectoryPicker' in window) {
            let dirHandle;

            // Try to reuse saved folder
            if (savedDirHandle) {
                try {
                    // Verify we still have permission
                    const permission = await savedDirHandle.queryPermission({ mode: 'read' });
                    if (permission === 'granted') {
                        dirHandle = savedDirHandle;
                        updateStatus('loading', 'Using saved folder...');
                    }
                } catch (e) {
                    // Saved handle is invalid, will prompt for new one
                    savedDirHandle = null;
                }
            }

            // If no saved folder or permission denied, ask user to select
            if (!dirHandle) {
                dirHandle = await window.showDirectoryPicker({ mode: 'read' });
                savedDirHandle = dirHandle;
                addTerminalOutput(`-- Folder saved: ${dirHandle.name}\n`, 'success');
            }

            await loadFromFolder(dirHandle);
        } else {
            // Fallback for Firefox: use webkitdirectory input
            document.getElementById('folder-input').click();
        }
    } catch (error) {
        if (error.name !== 'AbortError') {
            updateStatus('error', `Failed to access folder: ${error.message}`);
            console.error('Folder access error:', error);
        }
    }
}

async function handleFolderInputChange(event) {
    const files = event.target.files;
    if (!files || files.length === 0) return;

    updateStatus('loading', `Loading ${files.length} files from folder...`);

    let loadedCount = 0;
    for (const file of files) {
        const validExtensions = ['.parquet', '.csv', '.json', '.tsv', '.txt'];
        const isValidFile = validExtensions.some(ext => file.name.toLowerCase().endsWith(ext));

        if (isValidFile) {
            try {
                const arrayBuffer = await file.arrayBuffer();
                const uint8Array = new Uint8Array(arrayBuffer);

                await db.registerFileBuffer(file.name, uint8Array);

                uploadedFiles.push({
                    name: file.name,
                    size: file.size
                });

                addTerminalOutput(`-- File loaded: ${file.name}\n`, 'success');
                loadedCount++;
            } catch (error) {
                addTerminalOutput(`-- Error loading ${file.name}: ${error.message}\n`, 'error');
            }
        }
    }

    renderUploadedFiles();
    updateStatus('success', `Loaded ${loadedCount} Parquet files from folder`);

    // Reset input so the same folder can be selected again
    event.target.value = '';
}

// Expose export functions to window for onclick handlers
window.exportCSV = exportCSV;
window.exportJSON = exportJSON;
window.exportParquet = exportParquet;

// Initialize
document.addEventListener('DOMContentLoaded', () => {
    document.getElementById('file-input').addEventListener('change', handleFileUpload);
    document.getElementById('folder-input').addEventListener('change', handleFolderInputChange);
    document.getElementById('folder-button').addEventListener('click', handleFolderSelect);
    initDuckDB();
    terminalInput.focus();
});
</script>
{{< /rawhtml >}}

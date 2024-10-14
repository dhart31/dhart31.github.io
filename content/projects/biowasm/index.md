+++
title = "Identifying unique amplicon sequences with Biowasm"
+++

This is a simple reference-based mapping and duplicate removal pipeline that works entirely in the browser via [Biowasm](https://biowasm.com/). Handy for small runs. You can check out source code [here](https://github.com/dhart31/dhart31.github.io/blob/main/content/projects/biowasm/index.md?plain=1).

It performs the following steps:
1. Trim and merge paired reads with [fastp](https://github.com/OpenGene/fastp).
2. Map merged reads to reference with [minimap2](https://lh3.github.io/minimap2/minimap2.html).
3. Remove duplicates with [samtools markdup](http://www.htslib.org/doc/samtools-markdup.html).
4. Report mapping and duplicate removal results with [samtools flagstat](http://www.htslib.org/doc/samtools-flagstat.html).
5. Return unique sequences with samtools.

<!-- Add your biowasm script inside raw HTML -->
{{< rawhtml >}}

<style>
#btn, #download_btn {
    background-color: #d3d3d3; /* Green */
    color: black; /* White text */
    border: 2px solid; /* 2px wide, solid border */
    border-color: black; /* Black color */
    border-radius: 5px; /* Rounded edges with a radius of 10px */
    padding: 5px
}
#fastp_output,
#minimap2_output,
#markdup_output,
#output {
    background-color: #333; /* Dark background */
    color: #fff; /* Light text */
    font-family: monospace; /* Monospace font */
    padding: 20px; /* Padding inside the container */
    border-radius: 5px; /* Rounded corners */
    border: 1px solid #555; /* Slight border for depth */
    overflow: auto; /* In case of overflow */
    white-space: pre-wrap; /* Keeps the formatting of preformatted text */
    font-size: 11px;
}
</style>

<script src="https://biowasm.com/cdn/v3/aioli.js"></script>
<script type="module">
const CLI = await new Aioli(["fastp/0.20.1","minimap2/2.22","samtools/1.17", "gawk/5.1.0"]);

let globalOutputData = null;

// Function to launch samtools
async function run() {
	// CLI.mount returns the absolute path of each file mounted
	const files = document.getElementById("myfile").files;
    const ref = document.getElementById("myref").files
	const paths = await CLI.mount(files);
    const ref_path = await CLI.mount(ref);

	// Perform trimming
	fastp_output = await CLI.exec(`fastp -i ${paths[0]} --interleaved_in -m --merged_out output.fastq.gz`);
    document.getElementById("fastp_output").innerHTML = fastp_output;

    // Perform alignment and duplicate removal
	await CLI.exec(`minimap2 -a ${ref_path[0]} output.fastq.gz -o alignment.sam -v 3`);
    await CLI.exec(`samtools sort alignment.sam -o alignment.bam`)
    await CLI.exec(`samtools markdup alignment.bam markdup.bam`)
    markdup_output = await CLI.exec(`samtools flagstat markdup.bam`)
    document.getElementById("markdup_output").innerHTML = markdup_output;

    // Return unique sequences
    await CLI.exec(`samtools index markdup.bam`)
    await CLI.exec(`samtools view -F 1024 -h markdup.bam -o output.sam`)
    output = await CLI.exec("gawk",['/^@/ {next} {print ">"$1"\\n"$10}', "output.sam"])
    globalOutputData = await CLI.exec("samtools view -h output.sam");
    document.getElementById("output").innerHTML = output;

}
// Run samtools when the user clicks the "Run" button
document.getElementById("btn").addEventListener("click", run);

async function download(){
    // Check if globalOutputData has been set
    if (globalOutputData === null) {
        console.error("Data not ready for download.");
        return;
    }

    // Assuming 'output' contains the data you want to download
    const blob = new Blob([globalOutputData], { type: 'text/plain' });
    const href = URL.createObjectURL(blob);
    const link = document.createElement('a');
    link.href = href;
    link.download = "output.sam";
    document.body.appendChild(link);
    link.click();
    document.body.removeChild(link);
    URL.revokeObjectURL(href);
}
document.getElementById("download_btn").addEventListener("click",download)

</script>

<p>Upload FASTQ reads: <input id="myfile" type="file"></p>
<p>Upload FASTA reference: <input id="myref" type="file"></p>
<p><button id="btn">Find unique sequences</button></p>
<p><button id="download_btn">Download unique sequences</button></p>
<h4>Trimming results:</h4>
<pre id="fastp_output"></pre>
<h4>Mapping and duplicate removal results:</h4>
<pre id="markdup_output"></pre>
<h4>Unique Sequences:</h4>
<pre id="output"></pre>

{{< /rawhtml >}}

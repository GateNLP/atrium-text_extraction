# ATRIUM PDF Text Extraction

Converts PDFs into the ATRIUM JSON format described below:
```
#########################################################
# T4.1.2 PDF report text extraction -
# suggested JSON output per PDF report.
# Reports may be represented by separate JSON files, 
# or as separate records in a JSONL format file.
# Note - we don't need to include text for individual 
# identified sections as we have full text plus start/end 
# character positions of these sections
#########################################################
{
	"meta": {
		(any metadata about the source document)
	},
	"text": (full text contents of the document),
	"sections": [
		{ 
			"start": (number),	<-- character position
			"end": (number),	<-- character position
			"type": (string) 	<-- e.g. "title", "subtitle", "abstract", "conclusions", "references" etc.
		}
	]
	
}
```

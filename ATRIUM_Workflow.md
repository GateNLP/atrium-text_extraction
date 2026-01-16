# Text Extraction from PDFs

## Description
This workflow describes the process for extracting the textual content of PDF files, and performing some basic segmentation of the extracted text.

The workflow is intended to be used as the first step in larger workflows that process the text (such as geographic named entitiy extraction etc,) and is unlikely to be particularly useful as a standalone workflow.


## Contributors
Contributors to the design of the workflow include Mark A. Greenwood (USFD), Diana Maynard (USFD), Douglas Tudhope (USW), and Ceri Binding (USW). The implementation was completed by Mark A. Greenwood. 


## Requirements
- The workflow must be able to handle a wide variety of PDF files, including those produced via scanning paper documents as well as those that were _born digital_
- OCR techniques have improved considerably since many older PDFs were produced via scanning paper documents, and so optionally we should be able to re-generate the text through more modern OCR techniques.
- Output shouold be in a well defined/documented format that can be easily ingested via other tools for further processing.

## Workflow Steps

The workflow is implemented in Python with a simple CLI. Full details on installing and using the workflow are beyond the scope of this description but can be found along with the code in [this GitHub repository](https://github.com/GateNLP/atrium-text_extraction).

The high-level outline of the workflow is as follows:

1. __If requested re-run OCR on the PDF file.__ The workflow uses [OCRmyPDF](https://ocrmypdf.readthedocs.io/en/latest/index.html) for this step which means the OCR itself is carried out by [Tesseract](https://github.com/tesseract-ocr/tesseract).
2. __Extract the text from the PDF.__ Extraction is carried out using the Python module [pypdf](https://pypdf.readthedocs.io/en/latest/).
3. __Perform basic segmentation.__ Information about pages within the PDF come direct from the pypdf library. Currently the workflow also marks the end matter (bibliography and appendicies etc.) if it can
be detected.
4. __Export the extracted text and metadata into a JSON file.__ The output JSON file follows the following format

```
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

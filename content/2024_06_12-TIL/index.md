+++
title = "TIL 2024-03-11: Tesseract OCR output formats"
date = 2024-03-11
draft = false
[taxonomies]
tags = ["Tesseract", "NLP", "data", "formats", "OCR"]
+++

[Tesseract](https://github.com/madmaze/pytesseract) allows for various output formats for the analysis. Some are well-known formats like `txt`, `tsv` and `pdf`. Others are specialised in OCR analyses such as "Analyzed Layout and Text Object" (ALTO) and hOCR.
The PAGE format was mentioned on [the manual page](https://github.com/tesseract-ocr/tesseract/blob/main/doc/tesseract.1.asc) but Homebrew's Tesseract version doesn't seem equipped with that option.

# Analyzed Layout and Text Object (ALTO)
[ALTO](https://academic.oup.com/dsh/article/18/1/77/1047620?login=true) is based on an XML schema and details metadata about the layout and contents of physical text resources and is an extension of the Metadata Encoding and Transmission Schema for digital libraries. 

Its development started during the Metadata Engine Project (2002) due to the need to store metadata about digital library text positioning. At the time, there was no standard for this kind of data.

The file I've got from analysing some pages with Tesseract didn't contain the `<Styles>` section.
Only the `<Description>` and `<Layout>` sections were filled. 

In the `<Description>` section I got some metadata about the source data, the OCR processing, and the analysis results. Nothing too fancy.

```XML
[...]
<Description>
	<MeasurementUnit>pixel</MeasurementUnit>

	<sourceImageInformation>
	<fileName>data/totally_legally_acquired_document_name/page10.jpg</fileName>
	</sourceImageInformation>

	<OCRProcessing ID="OCR_0">
		<ocrProcessingStep>
			<processingSoftware>
				<softwareName>tesseract 5.3.4</softwareName>
			</processingSoftware>
		</ocrProcessingStep>
	</OCRProcessing>
</Description>
[...]
```

The `<Layout>` section contains the text layout metadata as the name suggests.

# hOCR
[hOCR](https://ieeexplore.ieee.org/document/4377078) was born due to the necessity of having a single format to represent intermediate and final OCR results.
At its basis, there are the XHTML and CSS formats. The OCR information is added using `<div>`s and `<span>`s becoming potentially invisible when a browser renders the result.

```HTML
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
"http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">

<html xmlns="http://www.w3.org/1999/xhtml" xml:lang="en" lang="en">
<head>
	<title></title>
	<meta http-equiv="Content-Type" content="text/html;charset=utf-8"/>
	<meta name='ocr-system' content='tesseract 5.3.4' />
	<meta name='ocr-capabilities' content='ocr_page ocr_carea ocr_par ocr_line ocrx_word ocrp_wconf'/>
</head>

<body>
	<div class='ocr_page' id='page_1' title='image "data/totally_legally_acquired_document_name/page10.jpg"; bbox 0 0 2466 3639; ppageno 0; scan_res 70 70'>
	[...]
	</div>
</body>
</html>
```

Thanks to its foundations being well-established web technologies, displaying the analysis output is quite painless thanks to projects like [hocrjs](https://github.com/kba/hocrjs).
You can put this tag (`<script src="https://unpkg.com/hocrjs"></script>`) at the end of the document body and display the file by opening it with a web browser.
Voilà, now the browser will show you the document structure obtained from Tesseract!

Thanks to hocrjs I discovered [Tampermonkey](https://www.tampermonkey.net/index.php) however I was unable to get it to work after loading the userscript. 

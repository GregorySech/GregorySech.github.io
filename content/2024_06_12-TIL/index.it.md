+++
title = "TIL 2024-03-11: Formati di output di Tesseract OCR"
date = 2024-03-11
draft = false
[taxonomies]
tags = ["Tesseract", "NLP", "data", "formats", "OCR"]
+++

[Tesseract](https://github.com/madmaze/pytesseract) permette di salvare i risultati delle proprie analisi in vari formati. Alcuni sono formati d'uso comune come `txt`, `tsv` and `pdf`. Altri sono specializzati per le analisi OCR come "Analyzed Layout and Text Object" (ALTO) ed hOCR.
Anche il formato PAGE è menzionato in questa [pagina del manuale](https://github.com/tesseract-ocr/tesseract/blob/main/doc/tesseract.1.asc) ma la versione di Tesseract ottenibile tramite Homebrew's non sembra supportare l'opzione.

# Analyzed Layout and Text Object (ALTO)
[ALTO](https://academic.oup.com/dsh/article/18/1/77/1047620?login=true) è basato su uno schema XML e descrive i metadati riguardanti il layout ed il contenuto di testo su supporti fisici. Questo formato è un'estensione del  Metadata Encoding and Transmission Schema per librerie digitali. 

Il suo sviluppo iniziò nel 2002 durante il Metadata Engine Project per via della necessità di salvare metadati riguardo al posizionamento del testo all'interno degli scritti presenti in una libreria digitale. Al tempo non c'erano standard per questo tipo di dati.

Il file che ho analizzato con Tesseract non contiene la sezione `<Styles>`. Solo `<Description>` e `<Layout>` sono presenti.

Nella sezione `<Description>` sono presenti alcuni metadati sui dati analizzati, sul processo di OCR ed sui risultati dell'analisi.

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

`<Layout>` contiene appunto la descrizione del layout del testo.

# hOCR
[hOCR](https://ieeexplore.ieee.org/document/4377078) nasce per cercare di avere un singolo formato per rappresentare i risultati di un'analisi OCR sia nella fase intermedia che in quella finale. Quindi non solo sapere il testo contenuto nell'immagine ma anche informazioni di layout. 
Si basa sui formati XHTML e CSS. L'informazione OCR viene aggiunta ad HTML tramite i tag `<div>` e `<span>` il che la rende invisibile al rendering dei web-browser.  

Segue un esempio di un output hOCR.

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

Grazie alla scelta di usare come fondamento di questo formato tecnologie web ben conosciute, visualizzare i risultati degli OCR diventa molto facile grazie a progetti come [hocrjs](https://github.com/kba/hocrjs).

Si può inserire un tag particolare (`<script src="https://unpkg.com/hocrjs"></script>`) alla fine del "body" del documento prima di aprirlo tramite browser e
voilà, ora possiamo visualizzare la struttura del documento ottenuta da Tesseract!

Grazie ad hocrjs ho scoperto [Tampermonkey](https://www.tampermonkey.net/index.php) però non sono riuscito ad usarlo per aggiungere il tag direttamente nel browser nonostante abbia correttamente caricato l'userscript che descrivono.

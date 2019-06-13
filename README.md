TCPDI
=====

Composer ready [TCPDI](https://github.com/pauln/tcpdi).

PDF importer for [TCPDF](http://www.tcpdf.org/), based on [FPDI](http://www.setasign.de/products/pdf-php-solutions/fpdi/).
Requires [pauln/tcpdi_parser](https://github.com/pauln/tcpdi_parser) and [FPDF_TPL](http://www.setasign.de/products/pdf-php-solutions/fpdi/downloads/)
which included in the repository.

Installation
------------

Link package in composer.json, e.g.

```json
{
    "require": {
        "mrpamacs/tcpdi": "dev-master"
    }
}
```

Usage
-----

Usage is essentially the same as FPDI, except importing TCPDI rather than FPDI.  It also has a "setSourceData()" function which accepts raw PDF data, for cases where the file does not reside on disk or is not readable by TCPDI.

```php
// Create new PDF document.
$pdf = new TCPDI(PDF_PAGE_ORIENTATION, PDF_UNIT, PDF_PAGE_FORMAT, true, 'UTF-8', false);

// Add a page from a PDF by file path.
$pdf->AddPage();
$pdf->setSourceFile('/path/to/file-to-import.pdf');
$idx = $pdf->importPage(1);
$pdf->useTemplate($idx);

$pdfdata = file_get_contents('/path/to/other-file.pdf'); // Simulate only having raw data available.
$pagecount = $pdf->setSourceData($pdfdata); 
for ($i = 1; $i <= $pagecount; $i++) { 
    $tplidx = $pdf->importPage($i);
    $pdf->AddPage();
    $pdf->useTemplate($tplidx); 
}
```

TCPDI_PARSER
============

Parser for use with TCPDI, based on TCPDF_PARSER.  Supports PDFs up to v1.7.

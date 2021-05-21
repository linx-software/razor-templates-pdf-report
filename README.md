# Razor Templates Examples including PDF Reports
This is a collection of example on how to use Razor Templates in Linx. This also inludes how to generate PDF Reports in Linx using HTML templates and a small command-line tool called "wkhtmltopdf"

## Overview

Razor templates are a really easy way to create text-based models and populate them with data. It's really helpful with anything HTML, but can be used on normal text as well. In this sample there are 4 different ways to use Razor templates to create text using a template and models. Additionally, an example on how to create PDF reports. A very helpful feature of any system is to be able to automatically generate reports and forward it to users, either via Email, or on a site for download. There are a lot of technologies available for large report generation, i.e. SQL Reporting Services, Knowage, Crystal Reports etc. But they are mostly targeting large setups, and sometimes you just want a quick report without the hassle.

Although Linx, by itself cannot create PDFs, with the help of some other tools, it’s really simple.

## How to use this sample

Using Linx Designer, open the solution file "PDFReportWithHTMLTemplate.lsoz", configure your settings as below, and Debug the function called "RunReport".

## Additional resources

- Download Linx at https://linx.software
- Download wkhtmltopdf at https://wkhtmltopdf.org/

## Dependencies

- Linx Designer 5.20 or newer
- wkhtmltopdf

## Settings

- Path to "wkhtmltopdf.exe" - wkhtmltopdfpath. Example: "C:\Program Files\wkhtmltopdf\bin\wkhtmltopdf.exe"
- Path to location to save example files - PathToSaveExampleFiles. Example: "C:\temp\" 

## Description

This example includes a small Linx Solution that:

- Show 4 different ways to use Models and Templates to Create text. Under the folder "RazorExamples"
- Uses data in a understandable structure
- With Razor Templates, generates text and HTML files
- Which then can be converted to a PDF file using a tool called wkhtmltopdf (https://wkhtmltopdf.org/ 4) You’ll need to download and install this to run this sample.

### Data Structure

For the Razor Examples, a Models folder with types for each sample.

For the PDF Reports, I’ve created a Type in Linx called “Report” which consists of some Report data, i.e. Report Name, Author, Date and Version. It also contains another Type called “Rows”. Each “Row” is split up into “Columns” which contains a “Value”. Please view the file "Datastructure.png" as an example representation of this.

### Functions

In the "RazorExamples" folder, the following functions are available:
- **A1_SimpleModel**: Shows how to create a text file using a simple model
- **A2_MoreComplexListModel**: Shows how to create a more complicated text file with a model containing a List
- **B1_SimpleHTML**: Shows how to create a simple HTML file using a simple model
- **B2_EmailTemplate**: Shows how to create a nicely formatted Email HTML using a complex data model with a List

In the "RazorPDFReport" folder, the following functions were built to build a basic report:

- **CleanUpData:** This first function simply takes the Report Data given and makes sure that each of the Rows has the same amount of Columns. That is important because the Report Generation will fail if they are not the same.
- **FormatReport:** Using Razor Templates and some really simple HTML, the Report Data is used to generate and HTML page for the report. Being HTML one can make use of CSS to give the Report really good aesthetics, or keep it simple like in this example.
- **HtmlToPDF:** This function then uses the wkhtmltopdf EXE file to convert the HTML to PDF. https://wkhtmltopdf.org/downloads.html

### Example Template:

For the PDF Report, Here’s the Razor Template. You can use any CSS or HTML:

```
<html>
<body>
<h1>@Model.ReportName</h1>
<h3>By: @Model.ReportAuthor</h2>
<h3>Date: @Model.ReportDate</h3>
<h3>Verion: @Model.ReportVersion</h3>
<hr>
<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  overflow:hidden;padding:10px 5px;word-break:normal;}
.tg th{border-color:black;border-style:solid;border-width:1px;font-family:Arial, sans-serif;font-size:14px;
  font-weight:normal;overflow:hidden;padding:10px 5px;word-break:normal;}
.tg .tg-0lax{text-align:left;vertical-align:top}
</style>
<table class="tg">
<thead>
  <tr>
    @for(var i = 0; i < @Model.Rows.RowOfColumns[0].Values.Count; i++)
	{
		<th class="tg-0lax">@Model.Rows.RowOfColumns[0].Values[i]</th>
	}
  </tr>
</thead>
<tbody>
 @for(var i = 1; i < @Model.Rows.RowOfColumns.Count; i++)
	{
		 <tr>
		 @for(var j = 0; j < @Model.Rows.RowOfColumns[i].Values.Count; j++)
			{
				<td class="tg-0lax">@Model.Rows.RowOfColumns[i].Values[j]</td>
			}
		 </tr>
	}
</tbody>
</table>
</body>
</html>
```

**HARDCODE WARNING** - This is just an Example Solution, so I’ve Hardcoded the file paths and Report Data. You can change this in any way you need.

### Example Report

The above HTML will produce a report like the included "ExampleReport.pdf"



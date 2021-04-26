# PDF-Reports
Generate PDF Reports in Linx using HTML templates and a small command-line tool called "wkhtmltopdf"

## Overview

A very helpful feature of any system is to be able to automatically generate reports and forward it to users, either via Email, or on a site for download. There are a lot of technologies available for large report generation, i.e. SQL Reporting Services, Knowage, Crystal Reports etc. But they are mostly targeting large setups, and sometimes you just want a quick report without the hassle.

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

## Description

In this example I’ve created a small Linx Solution that:

- Uses data in a understandable structure
- With Razor Templates, generates an HTML file
- Which then can be converted to a PDF file using a tool called wkhtmltopdf (https://wkhtmltopdf.org/ 4) You’ll need to download and install this to run this sample.

### Data Structure

I’ve created a Type in Linx called “Report” which consists of some Report data, i.e. Report Name, Author, Date and Version. It also contains another Type called “Rows”. Each “Row” is split up into “Columns” which contains a “Value”. Please view the file "Datastructure.png" as an example representation of this.

### Functions

The following functions were built to build a basic report:

- **CleanUpData:** This first function simply takes the Report Data given and makes sure that each of the Rows has the same amount of Columns. That is important because the Report Generation will fail if they are not the same.
- **FormatReport:** Using Razor Templates and some really simple HTML, the Report Data is used to generate and HTML page for the report. Being HTML one can make use of CSS to give the Report really good aesthetics, or keep it simple like in this example.
- **HtmlToPDF:** This function then uses the wkhtmltopdf EXE file to convert the HTML to PDF. https://wkhtmltopdf.org/downloads.html

### Example Template:

Here’s the Razor Template. You can use any CSS or HTML:

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



# docx-embeddedhtml-injection
This PowerShell script injects arbitrary HTML code into a docx file, replacing the value of a pre-existing embeddedHtml tag.

Researchers at Cymulate [found a vulnerability in Microsoft Word documents with an embedded video player](https://blog.cymulate.com/abusing-microsoft-office-online-video). This vulnerability lets anyone inject HTML code in place of the expected Youtube iframe.

The process to inject the HTML code can be somewhat tedious. This script attempts to automate this process.

## How to use

This script was made using PowerShell 5.1

Here's how the function works :
```powershell
Inject-Docx -Path "C:\This\Is\A\test.docx" -HtmlBlock "<h3>TEST</h3>" -DestinationName "destination.docx"
```
-Path being the path of the original document.

-HtmlBlock being the HTML block to be injected.

-DestinationName being the file name of the final document. This parameter is optional (default is "output.docx")

## Mitigation

Currently, the only way to mitigate this vulnerability is to block Word documents containing embedded video. Microsoft has not acknowledged this as being a vulnerability, and seem to have no plan to fix it. Here is the official response from Jeff Jones, senior director at Microsoft :

>“The product is properly interpreting html as designed — working in the same manner as similar products.”

[Source](https://www.scmagazine.com/home/security-news/researchers-report-vulnerability-in-microsoft-words-online-video-feature/)


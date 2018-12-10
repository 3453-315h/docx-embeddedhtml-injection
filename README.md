# docx-embeddedhtml-injection
Researchers at Cymulate [found a vulnerability in Microsoft Word documents with an embedded video player](https://blog.cymulate.com/abusing-microsoft-office-online-video). This vulnerability lets anyone inject HTML code in place of the expected Youtube iframe.

This PowerShell script exploits this known vulnerability in documents with embedded online videos by injecting them with HTML code, replacing the values of all pre-existing embeddedHtml tags. Microsoft Word will execute any HTML you inject, here's an example :

![xml_docx_example](https://user-images.githubusercontent.com/45467550/49740658-b9437300-fc62-11e8-9d29-9618777b90fe.PNG)

The process to inject the HTML code can be somewhat tedious. This script attempts to automate this process.

## How to use
### Prerequisites

You will need a Word document with at least one or more online videos. To add an online video in a Word document, simply go to **Insert > Online Video** and search for a video. If you have any issues, refer to the [official Microsoft documentation](https://support.office.com/en-us/article/video-insert-online-video-bf11b812-0243-4f53-a1f9-432fbf7ace2c).

This script was made using PowerShell 5.1, so you will need PowerShell version 5.1 or a newer version.

To use this function in the PowerShell terminal, you can simply [dot source](https://ss64.com/ps/source.html) it from the terminal :

```
PS C:\> . C:\scripts\docx-embedded-html.ps1

PS C:\> Inject-Docx -Path "C:\This\Is\A\test.docx" -HtmlBlock "<h3>Test</h3>"
```

To use this function in a script, you will need to dot source it in the script :
```powershell
. C:\scripts\docx-embedded-hmtl.ps1
```

### Function
Here's how the function works :
```powershell
Inject-Docx -Path "C:\This\Is\A\test.docx" -HtmlBlock "<h3>Test</h3>" -DestinationName "destination.docx"
```
`-Path` being the path of the original document.

`-HtmlBlock` being the HTML block to be injected.

`-DestinationName` being the file name of the final document. This parameter is optional (default is "output.docx")

## Vulnerability mitigation

Currently, the only way to mitigate this vulnerability is to block Word documents containing embedded video. Microsoft has not acknowledged this as being a vulnerability, and seem to have no plan to fix it. Here is the official response from Jeff Jones, senior director at Microsoft :

>“The product is properly interpreting html as designed — working in the same manner as similar products.”

[Source](https://www.scmagazine.com/home/security-news/researchers-report-vulnerability-in-microsoft-words-online-video-feature/)


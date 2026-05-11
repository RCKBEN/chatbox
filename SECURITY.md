# Security Policy

## Supported Versions

Use this section to tell people about which versions of your project are
currently being supported with security updates.

| Version | Supported          |
| ------- | ------------------ |
| 5.1.x   | :white_check_mark: |
| 5.0.x   | :x:                |
| 4.0.x   | :white_check_mark: |
| < 4.0   | :x:                |

## Reporting a Vulnerability

Use this section to tell people how to report a vulnerability.

Tell them where to go, how often they can expect to get an update on a
reported vulnerability, what to expect if the vulnerability is accepted or
declined, etc.
Google Git
Sign in
chromium/chromium/src/main/./chrome/updater/tools/file_inspector/file_inspector.html
blob: 6b0708728ae01f33b4c8925f7afbca561660b009 [file]
<!doctype html>
<!--
  File inspector is a simple tool for understanding the contents of various
  updater-related binary files, such as ZIP files or zucchini patch files.
 -->
<html>
  <head>
    <title>File Inspector</title>
    <meta charset="utf-8"></meta>
    <style>
      body {
        margin: 0;
        padding: 0;
        display: flex;
        flex-direction: column;
        font-family: sans-serif;
      }
      #help {
        padding: 1em;
      }
      #hexdump {
        max-width: 27.5em;
        overflow-wrap: break-word;
        font-family: monospace;
      }
      #hexdump > span > span {
        margin-left: 0.25em;
        margin-right: 0.25em;
      }
      #json {
        white-space: pre;
      }
      #output {
        display: flex;
        gap: 2em;
        align-items: flex-start;
      }
      #output > div {
        position: sticky;
        top: 0;
      }
    </style>
    <script src="insight-box.js" type="module"></script>
    <script src="parser.js" type="module"></script>
  </head>
  <body>
    <div id="controls">
      <label><input type="file" id="file"></input></label>
      <label>File Type:
        <select id="filetype">
          <option value="zip">ZIP Archive</option>
          <option value="zucc">Zucchini Patch File</option>
        </select>
      </label>
    </div>
    <div id="output">
      <div id="hexdump"></div>
      <div id="json"></div>
      <div id="findings"></div>
    </div>
    <div id="help">
    </div>
    <script type="module">
      import {render} from "./parser.js";
      document.getElementById("file").addEventListener("change", () => {
        const hexdump = document.getElementById("hexdump");
        const json = document.getElementById("json");
        const findings = document.getElementById("findings");
        hexdump.innerHTML = "Loading file...";
        json.innerHTML = "";
        findings.innerHTML = "";
        const reader = new FileReader();
        reader.addEventListener("loadend", () => {
          hexdump.innerHTML = "";
          render(
            new DataView(reader.result),
            document.getElementById("filetype").value,
            hexdump,
            json,
            findings);
          });
        reader.readAsArrayBuffer(document.getElementById("file").files[0]);
      });
    </script>
  </body>
</html>
Powered by Gitiles| Privacy| Terms
txt
json

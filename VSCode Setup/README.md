# Visual Studio Code configuraiton

1. Install Visual Studio Code Appliation (VS Code)
2. Install VSCode Plugins (Code Runner, HTML, CSV Excel, Markdown, PDF)
3. Configure Code Runner to run 'b4p' code by adding b4p extension to settings file


## VS Code Application
https://code.visualstudio.com/


## VS Code Runner

__Code Runner__
* https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner
* See vs-code-settings.json file for settings;  pertinent sections are below:

``` text
    "code-runner.executorMap": {
        "b4p": "b4p",
        .
        .
        .
    "code-runner.executorMapByFileExtension": {
         ".b4p": "b4p",
        .
        .
        .
   "code-runner.languageIdToFileExtensionMap": {
        "b4p": ".b4p",
         
```

## VS File Viewers
__HTML viewers__
* https://marketplace.visualstudio.com/items?itemName=ecmel.vscode-html-css
* https://marketplace.visualstudio.com/items?itemName=qinjia.view-in-browser

__CSV viewer__
* https://marketplace.visualstudio.com/items?itemName=RandomFractalsInc.vscode-data-preview

__Excel viewer__
* https://marketplace.visualstudio.com/items?itemName=GrapeCity.gc-excelviewer

__JSON viewer__
* https://marketplace.visualstudio.com/items?itemName=ZainChen.json
* https://marketplace.visualstudio.com/items?itemName=nickdemayo.vscode-json-editor

__Markdown viewer__
* https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced

__PDF viewer__
* https://marketplace.visualstudio.com/items?itemName=tomoki1207.pdf

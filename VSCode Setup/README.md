# Visual Studio Code configuraiton

1. Install Visual Studio Code Appliation (VS Code)
2. Enable launch from command line
3. Install VSCode Plugins (Code Runner, HTML, CSV Excel, Markdown, PDF)
4. Configure Code Runner to run 'b4p' code by adding b4p extension to settings file

## VS Code Installer
https://code.visualstudio.com/


## Enable launch from command line
* https://code.visualstudio.com/docs/setup/mac
* Launch VS Code.
* Open the Command Palette (Cmd+Shift+P) and type 'shell command' to find the Shell Command: Install 'code' command in PATH command.
* Restart the terminal for the new $PATH value to take effect. You'll be able to type 'code .' in any folder to start editing files in that folder.


## VS Code Runner

__Code Runner__
* https://marketplace.visualstudio.com/items?itemName=formulahendry.code-runner

__Settings File__
*  ~/Library/Application Support/Code/User
* vs-code-settings.json file for full file
* Pertinent sections:


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


## Optional Plugins
* https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker
* https://marketplace.visualstudio.com/items?itemName=GrapeCity.gc-excelviewer
* https://marketplace.visualstudio.com/items?itemName=tht13.html-preview-vscode
* https://marketplace.visualstudio.com/items?itemName=ZainChen.json
* https://marketplace.visualstudio.com/items?itemName=nickdemayo.vscode-json-editor
* https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter
* https://marketplace.visualstudio.com/items?itemName=shd101wyy.markdown-preview-enhanced
* https://marketplace.visualstudio.com/items?itemName=mongodb.mongodb-vscode
* https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers
* https://marketplace.visualstudio.com/items?itemName=qinjia.view-in-browser
* https://marketplace.visualstudio.com/items?itemName=tomoki1207.pdf
* https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools
* https://marketplace.visualstudio.com/items?itemName=ms-python.vscode-pylance
* https://marketplace.visualstudio.com/items?itemName=ms-python.python


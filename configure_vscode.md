# Configure VSCode
It is common practice to develop Odoo modules in a separate directory/workspace from the rest of the code. 
However, the path to odoo must be configured so that no errors (or squiggly lines are shown). To do this, several settings must be adjusted. 

## Add odoo as extra path
In the `.vscode/settings.json` file, add the path to Odoo in the `python.analysis.extraPaths` list. E.g.:
```json
"python.analysis.extraPaths": [
    "~/odoo/versions/<version_number>/odoo"
]
```

## Add final new line
Odoo coding guidelines suggest adding an empty line at the end of each file. This behavior can be configured on vscode in the `files.insertFinalNewline` attribute. E.g.:
```json
"files.insertFinalNewline": true
```

## Useful links
https://www.odoo.com/es_ES/forum/ayuda-1/how-to-properly-import-odoo-in-visualstudio-code-151327

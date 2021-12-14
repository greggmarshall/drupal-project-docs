# VS Code Extensions and Configurations

There are a number of VS Code Extensions to consider installing to make Drupal development more efficient and convenient.

## Microsoft Extensions for Remote Editing

**Remote - Containers**, ms-vscode-remote.remote-containers. Open any folder or repository inside a Docker container and take advantage of Visual Studio Code's full feature set.

**Remote - SSH**, ms-vscode-remote.remote-ssh. Open any folder on a remote machine using SSH and take advantage of VS Code's full feature set.

**Remote - SSH: Editing Configuration Files**, ms-vscode-remote.remote-ssh-edit. This extension complements the Remote - SSH extension with syntax colorization, keyword intellisense, and simple snippets when editing SSH configuration files.

**Remote - WSL**, ms-vscode-remote.remote-wsl. Open any folder in the Windows Subsystem for Linux (WSL) and take advantage of Visual Studio Code's full feature set.

**Remote Development**, ms-vscode-remote.vscode-remote-extensionpack. The Remote Development extension pack allows you to open any folder in a container, on a remote machine, or in the Windows Subsystem for Linux (WSL) and take advantage of VS Code's full feature set.

## Drupal Community Extensions

From <https://www.drupal.org/docs/develop/development-tools/configuring-visual-studio-code>

**phpcs**, ikappas.phpcs. PHP CodeSniffer for Visual Studio Code. Requires PHPCS be installed in project or globally.

**phpcbf**, persoderlind.vscode-phpcbf. PHP Code Beautifier and Fixer. PHPCBF must be installed. PHPCBF is installed when you install PHPCS.

**Debugger for Chrome**, msjsdiag.debugger-for-chrome. Debug your JavaScript code in the Chrome browser, or any other target that supports the Chrome Debugger protocol.

**PHP DocBlocker**, neilbrayfield.php-docblocker. A simple, dependency free PHP specific DocBlocking package.

**empty-indent**, dmitrydorofeev.empty-indent. Removes indentation in empty lines on save.

**PHP Debug**, felixfbecker.php-debug. Debug support for PHP with XDebug.

## Drupal 8 Recommended Extensions

**Composer**, ikappas.composer. This Visual Studio Code plugin provides an interface to Composer dependency manager for PHP. It also provides schema validation for composer.json configuration files..

**Twig Language 2**, mblode.twig-language-2. Snippets, Syntax Highlighting, Hover, and Formatting for Twig.

**Drupal 8 Snippets,** dssiqueira.drupal-8-snippets. Drupal 8.6.x Snippets.

**Drupal 8 JavaScript Snippets,** tsega.drupal-8-javascript-snippets. Useful Javascript snippets to use with Drupal 8.

**Drupal 8 Twig Snippets**, tsega.drupal-8-twig-snippets. A handful of twig functions to use with Drupal 8.

## Editor Settings

Change this by navigating to the User or Workspace settings page, and clicking the 'Open Settings (JSON)' button in the tab bar.

    {

    "breadcrumbs.enabled": true, "css.validate": true, "diffEditor.ignoreTrimWhitespace": false, "editor.tabSize": 2,

    "editor.autoIndent": true, "editor.insertSpaces": true, "editor.formatOnPaste": true, "editor.formatOnSave": false, "editor.renderWhitespace": "boundary", "editor.wordWrapColumn": 80, "editor.wordWrap": "off", "editor.detectIndentation": true, "editor.rulers": \[

    80

    \],

    "files.associations": { "\*.inc": "php",

    "\*.module": "php",

    "\*.install": "php",

    "\*.theme": "php",

    "\*.profile": "php",

    "\*.tpl.php": "php",

    "\*.test": "php",

    "\*.php": "php",

    "\*.info": "ini"

    },

    "files.trimTrailingWhitespace": true, "files.insertFinalNewline": true, "html.format.enable": true, "html.format.wrapLineLength": 80, "telemetry.enableTelemetry": false,

    /\* Empty Indent \*/ "emptyIndent.removeIndent": true, "emptyIndent.highlightIndent": false,

    "emptyIndent.highlightColor": "rgba(246,36,89,0.6)",

    }

## Configuring XDebug

Visual Studio Code uses "launch" configurations to provide support for debugging as well as other actions. Please read the drupal.org Xdebug debugging documentation page for instructions about configuring XDebug.

To create a launch configuration for XDebug,

1.  Click the Debug menu icon on the left-side (Command/Ctrl-Shift D).

2.  Click the Dropdown menu with "No Configurations" listed in it, and then choose "Add Configuration".

3.  Add the snippet below in the Editor pane titled "launch.json" and save.

4.  The "serverSourceRoot" is optional and used for Remote Debugging.

5.  Click the Play button (green triangle) to start debugger, and go to your local Drupal web site with the XDEBUG\_SESSION\_START=idekey query parameter where idekey is the value you configured in XDebug.


    {

    // Use IntelliSense to learn about possible attributes.

    // Hover to view descriptions of existing attributes.

    // For more information, visit: https://go.microsoft.com/fwlink/?

    linkid=830387 "version": "0.2.0", "configurations": \[

    {

    "name": "Listen for XDebug (DDEV)", "type": "php",

    "request": "launch", "hostname": "0.0.0.0",

    "port": 9000, "pathMappings": {

    "/var/www/html": "${workspaceRoot}"

    }

    }

    \],

    {

    "name": "Listen for XDebug (9003)", "type": "php",

    "request": "launch", "port": 9003,

    "log": true, "pathMappings": {

    "/app/": "${workspaceRoot}/",

    }

    }

    \]

    }

© 2020-2021. This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

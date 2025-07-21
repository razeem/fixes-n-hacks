# VS Code Settings and Extensions

## VS Code Settings
- Map custom extensions to languages, recommended extensions, and settings.
- Example settings:
```json
{
  "files.associations": {
    "*.inc": "php",
    "*.module": "php",
    "*.install": "php",
    "*.theme": "php",
    "*.tpl.php": "php",
    "*.test": "php",
    "*.php": "php",
    "*.info": "ini"
  },
  "editor.tabSize": 2,
  "editor.insertSpaces": true,
  "editor.formatOnPaste": true,
  "editor.formatOnSave": false,
  "files.trimTrailingWhitespace": true,
  "files.insertFinalNewline": true
}
```
- Recommended extensions: Drupal 8 Snippets, Drupal 8 Twig Snippets, JS-CSS-HTML Formatter, PHP Intelephense, Twig, Twig Language 2, YAML

## PHP Indentation
- Install php-cs-fixer:
```
curl -L http://cs.sensiolabs.org/download/php-cs-fixer-v2.phar -o php-cs-fixer
sudo chmod a+x php-cs-fixer
sudo mv php-cs-fixer /usr/local/bin/php-cs-fixer
composer global require friendsofphp/php-cs-fixer
```
- VS Code extension: kokororin.vscode-phpfmt

## PHP Intellisense
- https://marketplace.visualstudio.com/items?itemName=felixfbecker.php-intellisense

## Twig Intellisense
- https://marketplace.visualstudio.com/items?itemName=mblode.twig-language

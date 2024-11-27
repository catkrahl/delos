# SASS cate90
## Guidelines

### PATCH MARKER
* patches mit '//###_cate-skin-patch' markieren und mehrzeilig mit '//###_patch_end' beenden
* patches für den ILIAS-Kern mit //###_skin-core-fix markieren

### Allgemein
* Änderungen nicht direkt im Code der Module, sondern - falls möglich - in der modul/index.scss
* dies klappt nicht, wenn Variablen als Wert eine andere Variable zugewiesen wird (s.Beispiel mainbar-bg-color)

#### MODUL-VARS
* !default-flag im Modul und in cate-base mit anderem Wert überschreiben 

#### colors/color-maps 
* Farben nicht mit einer map in der settings/index (re-)definieren, weil sie dann nicht mehr weiter exposed (cate.scss/customer.scss) werden können

### Beispiel: 

#### mainbar bg color
* $il-mainbar-btn-bg-color-engaged: $il-main-color;
* settings/index änderungen nicht möglich, weil $il-main-color dort nicht bekannt

#### Avatar border-variable
* Überschreibung des Variablenwerts in Customizing/components/symbols ...
* eine Überschreibung in der skin-cate.scss wäre generischer, ist aber nicht möglich wegen des fehlenden !default-flags
* wo das flag setzen? 
* flag in der datei _ui-component_avatar und @forward hat nicht geklappt 

#### mainbar icon-filter
* $il-mainbar-btn-icon-filter
* Überschreibung am Ende der 070-components/index.scss
* unproblematisch bei einem rebase

### QUESTIONS
* wo werden die parameter für die Farbe des dropdown-toggle-button übergeben? -> änderungen zu machen ist schwer bzw. nicht verständlich
* kann ich z.B. eine globale Variable für den border-radius setzen, der auch bei anderen Elementen im Skin sich entsprechend auswirkt? Mit der Parameter-Übergabe am make-button-mixin wirkt sich das ja nicht gleichzeitig für andere Elemente aus, wenn man das möchte
* ui_component_mainbar -> mixin in datei oder in mixins?
* 3 Stellen für typo: settings_typography/normalize_typography/elements_typography
* tabs hover bg-color in _c-toolbar, nicht in _c-tabs

### IMPROVEMENTS
* mixin 030_tools/_tool_border-radius ist repetitiv, top,right,bottom, left sollte ein parameter werden!
* @import ersetzen in -ui-component_maincontrols
* 0px überall entfernen!
* benennung module NUR singl. oder plural

### GIT SUBTREE 

#### add:
git subtree add --prefix Customizing/global/skin/cate git@github.com:conceptsandtraining/delos.git cate90 --squash
* --squash-flag: will NOT store the history of the subtree-repo in th main repository (we SHOULD?)

#### pull: 
git subtree pull --prefix Customizing/global/skin/cate git@github.com:conceptsandtraining/delos.git cate90 master --squash

#### push:
git subtree push --prefix Customizing/global/skin/cate git@github.com:conceptsandtraining/delos.git cate90

# SASS cate90
## Guidelines

### Patch Marker
* patches mit '//###_cate-skin-patch' markieren und mehrzeilig mit '//###_patch_end' beenden
* patches für den ILIAS-Kern mit //###_core-fix markieren

### Allgemein
* Änderungen nicht direkt im Code der Module, sondern - falls möglich - in der modul/index.scss
* dies klappt nicht, wenn Variablen als Wert eine andere Variable zugewiesen wird (s.Beispiel mainbar-bg-color)

#### MODUL-VARS
* !default-flag im Modul und in cate-base mit anderem Wert überschreiben 

#### colors/color-maps 
* Farben nicht mit einer map in der settings/index (re-)definieren, weil sie dann nicht mehr weiter exposed (cate.scss/customer.scss) werden können

### Beispiel: 
#### Typo Nunito/font-weight 
* Überschreibung in der skin-xyz.scss zu redundant
* Änderungen müssten in allen skin-Dateien gemacht werden
* Änderungen in 010-settings/index 

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

#### ERROR2 (siehe 070-components)
* These: Überschreibung von Variablenwerten nicht im Modul selbst, sondern am Ende jeder index.scss
* Vorteil: leicht zu rebasen
* Fehler: 070-components/index.scss -> wenn lokale Variablen globale Variablen enthalten, die an dieser Stellen nicht bekannt sind
* $il-mainbar-btn-border: 0px solid $il-standard-page-border-light-color; ($il-standard-page-border-light-color)
* Idee: Überschreibung am Ende der urspünglichen Datei unter Beibehaltung des Ausgangswerts von ilias

### ???
* wo werden die parameter für die Farbe des dropdown-toggle-button übergeben? -> änderungen zu machen ist schwer bzw. nicht verständlich
* kann ich z.B. eine globale Variable für den border-radius setzen, der auch bei anderen Elementen im Skin sich entsprechend auswirkt? Mit der Parameter-Übergabe am make-button-mixin wirkt sich das ja nicht gleichzeitig für andere Elemente aus, wenn man das möchte
* ui_component_mainbar -> mixin in datei oder in mixins?
* 3 Stellen für typo: settings_typography/normalize_typography/elements_typography
* tabs hover bg-color in _c-toolbar, nicht in _c-tabs

### improvments
* mixin 030_tools/_tool_border-radius ist repetetive, top,right,bottom, left sollte ein parameter werden!

### citations:
"And, if we need, we can always @use and @forward the same module by adding both rules:
@forward 'forms';
@use 'forms';
That’s particularly useful if you want to wrap a library with configuration or any additional tools, before passing it along to your other files."
(https://css-tricks.com/introducing-sass-modules/)

git subtree push:
git subtree push --prefix=Customizing/global/skin/cate git@github.com:conceptsandtraining/delos.git cate90

# SASS cate90
## Guidelines

### Patch Marker
* patches mit '//###_cate-skin-patch' markieren und mehrzeilig mit '//###_patch_end' beenden

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
* ui_component_mainbar -> mixin in datei oder in mixins?
* 3 Stellen für typo: settings_typography/normalize_typography/elements_typography

### citations:
"And, if we need, we can always @use and @forward the same module by adding both rules:
@forward 'forms';
@use 'forms';
That’s particularly useful if you want to wrap a library with configuration or any additional tools, before passing it along to your other files."
(https://css-tricks.com/introducing-sass-modules/)
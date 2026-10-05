# Lab Writeup: Reflected XSS (Event Handlers & href Blocked)

- Tento dokument slouží jako studijní materiál a záznam z PortSwigger Web Security Academy
- **Lab Name:** Reflected XSS with event handlers and href attributes blocked 

# Popis útoku
Aplikace reflektovala uživatelský vstup zpět do HTML těla stránky, ale obsahovala bezpečnostní filtry, které blokovaly běžné spouštěče (event handery jako `onload`/`onclick` a `href` atributy). 

# Proč to fungovalo?
Využitím specifického payloadu z nápovědy, který obešel zavedené filtry (např. alternativním tagem nebo jinou strukturou HTML), došlo k úspěšnému provedení skriptu v kontextu prohlížeče a okamžitému vyřešení labu.

## Použitý payload:
> **Pozor:** Místo `YOUR-LAB-ID` si v URL adrese dosaď své vlastní ID aktivního labu z PortSwiggeru.

```text
[https://YOUR-LAB-ID.web-security-academy.net/?search=%3Csvg%3E%3Ca%3E%3Canimate+attributeName%3Dhref+values%3Djavascript%3Aalert(1)+%2F%3E%3Ctext+x%3D20+y%3D20%3EClick+me%3C%2Ftext%3E%3C%2Fa%3E](https://YOUR-LAB-ID.web-security-academy.net/?search=%3Csvg%3E%3Ca%3E%3Canimate+attributeName%3Dhref+values%3Djavascript%3Aalert(1)+%2F%3E%3Ctext+x%3D20+y%3D20%3EClick+me%3C%2Ftext%3E%3C%2Fa%3E)
 
#Postup řešení

Analýza zadání a filtrů: Zjistil jsem, že aplikace je zranitelná vůči Reflected XSS, ale obsahuje bezpečnostní filtry, které blokují obvyklé spouštěče (event handery jako onclick/onload a href atributy).

Využití nápovědy: Prozkoumal jsem nápovědu labu, abych našel alternativní HTML tag nebo atribut, který filtry přehlížejí a neblokují.

Nasazení payloadu: Vzal jsem specifický payload z nápovědy a vložil ho do URL adresy / vstupního pole aplikace.

Bypass obrany: Vstup úspěšně prošel přes filtr, protože ho bezpečnostní mechanizmy neočekávaly.

Provedení skriptu a výhra: Prohlížeč kód vykreslil a spustil jako skript, čímž se lab úspěšně vyřešil.
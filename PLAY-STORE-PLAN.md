# Tresor im Play Store: Plan, Preis, Checkliste

Stand: 9. November 2026. Preise und Regeln unten stammen aus meiner Recherche heute. Vor dem Eintragen bitte kurz auf den Originalseiten gegenprüfen.

## 1. Preis

**Was andere verlangen (Einzelperson, pro Jahr bzw. Monat)**
- Bitwarden Premium: 19,80 US-$/Jahr (seit Januar 2026, vorher 9,99 $)
- Proton Pass Plus: ca. 2 bis 2,49 €/Monat
- 1Password: ca. 3 bis 3,65 €/Monat (Preiserhöhung März 2026)
- NordPass: ab ca. 1,49 $/Monat
- Die Gratis-Versionen von Bitwarden und Proton Pass erlauben unbegrenzt viele Passwörter.

**Empfehlung für Tresor**
- Einmalkauf **„Tresor Pro“, 4,99 €** (sinnvoll: 3,99 bis 6,99 €). Kein Abo, weil du keine Serverkosten hast und ein Einmalpreis zu „ohne Konto, ohne Tracker“ passt.
- Gratis-Version: **10 Einträge**, **keine Kategorien**, **ein Login pro Eintrag** (`FREE_MAX` in der Datei einstellbar). Die großen Anbieter sind gratis unbegrenzt, darum kann es bei einem so strengen Limit Kritik geben. Pro: unbegrenzt, Kategorien, mehrere Logins pro Eintrag.
- Im Play Store die App selbst **gratis** anbieten und Pro als **In-App-Produkt** (Typ: einmalig) verkaufen. Google verlangt Play Billing für digitale Käufe. Ein bezahlter Download passt hier nicht, weil Gratis + Pro nur so geht.
- Google-Gebühr: 15 % auf die ersten 1 Mio. $/Jahr, wenn du dich für die 15-%-Stufe anmeldest. Google nennt für EU/UK/US ab Mitte 2026 teils neue Sätze (10 % + 5 % Abrechnungsgebühr). Rechne mit 10 bis 20 % Abzug. Von 4,99 € bleiben dir grob 4 €.
- Steuern: Das Einkommen musst du in Italien melden. Frag dazu bitte eine Steuerberatung (commercialista), ob du eine Partita IVA brauchst.

## 2. Was ich schon eingebaut habe (Ordner `play/`)

- Gratis-Regeln (10 Einträge, keine Kategorien, ein Login pro Eintrag) mit Sperre beim Anlegen, beim Import und beim Zusammenführen. Bestehende Daten werden nie gelöscht.
- **Privater Gutschein-Code** nur für dich (Menü „🎟 Code einlösen“, für PC und Handy). Die App prüft beim Start die Liste `gutscheine.json` in deinem Repository. Code zurückziehen = Zeile in der Datei auf github.com löschen. Offline bleibt Pro 14 Tage. Geschenke an andere laufen über Einmal-Codes aus der Play Console.
- Pro-Freischaltung über Play Billing (Digital Goods API) und „Kauf wiederherstellen“.
- Menüpunkte **📤 App teilen** (Teilen-Dialog des Handys, sonst Link kopieren) und **⭐ Pro**. Deutsch und Italienisch.
- Datenschutz-Abschnitt um den Kauf ergänzt, eigene Seite `datenschutz.html` (Play braucht eine öffentliche Datenschutz-URL).
- Manifest ergänzt (id, Beschreibung, Kategorien), Service-Worker-Version erhöht, Vorlage `.well-known/assetlinks.json`.

**Bitte beachten**
- Ich konnte die App nicht auf einem Android-Gerät testen. Der Kauf muss im Play-Test (Lizenztester) geprüft werden.
- Die Pro-Markierung liegt auf dem Gerät und wird bei jedem Entsperren gegen Google Play geprüft. Wer das Gerät manipuliert, könnte Pro umgehen. Für einen symbolischen Preis ist das üblich.
- Die Paket-ID `com.tamarajost.tresor` ist **nach der Veröffentlichung nicht mehr änderbar**. Sag Bescheid, wenn du eine andere willst.
- Die Teilen-Funktion teilt den Link zur App (Play-Store-Link). Der Link funktioniert erst, wenn die App veröffentlicht ist.

## 3. Was noch fehlt

1. **Google-Cloud-Projekt finden (wichtig).** In `index.html` steht eine Google-Client-ID, die mit `577667444757` beginnt. Das ist die Projektnummer. Öffne console.cloud.google.com, melde dich nacheinander mit deinen Google-Konten an und suche das Projekt mit dieser Nummer. So findest du das Konto, das du vergessen hast. Dort prüfen: (a) die Web-Domain deiner App steht unter „Autorisierte JavaScript-Quellen“, (b) die OAuth-Zustimmung steht auf „In Produktion“ (sonst laufen Anmeldungen nach 7 Tagen ab und nur Testnutzer dürfen sich anmelden), (c) Datenschutz-URL und App-Name sind eingetragen. Findest du das Projekt nicht, lege ein neues an und tausche die Client-ID (`GID`) aus. Dann funktioniert der Sync mit Google Drive für alte Daten nicht mehr automatisch.
2. **Öffentliche Web-Adresse mit HTTPS.** Die App muss irgendwo online liegen (z. B. GitHub Pages, Cloudflare Pages, Netlify). Wo liegt sie jetzt? Das brauche ich von dir.
3. **Android-Paket (.aab) bauen.** Am einfachsten ohne Programmieren: pwabuilder.com, Adresse eingeben, „Package for stores“, Android. Dort „Google Play Billing“ aktivieren und die Paket-ID eintragen. Den erzeugten Signaturschlüssel sicher aufbewahren. Ich kann das hier nicht für dich bauen, weil meine Umgebung keinen Internetzugriff für Installationen hat.
4. **assetlinks.json ausfüllen.** Den SHA-256-Fingerabdruck aus der Play Console (Setup → App-Signatur) in `.well-known/assetlinks.json` eintragen und hochladen. Sonst zeigt die App oben eine Browserleiste.
5. **Store-Grafiken.** Icon 512×512 hast du. Fehlt: **Feature-Grafik 1024×500** und **mind. 2 Handy-Screenshots**. Mach die Screenshots bitte mit Fantasie-Daten, nie mit echten Passwörtern.
6. **Play Console:** Datenschutz-URL, Datensicherheit, Inhaltseinstufung, Zielgruppe (nicht für Kinder), Werbung (nein), Preise/Länder, Händlerprofil für Zahlungen, In-App-Produkt `tresor_pro` (einmalig, 4,99 €).
7. **Testphase:** Ist dein Entwicklerkonto ein privates, nach dem 13. November 2023 erstelltes Konto, musst du vor der Veröffentlichung **12 Tester 14 Tage lang** im geschlossenen Test haben (Stand heute laut Google). Das gilt pro App. Plane dafür rund 3 Wochen ein. Organisationskonten sind ausgenommen.
8. **Rechtliches.** Die Datenschutzerklärung ist als „Entwurf“ markiert und nennt deine Privatadresse. Bei bezahlten Inhalten zeigt Google Händlerangaben öffentlich an. Lass beides prüfen und entscheide, welche Adresse öffentlich sein darf.

## 4. Antworten für das Formular „Datensicherheit“ (Vorschlag)

- Sammelt oder teilt die App Daten? **Nein, keine Daten an uns.** Der optionale Sync schreibt nur eine verschlüsselte Datei in das eigene Google Drive des Nutzers, und die Google-E-Mail wird nur lokal angezeigt. Beschreibe das im Formular ehrlich, damit es zur Datenschutzerklärung passt.
- Verschlüsselung bei der Übertragung: ja. Löschung der Daten möglich: ja (Einstellungen → Alle Daten löschen).
- Das richtige Formular-Ergebnis hängt von Googles Definition von „Erfassung“ ab. Prüfe das im Formular selbst.

## 5. Store-Texte (Deutsch)

**Titel (max. 30 Zeichen):** Tresor – Passwort-Tresor

**Kurzbeschreibung (max. 80 Zeichen):** Deine Passwörter verschlüsselt. Ohne Konto, ohne Werbung, ohne Tracker.

**Beschreibung:**
Tresor bewahrt deine Zugangsdaten verschlüsselt auf deinem Gerät auf. Du brauchst kein Konto, es gibt keine Werbung und keine Tracker.

• Verschlüsselung mit AES-256 und deinem Master-Passwort
• Kategorien mit eigener Farbe, mehrere Konten pro Eintrag
• Anmeldeart (Passwort oder Google, Apple, Facebook, Microsoft), API-Keys, Notizen und Fotos
• Suche, Verschieben per Ziehen, Dark Mode
• Entsperren mit Fingerabdruck oder Gesicht (wenn dein Gerät es kann)
• Verschlüsselter Export und Import
• Optionaler Abgleich mit deinem eigenen Google Drive
• Deutsch und Italienisch

Gratis: bis zu 10 Einträge. Mit Tresor Pro (einmaliger Kauf, kein Abo) unbegrenzt, mit Kategorien und mehreren Logins pro Eintrag.

Wichtig: Dein Master-Passwort kann niemand zurücksetzen. Wer es vergisst, verliert die Daten. Mach regelmäßig einen Export.

## 6. Reihenfolge

1. Web-Adresse klären, Dateien aus `play/` hochladen
2. Google-Cloud-Projekt prüfen (Punkt 3.1)
3. .aab mit PWABuilder bauen, Play Billing an
4. Play Console: App anlegen, In-App-Produkt `tresor_pro`, Formulare
5. Geschlossener Test mit 12 Testern (14 Tage), Kauf mit Lizenztester prüfen
6. Produktionszugang beantragen, veröffentlichen

# MorseBuzz — downloads en updatemanifest

Deze repo bevat geen broncode. Hij doet twee dingen:

1. **`update.json`** wordt via GitHub Pages geserveerd op
   <https://matthijsjonkers.github.io/morsebuzz/update.json>. De app haalt dat
   bestand bij het starten op en vergelijkt het `versionCode` met het eigen
   `BuildConfig.VERSION_CODE`.
2. De **releases** van deze repo bevatten de APK. `latest` wijst altijd naar de
   nieuwste.

## Nieuwe versie uitbrengen

1. Hoog `versionCode` én `versionName` op in `app/build.gradle.kts` van het
   app-project en bouw een nieuwe `MorseBuzz.apk`.
2. Maak een release met die APK als asset, waarbij de bestandsnaam exact
   `MorseBuzz.apk` blijft (de downloadlink is daarop vastgelegd):

   ```
   gh release create v<versionName> MorseBuzz.apk --title "MorseBuzz <versionName>" --notes "<wat er nieuw is>"
   ```

3. Pas daarna `update.json` hier aan en push. Doe dat als laatste: zodra het
   manifest een hoger `versionCode` noemt, krijgen gebruikers de melding, en dan
   moet de download er al zijn.

`versionCode` in `update.json` moet hetzelfde getal zijn als in
`app/build.gradle.kts`. Zonder ophogen werkt de controle niet, want hij
vergelijkt precies dat getal.

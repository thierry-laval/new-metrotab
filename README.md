# Réparer en permettant de sauvegarder ses paramètres dans le plugins nouvelle metrotab v1.1.0 de Google Chrome (dév) <img src="icon_128.png" align="right" alt="" width="128">

nouvelle metroTab v1.1.0 https://chrome.google.com/webstore/detail/new-metrotab/oogmkbpkoblajkomflhkkdmbfggdmefd?hl=fr

Corriger le nouveau metroTab sur le Chrome Web Store ?

### Comment sauvegarder les tuiles ?

new metroTab stocke les tuiles dans la base de données indexée du navigateur pour l'extension, de sorte que nous pouvons les récupérer à partir de là.

> La procédure suivante exécute un script externe dans le contexte de la page. Ne faites pas ce genre de procédure sur d'autres sites comme facebook ou votre site de messagerie si vous ne savez pas **exactement, ligne par ligne**, ce que fait le code que vous utilisez.

Suivez ces étapes pour télécharger le fichier de sauvegarde des tuiles :

1. Allez dans les options (Survolez le badge de l'utilisateur > Options)
2. Ouvrez un menu contextuel (clic droit) n'importe où sur la page des options, et sélectionnez l'option "Inspecter". C'est généralement la dernière. L'écran des options devrait se diviser et du code devrait apparaître.
3. Dans cette nouvelle zone, cliquez sur l'onglet "Console".
4. Collez ce code :

```js
MT.miniDB.cursor().then(tiles => {
  const blob = new Blob([JSON.stringify(tiles, null, 2)], {type: "application/json"});
  const anchor = document.createElement("a");
  anchor.href = window.URL.createObjectURL(blob);
  anchor.download = "metrotab_tiles.json";
  anchor.click();
});
```
5. Appuyez sur la touche Entrée pour exécuter le code. Après avoir appuyé sur la touche Entrée, l'invite de téléchargement du navigateur doit apparaître. Enregistrez ce fichier.

## Qu'en est-il des autres options ?

Suivez la même procédure, mais exécutez cet autre extrait :

```js
(function() {
  const config = {
    "instalado": localStorage.getItem("instalado"),
    "bloques_info": localStorage.getItem("bloques_info"),
    "apar_bgcolor": localStorage.getItem("apar_bgcolor"),
    "apar_bgimg": localStorage.getItem("apar_bgimg"),
    "livet_clima_ubic": localStorage.getItem("livet_clima_ubic"),
    "livet_da_include": localStorage.getItem("livet_da_include"),
    "livet_zonahora": localStorage.getItem("livet_zonahora"),
  };
  document.querySelectorAll('.autosave').forEach(node => {
    const value = localStorage.getItem(node.name);
    value && Object.defineProperty(config, node.name, {value});
  });

  const blob = new Blob([JSON.stringify(config, null, 2)], {type: "application/json"});
  const anchor = document.createElement("a");
  anchor.href = window.URL.createObjectURL(blob);
  anchor.download = "metrotab_config.json";
  anchor.click();
})();
```

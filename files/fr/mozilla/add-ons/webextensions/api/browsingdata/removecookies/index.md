---
title: browsingData.removeCookies()
slug: Mozilla/Add-ons/WebExtensions/API/browsingData/removeCookies
tags:
  - API
  - Add-ons
  - Extensions
  - Méthode
  - Reference
  - WebExtensions
  - browsingData
  - removeCookies
translation_of: Mozilla/Add-ons/WebExtensions/API/browsingData/removeCookies
---
{{AddonSidebar()}}

Efface les cookies du navigateur

Vous pouvez utiliser le paramètre `removalOptions`, qui est un objet  {{WebExtAPIRef("browsingData.RemovalOptions")}} pour :

- Efface seulement les cookies créés après un temps donné
- Contrôlez si les cookies doivent être supprimés uniquement à partir des pages Webnormales ou si vous souhaitez supprimer les cookies des applications et des extensions hébergées.

C'est une fonction asynchrone qui renvoie une [`Promise`](/fr/docs/Web/JavaScript/Reference/Objets_globaux/Promise).

## Syntaxe

```js
var removing = browser.browsingData.removeCookies(
  removalOptions            // RemovalOptions object
)
```

### Paramètres

- `removalOptions`
  - : `object`. Un objet {{WebExtAPIRef("browsingData.RemovalOptions")}}, qui peut être utilisé pour effacer uniquement les cookies créés après un délais donné, et pour supprimer les cookies uniquement des pages Web normales ou pour supprimer les cookies des applications et extensions hébergées.

### Valeur retournée

Une [`Promise`](/fr/docs/Web/JavaScript/Reference/Objets_globaux/Promise) qui sera remplie sans argument lorsque la suppression est terminée. Si une erreur se produit, la promise sera rejetée avec un message d'erreur.

## Compatibilité du navigateur

{{Compat("webextensions.api.browsingData.removeCookies")}}

## Exemples

Supprime les cookies créés la semaine dernière :

```js
function onRemoved() {
  console.log("removed");
}

function onError(error) {
  console.error(error);
}

function weekInMilliseconds() {
  return 1000 * 60 * 60 * 24 * 7;
}

var oneWeekAgo = (new Date()).getTime() - weekInMilliseconds();

browser.browsingData.removeCookies(
  {since: oneWeekAgo}).
then(onRemoved, onError);
```

Supprime tous les cookies :

> **Attention :**
>
> L'utilisation de l'API pour supprimer tous les cookies effacera simultanément tous les objets de stockage locaux (y compris ceux des autres extensions).
>
> Si vous souhaitez simplement effacer tous les cookies sans perturber les installations de stockage locales, utilisez [browser.cookies](/fr/docs/Mozilla/Add-ons/WebExtensions/API/cookies) pour faire une boucle et supprimer le contenu de tous les magasins de cookies.

```js
function onRemoved() {
  console.log("removed");
}

function onError(error) {
  console.error(error);
}

browser.browsingData.removeCookies({}).
then(onRemoved, onError);
```

{{WebExtExamples}}

> **Note :**
>
> Cette API est basée sur l'API Chromium [`chrome.browsingData`](https://developer.chrome.com/extensions/browsingData).
>
> Les données de compatibilité relatives à Microsoft Edge sont fournies par Microsoft Corporation et incluses ici sous la licence Creative Commons Attribution 3.0 pour les États-Unis.

<div class="hidden"><pre>// Copyright 2015 The Chromium Authors. All rights reserved.
//
// Redistribution and use in source and binary forms, with or without
// modification, are permitted provided that the following conditions are
// met:
//
//    * Redistributions of source code must retain the above copyright
// notice, this list of conditions and the following disclaimer.
//    * Redistributions in binary form must reproduce the above
// copyright notice, this list of conditions and the following disclaimer
// in the documentation and/or other materials provided with the
// distribution.
//    * Neither the name of Google Inc. nor the names of its
// contributors may be used to endorse or promote products derived from
// this software without specific prior written permission.
//
// THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS
// "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT
// LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR
// A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT
// OWNER OR CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
// SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT
// LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE,
// DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY
// THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
// (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE
// OF THIS SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
</pre></div>

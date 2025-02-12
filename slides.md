---
# You can also start simply with 'default'
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://cover.sli.dev
# some information about your slides (markdown enabled)
title: Welcome to Slidev
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# light ou dark
colorSchema: light
addons:
  - excalidraw
  - slidev-component-scroll
---

# Projet Myyebok

Gestion d'une bibliothèque

<div @click="$slidev.nav.next" class="mt-12 py-1" hover:bg="white op-10">
</div>

<div class="abs-br m-6 text-xl">
  <button @click="$slidev.nav.openInEditor" title="Open in Editor" class="slidev-icon-btn">
    <carbon:edit />
  </button>
  <a href="https://github.com/mevine54/myyebook" target="_blank" class="slidev-icon-btn">
    <carbon:logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
layout: center
---

# Besoin et contrainte du projet

- **Contexte** : Projet de groupe 
- **Projet** : Site permettant de gérer une bibliothèque
- **Durée** : 1 mois environ


---
layout: full
---


# Spécificités techniques

* **Gestion de projet** : Trello
- **Wireframe** : Excalidraw
* **Front-end** : HTML5, CSS3 ( BOOTSTRAP 5 ), Javascript ( HTMX + Sweet Alert 2)
* **Serveur d'applications** : Tomcat 10
* **Back-end** : JAVA 21
  * **Gestion des dépendances** : Maven
    * Jakarta ( Servlet et JSP ) - Password4J - Lombok - Slf4j et Logback
* **Base de donnée** : Mysql 8 
<div class="flex  ">
<ul>
<li> <b>Gestion de version</b> : Git / Github</li>
</ul>
<div class="w-a h-5">
```mermaid
---
title: "Strategie: Github Flow" 
---
gitGraph
   commit
   branch model
   checkout model
   commit
   commit
   checkout main
   merge model
   branch dao
   checkout dao
   commit
   commit
   checkout main
   merge dao
```
</div>
</div>

---
layout: center
---

# Architecture du site


<div class="h-a w-lg">
```plantuml
@startwbs
+[#SkyBlue] MYYEBOOK
++[#lightgreen] Accueil <color:blue>( Visiteur / Client )</color>
+++[#aliceblue] Connexion
+++[#aliceblue] S'incrire pour devenir client
+++[#beige]  Barre de recherche dynamique
+++[#beige]  Liste des livres
++++[#bisque]  Description d'un livre
++[#pink] Client
+++[#aliceblue] Modifier info
+++[#aliceblue] Voir emprunt
+++[#aliceblue] Se deconnecter
++[#pink] Libraires
+++[#aliceblue] liste emprunts
++++_ CRUD emprunts
+++[#aliceblue] liste livres
++++_ CRUD livres
+++[#aliceblue] liste auteur
++++_ CRUD auteurs
+++[#aliceblue] liste categories
++++_ CRUD categories
+++[#aliceblue] liste clients
++++_ CRUD clients
+++[#aliceblue] liste libraires
++++_ CRUD libraires
+++[#aliceblue] Se deconnecter
@endwbs
```

</div>

---
layout: center
---


# Cas d'utilisations 

<div class="flex h-xs mt-4 flex-items-center w-3xl m-auto">

<div class="me self-auto " >

```plantuml
@startuml
!theme sunlust
' !theme reddress-lightblue
skinparam usecase {
BackgroundColor DarkSeaGreen
BorderColor DarkSlateGray

BackgroundColor<< Main >> YellowGreen
BorderColor<< Main >> YellowGreen

ArrowColor Olive
ActorBorderColor black
ActorFontName Courier

' ActorBackgroundColor<< Human >> DarkSeaGreen
}


left to right direction
actor Visiteur as v


rectangle "Visiteur" {
  usecase "Consulter livres\nRechercher livre" as UC_consulter_livre
  usecase "Creer un compte abonne" as UC_creer_compte_abonne
}

v --> UC_consulter_livre
v --> UC_creer_compte_abonne

@enduml

```

</div>
<div>

```plantuml
@startuml
!theme sunlust
' !theme reddress-lightblue
skinparam usecase {
BackgroundColor DarkSeaGreen
BorderColor DarkSlateGray

BackgroundColor<< Main >> YellowGreen
BorderColor<< Main >> YellowGreen

ArrowColor Olive
ActorBorderColor black
ActorFontName Courier

' ActorBackgroundColor<< Human >> DarkSeaGreen
}


left to right direction
actor Abonne as a

rectangle "Abonne" {
  usecase "Consulter livres\nRechercher livre" as UC_consulter_livre_abo
  usecase "Consulter compte\nModifier compte" as UC_compte
  usecase "Emprunter un livre" as UC_emprunter
  usecase "Lister emprunts" as UC_liste_emprunt

}

a --> UC_emprunter
a --> UC_liste_emprunt
a --> UC_compte
a --> UC_consulter_livre_abo

@enduml
```
</div>
<div>
```plantuml
@startuml
!theme sunlust
' !theme reddress-lightblue
skinparam usecase {
BackgroundColor DarkSeaGreen
BorderColor DarkSlateGray

BackgroundColor<< Main >> YellowGreen
BorderColor<< Main >> YellowGreen

ArrowColor Olive
ActorBorderColor black
ActorFontName Courier

' ActorBackgroundColor<< Human >> DarkSeaGreen
}


left to right direction
actor Libraire as l
rectangle "Libraire" {
  usecase "Lister et CRUD livres" as UC_crud_livre
  usecase "Lister et CRUD auteurs" as UC_crud_auteur
  usecase "Lister et CRUD abonnes" as UC_crud_abonne
  usecase "Lister et CRUD libraires" as UC_crud_libraire
}
l --> UC_crud_livre
l --> UC_crud_auteur
l --> UC_crud_abonne
l --> UC_crud_libraire


@enduml
```
</div>
</div>

---
layout: full
---

<!--
- méthode merise
- cardinalité
- ajout: compte -> date pour le RGPD ( On ne garde pas les données indéfiniment)
- ajout: emprunter date de reservation
- contrainte d'inter association - exclusivité ( un compte appartient a un libraire ou un client mais pas les 2 à la fois )
- trigger : emprunter date
- contrainte: quantite des livres
- emprunter un livre seulement si la quantite est supérieur à zero
-->
# Modèle conceptuel des données

<Transform scale=0.75>
<img src="/src/mcd.jpg"/>
</Transform>


---
layout: full
---

<!--
- 
-->
# Modèle physique des données
<Transform scale=0.75>
<img src="/src/mpd.jpg"/>
</Transform>

---
layout: two-cols
image: /src/maquettage_mobile_accueil.svg
---

<!--
- La partie utilisateur est responsive -> BOOTSTRAP
- 
- ajout: compte -> date pour le RGPD ( On ne garde pas les données indéfiniment)
- ajout: emprunter date de reservation
- contrainte d'inter association - exclusivité ( un compte appartient a un libraire ou un client mais pas les 2 à la fois )
- trigger : emprunter date
- contrainte: quantite des livres
- emprunter un livre seulement si la quantite est supérieur à zero
-->

# Maquettage mobile
## Visiteur et client

::right::

<Transform scale=1.05>
<img src="/src/maquettage_mobile_accueil.svg"/>
</Transform>

---
layout: center

---


# Maquettage Desktop

Libraire ->  Partie livre

<div class="flex items-center justify-center">
<div class="w-[800px] ">
  <img src="/src/maquettage_desktop_libraire_livre.svg"/>
</div>
</div>

---
level: 4
---

# Composant Métiers ( Client )

<!--
- utilisation de javadoc
- on passe par les setters -> encapsulation des données
- pour la validation  on utilise des exceptions personnalisées
-->

<div class="flex gap-col-lg ">

<Transform :scale="0.85">
<h4><b>Constructeur</b></h4>
```java {*|1-12|13-25|43-54}
  /**
    * Instantiates a new Client.
     *
     * @param compte     the compte
     * @param clientId   the client id
     * @param nom        the nom
     * @param prenom     the prenom
     * @param email      the email
     * @param adresse    the adresse
     * @param ville      the ville
     * @param codePostal the code postal
     */
    public Client (Compte compte, Integer clientId,
     String nom, String prenom, 
    String email, String adresse,
     String ville, String codePostal) {
        compte.setRole("ROLE_CLIENT");
        setCompte(compte);
        setClientId(clientId);
        setNom(nom);
        setPrenom(prenom);
        setEmail(email);
        setAdresse(adresse);
        setVille(ville);
        setCodePostal(codePostal);
    }
```
</Transform>

<Transform :scale="0.85">
<h4><b>SetNom</b></h4>
```java {*|8-12|14-16|17-18|19-20|}
    /**
     * Sets nom.
     *
     * @param nom the nom
     */
    public void setNom(String nom) {
        int longueurMin = 2;
        int longueurMax = 50;
        if (nom == null) {
            throw new NullValueException("Le nom du client ne peut pas etre null");
        }
        nom = nom.trim();
        String regex = "^[A-Za-zàâäéèêëîïôöùûüçÀÂÄÉÈÊËÎÏÔÖÙÛÜÇ\\-]{" + longueurMin + "," + longueurMax + "}$";
        if (nom.length() < longueurMin) {
            throw new LongueurMinimaleException("Le nom du client est trop court:" + nom + ", " + nom.length() + " caracteres");
        } else if (nom.length() > longueurMax) {
            throw new LongueurMaximaleException("Le nom du client est trop long:" + nom + ", " + nom.length() + " caracteres");
        } else if (!nom.matches(regex)) {
            throw new RegexValidationException("Le nom n'est pas valide. Veuillez entrer un nom contenant uniquement des lettres et des espaces, avec une longueur de " + longueurMin + " à " + longueurMax + " caractères");
        }
        this.nom = nom;
    }
```
</Transform>
</div>

---
layout: two-cols
---

# DAO - Libraire

- Implémentation de l'interface DAO
- Création d'un compte -> Transaction 
- Requêtes préparées
- Utilisation du logger
- Création de la libraire 
- Validation ou rollback
- fin de la transaction

::right::
<Transform :scale="0.55" class="w-180%">
```java {|1|2-14|18|13-28|29-32|38-42|}{lines:true}
@Override
public Integer insert(Libraire libraire) throws SQLException {
    Integer libId = null;
    String sql = "INSERT INTO Compte (cpt_login, cpt_mdp,cpt_role) VALUES ( ?, ?,?)";
    Integer compteId = 0;
    try {
        Connection connection = DatabaseConnection.getInstanceDB();
        connection.setAutoCommit(false);
        PreparedStatement ps = connection.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);
        ps.setString(1, libraire.getCompte().getLogin());
        ps.setString(2, libraire.getCompte().getPassword());
        ps.setString(3, libraire.getCompte().getRole());
        ps.executeUpdate();
        ResultSet generatedKeysCompte = ps.getGeneratedKeys();
        if (generatedKeysCompte.next()) {
            sql = "INSERT INTO libraire ( lib_nom, lib_prenom,cpt_id) VALUES ( ?, ?,?)";
            compteId = generatedKeysCompte.getInt(1);
            log.info("COMPTE : -----  " + compteId);
            ps = connection.prepareStatement(sql, Statement.RETURN_GENERATED_KEYS);
            ps.setString(1, libraire.getNom());
            ps.setString(2, libraire.getPrenom());
            ps.setInt(3, compteId);
            ps.executeUpdate();
            ResultSet generatedKeysLibraire = ps.getGeneratedKeys();
            if (generatedKeysLibraire.next()) {
                int libraireId = generatedKeysLibraire.getInt(1);
                libraire.setLibId(libraireId);
                connection.commit();
            }
        } else {
            connection.rollback();
        }
    } catch (SQLException e) {
        connection.rollback();
        throw new RuntimeException(e);
    } finally {
        if (connection != null) {
            try {
                connection.setAutoCommit(true);
            } catch (SQLException e) {
                log.warn("Impossible de rétablir l'autocommit", e);
            }
        }
    }
    return libId;
}
```
</Transform>

---
layout: center
---

<!--
- Tomcat: recoit la requete http et l envoie a une servlet ( controlleur) 
- Model: Classe Métier java
- Vue: JSP 
-->

# Modèle vue contrôleur

<div class="w-[500px] ">
  <img src="/src/mvc.jpg"/>
</div>

---
layout: center
---


# Les rôles

```plantuml
@startuml
skinparam sequence {
    ActorBackgroundColor<<Visiteur>> LightBlue
    ActorBackgroundColor<<Client>> LightGreen
    ActorBackgroundColor<<Libraire>> LightYellow
    ActorBackgroundColor<<Libraire_attente>> LightCoral
}
actor Visiteur <<Visiteur>>
box "Après connexion" #LightBlue
actor Client <<Client>>
actor Libraire <<Libraire>>
actor Libraire_Attente <<Libraire_Attente>>
end box

Visiteur -> Client : S'inscrire
Libraire -> Libraire_Attente : Créer un autre libraire
Libraire_Attente -> Libraire : Changer le mot de passe
@enduml

@enduml
```

---
layout: full
---

```java 
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
        String utilisateur = request.getParameter("utilisateur");
        String mdp = request.getParameter("mdp");

        CompteDAOImp compteDAOImpl = new CompteDAOImp();
        LibraireDAOImp libraireDAOImpl = new LibraireDAOImp();
        ClientDAOImp clientDAOImp = new ClientDAOImp();
        HttpSession session = null;
        Compte compte = null;
        try {
            compte = compteDAOImpl.getParLogin(utilisateur);
            if (compte != null) {
                String hashedPassword = compteDAOImpl.getHashedPasswordByLogin(utilisateur);
                boolean estAuthentifie = Password.check(mdp, hashedPassword).addPepper(PoivreToken.POIVRE).withBcrypt();
                if (!estAuthentifie) {
                    response.sendRedirect("connexion?info=cred-invalid");
                }

                log.info("compte: " + compte);

                if (compte.getRole().equals("ROLE_LIBRAIRE") || compte.getRole().equals("ROLE_LIBRAIRE_ATTENTE")) {
                    Libraire libraire = libraireDAOImpl.getParCompteId(compte.getCompteId());
                    log.info("estAuthentifie: " + estAuthentifie);
                    if (libraire != null && estAuthentifie) {
                        session = request.getSession(true);
                        if (libraire.isEstApprouve()) {
                            session.setAttribute("role", "ROLE_LIBRAIRE");
                            response.sendRedirect("monCompteLibraire");
                        } else {
                            session.setAttribute("role", "ROLE_LIBRAIRE_ATTENTE");
                            // TODO: rediriger vers une page changer password
                            response.sendRedirect("monCompteLibraire");
                        }
                    }
                    log.info("libraire: " + libraire);
                } else if (compte.getRole().equals("ROLE_CLIENT") && estAuthentifie) {
                    Client client = clientDAOImp.getParCompteId(compte.getCompteId());
                    if (client != null) {
                        session = request.getSession(true);
                        session.setAttribute("role", "ROLE_CLIENT");
                        response.sendRedirect("monCompteClient");
                    }
                    log.info("client: " + client);
                }
            }
            else{
                response.sendRedirect("connexion?info=cred-invalid");
            }
        } catch (SQLException e) {
            log.error("Erreur lors de la récupération du compte", e);
            response.sendRedirect("connexion.jsp?error=true");
        }
    }
```


---
transition: fade-out
---

# What is Slidev?

Slidev is a slides maker and presenter designed for developers, consist of the following features

- 📝 **Text-based** - focus on the content with Markdown, and then style them later
- 🎨 **Themable** - themes can be shared and re-used as npm packages
- 🧑‍💻 **Developer Friendly** - code highlighting, live coding with autocompletion
- 🤹 **Interactive** - embed Vue components to enhance your expressions
- 🎥 **Recording** - built-in recording and camera view
- 📤 **Portable** - export to PDF, PPTX, PNGs, or even a hostable SPA
- 🛠 **Hackable** - virtually anything that's possible on a webpage is possible in Slidev
<br>
<br>

Read more about [Why Slidev?](https://sli.dev/guide/why)

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

<!--
Here is another comment.
-->

---
transition: slide-up
level: 2
---

# Navigation

Hover on the bottom-left corner to see the navigation's controls panel, [learn more](https://sli.dev/guide/ui#navigation-bar)

## Keyboard Shortcuts

|                                                     |                             |
| --------------------------------------------------- | --------------------------- |
| <kbd>right</kbd> / <kbd>space</kbd>                 | next animation or slide     |
| <kbd>left</kbd>  / <kbd>shift</kbd><kbd>space</kbd> | previous animation or slide |
| <kbd>up</kbd>                                       | previous slide              |
| <kbd>down</kbd>                                     | next slide                  |

<!-- https://sli.dev/guide/animations.html#click-animation -->
<img
  v-click
  class="absolute -bottom-9 -left-7 w-80 opacity-50"
  src="https://sli.dev/assets/arrow-bottom-left.svg"
  alt=""
/>
<p v-after class="absolute bottom-23 left-45 opacity-30 transform -rotate-10">Here!</p>

---
layout: two-cols
layoutClass: gap-16
---

# Table of contents

You can use the `Toc` component to generate a table of contents for your slides:

```html
<Toc minDepth="1" maxDepth="1" />
```

The title will be inferred from your slide content, or you can override it with `title` and `level` in your frontmatter.

::right::

<Toc text-sm minDepth="1" maxDepth="2" />

---
layout: image-right
image: https://cover.sli.dev
---

# Code

Use code snippets and get the highlighting directly, and even types hover!

```ts {all|5|7|7-8|10|all} twoslash
// TwoSlash enables TypeScript hover information
// and errors in markdown code blocks
// More at https://shiki.style/packages/twoslash

import { computed, ref } from 'vue'

const count = ref(0)
const doubled = computed(() => count.value * 2)

doubled.value = 2
```

<arrow v-click="[4, 5]" x1="350" y1="310" x2="195" y2="334" color="#953" width="2" arrowSize="1" />

<!-- This allow you to embed external code blocks -->
<<< @/snippets/external.ts#snippet

<!-- Footer -->

[Learn more](https://sli.dev/features/line-highlighting)

<!-- Inline style -->
<style>
.footnotes-sep {
  @apply mt-5 opacity-10;
}
.footnotes {
  @apply text-sm opacity-75;
}
.footnote-backref {
  display: none;
}
</style>

<!--
Notes can also sync with clicks

[click] This will be highlighted after the first click

[click] Highlighted with `count = ref(0)`

[click:3] Last click (skip two clicks)
-->

---
level: 2
---

# Shiki Magic Move

Powered by [shiki-magic-move](https://shiki-magic-move.netlify.app/), Slidev supports animations across multiple code snippets.

Add multiple code blocks and wrap them with <code>````md magic-move</code> (four backticks) to enable the magic move. For example:

````md magic-move {lines: true}
```ts {*|2|*}
// step 1
const author = reactive({
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
})
```

```ts {*|1-2|3-4|3-4,8}
// step 2
export default {
  data() {
    return {
      author: {
        name: 'John Doe',
        books: [
          'Vue 2 - Advanced Guide',
          'Vue 3 - Basic Guide',
          'Vue 4 - The Mystery'
        ]
      }
    }
  }
}
```

```ts
// step 3
export default {
  data: () => ({
    author: {
      name: 'John Doe',
      books: [
        'Vue 2 - Advanced Guide',
        'Vue 3 - Basic Guide',
        'Vue 4 - The Mystery'
      ]
    }
  })
}
```

Non-code blocks are ignored.

```vue
<!-- step 4 -->
<script setup>
const author = {
  name: 'John Doe',
  books: [
    'Vue 2 - Advanced Guide',
    'Vue 3 - Basic Guide',
    'Vue 4 - The Mystery'
  ]
}
</script>
```
````

---

# Components

<div grid="~ cols-2 gap-4">
<div>

You can use Vue components directly inside your slides.

We have provided a few built-in components like `<Tweet/>` and `<Youtube/>` that you can use directly. And adding your custom components is also super easy.

```html
<Counter :count="10" />
```

<!-- ./components/Counter.vue -->
<Counter :count="10" m="t-4" />

Check out [the guides](https://sli.dev/builtin/components.html) for more.

</div>
<div>

```html
<Tweet id="1390115482657726468" />
```

<Tweet id="1390115482657726468" scale="0.65" />

</div>
</div>

<!--
Presenter note with **bold**, *italic*, and ~~striked~~ text.

Also, HTML elements are valid:
<div class="flex w-full">
  <span style="flex-grow: 1;">Left content</span>
  <span>Right content</span>
</div>
-->

---
class: px-20
---

# Themes

Slidev comes with powerful theming support. Themes can provide styles, layouts, components, or even configurations for tools. Switching between themes by just **one edit** in your frontmatter:

<div grid="~ cols-2 gap-2" m="t-2">

```yaml
---
theme: default
---
```

```yaml
---
theme: seriph
---
```

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-default/01.png?raw=true" alt="">

<img border="rounded" src="https://github.com/slidevjs/themes/blob/main/screenshots/theme-seriph/01.png?raw=true" alt="">

</div>

Read more about [How to use a theme](https://sli.dev/guide/theme-addon#use-theme) and
check out the [Awesome Themes Gallery](https://sli.dev/resources/theme-gallery).

---

# Clicks Animations

You can add `v-click` to elements to add a click animation.

<div v-click>

This shows up when you click the slide:

```html
<div v-click>This shows up when you click the slide.</div>
```

</div>

<br>

<v-click>

The <span v-mark.red="3"><code>v-mark</code> directive</span>
also allows you to add
<span v-mark.circle.orange="4">inline marks</span>
, powered by [Rough Notation](https://roughnotation.com/):

```html
<span v-mark.underline.orange>inline markers</span>
```

</v-click>

<div mt-20 v-click>

[Learn more](https://sli.dev/guide/animations#click-animation)

</div>

---

# Motions

Motion animations are powered by [@vueuse/motion](https://motion.vueuse.org/), triggered by `v-motion` directive.

```html
<div
  v-motion
  :initial="{ x: -80 }"
  :enter="{ x: 0 }"
  :click-3="{ x: 80 }"
  :leave="{ x: 1000 }"
>
  Slidev
</div>
```

<div class="w-60 relative">
  <div class="relative w-40 h-40">
    <img
      v-motion
      :initial="{ x: 800, y: -100, scale: 1.5, rotate: -50 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-square.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ y: 500, x: -100, scale: 2 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-circle.png"
      alt=""
    />
    <img
      v-motion
      :initial="{ x: 600, y: 400, scale: 2, rotate: 100 }"
      :enter="final"
      class="absolute inset-0"
      src="https://sli.dev/logo-triangle.png"
      alt=""
    />
  </div>

  <div
    class="text-5xl absolute top-14 left-40 text-[#2B90B6] -z-1"
    v-motion
    :initial="{ x: -80, opacity: 0}"
    :enter="{ x: 0, opacity: 1, transition: { delay: 2000, duration: 1000 } }">
    Slidev
  </div>
</div>

<!-- vue script setup scripts can be directly used in markdown, and will only affects current page -->
<script setup lang="ts">
const final = {
  x: 0,
  y: 0,
  rotate: 0,
  scale: 1,
  transition: {
    type: 'spring',
    damping: 10,
    stiffness: 20,
    mass: 2
  }
}
</script>

<div
  v-motion
  :initial="{ x:35, y: 30, opacity: 0}"
  :enter="{ y: 0, opacity: 1, transition: { delay: 3500 } }">

[Learn more](https://sli.dev/guide/animations.html#motion)

</div>

---

# LaTeX

LaTeX is supported out-of-box. Powered by [KaTeX](https://katex.org/).

<div h-3 />

Inline $\sqrt{3x-1}+(1+x)^2$

Block
$$ {1|3|all}
\begin{aligned}
\nabla \cdot \vec{E} &= \frac{\rho}{\varepsilon_0} \\
\nabla \cdot \vec{B} &= 0 \\
\nabla \times \vec{E} &= -\frac{\partial\vec{B}}{\partial t} \\
\nabla \times \vec{B} &= \mu_0\vec{J} + \mu_0\varepsilon_0\frac{\partial\vec{E}}{\partial t}
\end{aligned}
$$

[Learn more](https://sli.dev/features/latex)

---

# Diagrams

You can create diagrams / graphs from textual descriptions, directly in your Markdown.

<div class="grid grid-cols-4 gap-5 pt-4 -mb-6">

```mermaid {scale: 0.5, alt: 'A simple sequence diagram'}
sequenceDiagram
    Alice->John: Hello John, how are you?
    Note over Alice,John: A typical interaction
```

```mermaid {theme: 'neutral', scale: 0.8}
graph TD
B[Text] --> C{Decision}
C -->|One| D[Result 1]
C -->|Two| E[Result 2]
```

```mermaid
mindmap
  root((mindmap))
    Origins
      Long history
      ::icon(fa fa-book)
      Popularisation
        British popular psychology author Tony Buzan
    Research
      On effectiveness<br/>and features
      On Automatic creation
        Uses
            Creative techniques
            Strategic planning
            Argument mapping
    Tools
      Pen and paper
      Mermaid
```

```plantuml {scale: 0.7}
@startuml

package "Some Group" {
  HTTP - [First Component]
  [Another Component]
}

node "Other Groups" {
  FTP - [Second Component]
  [First Component] --> FTP
}

cloud {
  [Example 1]
}

database "MySql" {
  folder "This is my folder" {
    [Folder 3]
  }
  frame "Foo" {
    [Frame 4]
  }
}

[Another Component] --> [Example 1]
[Example 1] --> [Folder 3]
[Folder 3] --> [Frame 4]

@enduml
```

</div>

Learn more: [Mermaid Diagrams](https://sli.dev/features/mermaid) and [PlantUML Diagrams](https://sli.dev/features/plantuml)

---
foo: bar
dragPos:
  square: 691,32,167,_,-16
---

# Draggable Elements

Double-click on the draggable elements to edit their positions.

<br>

###### Directive Usage

```md
<img v-drag="'square'" src="https://sli.dev/logo.png">
```

<br>

###### Component Usage

```md
<v-drag text-3xl>
  <div class="i-carbon:arrow-up" />
  Use the `v-drag` component to have a draggable container!
</v-drag>
```

<v-drag pos="663,206,261,_,-15">
  <div text-center text-3xl border border-main rounded>
    Double-click me!
  </div>
</v-drag>

<img v-drag="'square'" src="https://sli.dev/logo.png">

###### Draggable Arrow

```md
<v-drag-arrow two-way />
```

<v-drag-arrow pos="67,452,253,46" two-way op70 />

---
src: ./pages/imported-slides.md
hide: false
---

---

# Monaco Editor

Slidev provides built-in Monaco Editor support.

Add `{monaco}` to the code block to turn it into an editor:

```ts {monaco}
import { ref } from 'vue'
import { emptyArray } from './external'

const arr = ref(emptyArray(10))
```

Use `{monaco-run}` to create an editor that can execute the code directly in the slide:

```ts {monaco-run}
import { version } from 'vue'
import { emptyArray, sayHello } from './external'

sayHello()
console.log(`vue ${version}`)
console.log(emptyArray<number>(10).reduce(fib => [...fib, fib.at(-1)! + fib.at(-2)!], [1, 1]))
```

---
layout: center
class: text-center
---

# Learn More

[Documentation](https://sli.dev) · [GitHub](https://github.com/slidevjs/slidev) · [Showcases](https://sli.dev/resources/showcases)

<PoweredBySlidev mt-10 />

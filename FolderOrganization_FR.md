# Organisation des répertoires d'un référentiel Github pour la conception d'une ontologie
>>> Une place pour chaque document et chaque document à sa place ;-)

Introduction
-
L'organisation proposée découle directement de la méthodologie de conception d'une ontologie telle que présentée <a href="https://docs.google.com/document/d/10uLIh04yptZ8NwRA6wBGdvEjfF96tPkB1S0ggKmjw8o">ICI</a>

Proposition
-
<table>
    <thead>
        <tr>
            <th>#</th>
            <th>Label</th>
            <th>Objective</th>
            <th>Description / Content</th>
            <th>Comment</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>0.</td>
            <td>Finality</td>
            <td>Document(s) permettant de définir la finalité de l’ontologie</td>
            <td>Quel son but, son usage clef ?</br>A qui et à quoi va-t-elle servir ?</td>
            <td>Il est pertinent d'identifier les  3  choses suivantes :
</br>* Les objectifs à atteindre
</br>* Les facteurs influençants (éléments perturbants le fonctionnement actuel)
</br>* Les initiatives imaginées pour répondre aux objectifs  tout en contrant les influences</td>
        </tr>
        <tr>
            <td>1.</td>
            <td>Scope</td>
            <td>Document(s) permettant de définir le périmètre de l’ontologie</td>
            <td>Quelle est sa “largeur” et sa “profondeur” ?</br>Quel est sont impact ?</td>
            <td>Le périmètre d’une ontologie se définit d’abord et avant tout par la liste exhaustive des activités métiers devant être supportées.</br>
Ensuite, dans certaines circonstances, il peut être utile d'identifier en complément :
</br>* Les documents à remplacer
</br>* Les applications informatiques impactées
</br>* Les vocabulaires utilisées
</br>* Les individus concernés</td>
        </tr>
         <tr>
            <td>1.0.</td>
            <td>Overview</td>
            <td>Document de présentation concise du périmètre de l’ontologie</td>
            <td>Liste des activités métiers à supporter</td>
            <td></td>
        </tr>
        <tr>
            <td>1.1.</td>
            <td>Use Case</td>
            <td>Document(s) permettant de décrire de manière détaillée les usages de l’ontologie</td>
            <td>Description des activités métiers de manière générique ou de manière spécifique via des cas d'usages concrets.</br>Un cas d’usage étant vu comme une activité métier “instancié” (avec utilisation d’individus).
</td>
            <td>Pour chaque activité et/ou cas d’usage : 
</br>* Rôle impliqué(s)
</br>* Finalité
</br>* Description
</br>* Evènement déclencheur
</br>* Concepts produits
</br>* Concepts consommés
</br>* Exigences associées
</br>* Commentaires
</td>
        </tr>
        <tr>
            <td>1.2.</td>
            <td>Documents</td>
            <td>Document de présentation concise du périmètre de l’ontologie</td>
            <td>Liste de documents et des concepts métiers associés</td>
            <td>Permet d’extraire les concepts métiers dont “parle” les documents</td>
        </tr>
        <tr>
            <td>1.3.</td>
            <td>Applications</td>
            <td>Document permettant d’identifier les applications informatiques  actuellement en charge des activités métiers</td>
            <td>Liste d'applications informatique et des modèles de données associés</td>
            <td>Permet de faire du “reverse engineering” à partir des modèles de données de chaque application</td>
        </tr>
        <tr>
            <td>1.4.</td>
            <td>Vocabularies</td>
            <td>Document permettant d’identifier les vocabulaires potentiellement intéressant pour l’ontologie</td>
            <td>Liste de vocabulaires</td>
            <td>Permet d’identifier les concepts métiers dénommé par les termes du vocabulaire</td>
        <tr>
            <td>1.5.</td>
            <td>Individuals</td>
            <td>Document  permettant  d'identifier les individus du périmètre</td>
            <td>Liste d’individus, classé par concept(s)</td>
            <td>Permet de remonter au concept depuis l'individu identifié</td>
        </tr>
         <tr>
            <td>2.</td>
            <td>Semantic</td>
            <td>Document(s) permettant de définir le modèle sémantique des concepts métiers</td>
            <td></td>
            <td></td>
        </tr>
        <tr>
            <td>2.0.</td>
            <td>Conceptionary</td>
            <td>Document listant les concepts métiers candidats au modèle</td>
            <td>Liste de référence des concepts métiers</td>
            <td>our chaque concept : 
</br>* Terme préféré (obligatoire / unique)
</br>* Termes alternatifs (optionnel / multiple)
</br>* Description (obligatoire / unique)
</br>* Commentaire (optionnel / multiple)
</br>* Exemples (idéalement 3 à 5)
</br>* Classification (le cas échant)
</td>
        </tr>
        <tr>
            <td>2.1.</td>
            <td>Model</td>
            <td>Documents mettant en relation les concepts métiers</td>
            <td>Mise en relation des concept métiers (et propriétés)</td>
            <td>Graphes, Tables de propriétés, ...</td>
        </tr>
        <tr>
            <td>2.2.</td>
            <td>Rules</td>
            <td>Documents décrivant la manière dont le modèls sémantique des concepts métiers est contraint / controlé</td>
            <td>Règles métiers de structure “si ... , alors …”</td>
            <td></td>
        </tr>
        <tr>
            <td>3.0.</td>
            <td>Ontology</td>
            <td>To Be Defined by Thomas</td>
            <td></td>
            <td></td>
        </tr>
    </tbody>
</table>


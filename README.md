# WEB3.0 - Le langage de requêtes **SPARQL** (recherche de motifs dans un graphe)

### ANTELME Mathis

## 1. Le langage **SPARQL**

À partir du fichier `univ1.rdfs` présent dans l’archive du TP (contenant un schéma et des données), du cours, d’une présentation de SPARQL et de la recommandation W3, écrire les requêtes **SPARQL** permettant d’obtenir les informations suivantes:

> **1.** *Déterminer les personnes qui sont enseignantes. On attend le résultat suivant:*

```xml
<results>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#FredMartin</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#HerveBlanchon</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#RobertDupond</uri>
        </binding>
    </result>
</results>
```

La requête:

```SQL
PREFIX ex:  <http://example.org#>

SELECT ?x
WHERE
{
    ?x rdf:type ex:Teacher .
}
```

> *Est-ce que **CORESE** supporte l’inférence ?*

Oui car sinon on n'aurait pas accès à toutes les données que l'on souhaite.

> *Que se passe-t-il lorsque l'on décoche l'option **RDFS** dans le menu engine et que l'on exécute de nouveau la requête ?*

Il nous manque le résultat suivante: `<binding name='x'><uri>http://www.univ-larochelle.fr#FredMartin</uri></binding>`, ce qui prouve bien que **CORESE** supporte l'inférence.

---

> **2.** *Déterminer les personnes employées par l'université et de la Rochelle et leur statut. On attend le résultat suivant:*

```xml
<results>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#FredMartin</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Person</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#FredMartin</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Phd-Student</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#HerveBlanchon</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Person</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#HerveBlanchon</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Teacher</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#RobertDupond</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Person</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#RobertDupond</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Teacher</uri>
        </binding>
    </result>
</results>
```

La requête:

```SQL
PREFIX ex:  <http://example.org#>

SELECT ?x ?type
WHERE
{ 
    ?x rdf:type ?type .
    ?x ex:employed-by <http://www.univ-larochelle.fr> .
}
```

---

> **3.** *Par rapport à la requête précédente, on souhaiterait récupérer uniquement les résultats suivants (ne pas récupérer les réponses liées au type `Person`):*

```xml
<results>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#FredMartin</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Phd-Student</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#HerveBlanchon</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Teacher</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#RobertDupond</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Teacher</uri>
        </binding>
    </result>
</results>
```

La requête:

```SQL
PREFIX ex:  <http://example.org#>

SELECT ?x ?type
WHERE
{ 
    ?x rdf:type ?type .
    ?x ex:employed-by <http://www.univ-larochelle.fr>
    FILTER (?type != ex:Person)
}
```

---

> **4.** *Déterminer les personnes étant en relation avec l’université. Le résultat attendu est le suivant:*

```xml
<results>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#RobertDupond</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Teacher</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#HerveBlanchon</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Teacher</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#HenriDurand</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Student</uri>
        </binding>
    </result>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#FredMartin</uri>
        </binding>
        <binding name= ’type’>
            <uri>http://example.org#Phd-Student</uri>
        </binding>
</results>
```

La requête:

```SQL

```

---

> **5.** *Déterminer les personnes ayant comme responsable `Robert Dupond`. Le résultat attendu est le suivant:*

```xml
<results>
    <result>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#FredMartin</uri>
        </binding>
        <binding name= ’x’>
            <uri>http://www.univ-larochelle.fr#HerveBlanchon</uri>
        </binding>
</results>
```

La requête:

```SQL

```

---

> **6.** *Construire le graphe **RDF** suivant à partir d’une requête **SPARQL** :*

```xml
<?xml version="1.0"?>
<rdf:RDF xmlns:rdf= ’http: www.w3.org 1999 02 22-rdf-syntax-ns#’ xmlns:ex= ’http: example.org#’ xmlns:ulr= ’http: www.univ-larochelle.fr#’>
    <rdf:Description rdf:about= ’http: www.univ-larochelle.fr#HerveBlanchon’>
        <ex:is-managed-by rdf:resource= ’http: www.univ-larochelle.fr#RobertDupond’ />
    </rdf:Description>
    <rdf:Description rdf:about= ’http: www.univ-larochelle.fr#FredMartin’>
        <ex:is-managed-by rdf:resource= ’http: www.univ-larochelle.fr#RobertDupond’ />
    </rdf:Description>
</rdf:RDF>
```

La requête:

```SQL

```

---

> **7.** *À partir du schéma `univ2.rdfs` (utilisant cette fois-ci des nœuds anonymes) déterminer le nom des personnes qui sont enseignantes. Si elles possèdent un responsable, le faire apparaître. Le résultat attendu est le suivant:*

```xml
<results>
    <result>
        <binding name= ’teacher_name’>
            <literal>Herve Blanchon</literal>
        </binding>
        <binding name= ’manager_name’>
            <literal>Robert Dupond</literal>
        </binding>
    </result>
    <result>
        <binding name= ’teacher_name’>
            <literal>Fred Martin</literal>
        </binding>
        <binding name= ’manager_name’>
            <literal>Robert Dupond</literal>
        </binding>
    </result>
    <result>
        <binding name= ’teacher_name’>
            <literal>Robert Dupond</literal>
        </binding>
    </result>
</results>
```

La requête:

```SQL

```

---

> **8.** *Déterminer le nom des personnes qui sont inscrites ou employées à l’université de La Rochelle. En modifiant votre requête, distinguer les noms dans chaque catégorie. Le premier résultat attendu est le suivant:*

```xml
<results>
    <result>
        <binding name= ’name’>
            <literal>Herve Blanchon</literal>
        </binding>
    </result>
    <result>
        <binding name= ’name’>
            <literal>Fred Martin</literal>
        </binding>
    </result>
    <result>
        <binding name= ’name’>
            <literal>Robert Dupond</literal>
        </binding>
    </result>
    <result>
        <binding name= ’name’>
            <literal>Henri Durand</literal>
        </binding>
    </result>
</results>
```
> *Le second résultat attendu est le suivant:*

```xml
<results>
    <result>
        <binding name= ’employe_name’>
            <literal>Herve Blanchon</literal>
        </binding>
    </result>
    <result>
        <binding name= ’employe_name’>
            <literal>Fred Martin</literal>
        </binding>
    </result>
    <result>
        <binding name= ’employe_name’>
            <literal>Robert Dupond</literal>
        </binding>
    </result>
    <result>
        <binding name= ’student_name’>
            <literal>Fred Martin</literal>
        </binding>
    </result>
    <result>
        <binding name= ’student_name’>
            <literal>Henri Durand</literal>
        </binding>
    </result>
</results>
```

La requête:

```SQL

```

---

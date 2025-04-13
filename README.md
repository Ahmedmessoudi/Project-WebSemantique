# 🧠 Ontologie de la Santé - Mini Projet Sémantique

## 📚 Description du Projet

Ce mini projet a pour objectif de mettre en pratique les technologies du Web sémantique : **RDF**, **RDFS**, **OWL**, **SPARQL** et **SWRL**. Le domaine choisi est **la santé**, un domaine riche en concepts, idéal pour illustrer la puissance des ontologies. Le projet est réalisé avec l’outil **Protégé**, et les fichiers RDF/XML sont publiés sur GitHub.

## 🎯 Objectifs pédagogiques

À l’issue du projet, les objectifs suivants doivent être atteints :

- 📐 **Modélisation** : conception d’une ontologie en RDF, RDFS et OWL.
- 🔎 **Requêtes** : interroger l’ontologie avec SPARQL.
- 🧠 **Inférences** : enrichissement avec des règles SWRL.
- 🗂️ **Documentation** : production d’une documentation claire et précise.
- 💻 **Partage** : hébergement du projet sur GitHub et partage sur Moodle.

---

## 🏥 Domaine : Santé

Le domaine de la santé est choisi pour son importance sociétale et sa richesse sémantique. Il comprend :

- 👨‍⚕️ **Médecins**
- 👩‍⚕️ **Infirmiers**
- 🧪 **Spécialités médicales**
- 🏥 **Services hospitaliers**
- 🩺 **Consultations**
- 🧾 **Dossiers médicaux**
- 💊 **Médicaments**

---

## 🧩 Technologies et Standards Utilisés

| Nom | Namespace |
|-----|-----------|
| XML Schema | `http://www.w3.org/2001/XMLSchema#` |
| Dublin Core | `http://purl.org/dc/elements/1.1/` |
| FOAF | `http://xmlns.com/foaf/0.1/` |
| SKOS | `http://www.w3.org/2004/02/skos/core#` |
| RDFS | `http://www.w3.org/2000/01/rdf-schema#` |
| OWL | `http://www.w3.org/2002/07/owl#` |

---

## 🧱 Architecture du Projet

```plaintext
📁 sante-ontologie/
    ├──  ontology
        ├── 📄 sante ontologie.rdf     → Ontologie en RDF
        ├── 📄 sante ontologie.owl     → Ontologie enrichie en OWL
    ├──   queries
        ├── 📄 medica.sparql           → Requêtes SPARQL
    ├──  docs
        ├── 📄 rapport.pdf          → Rapport finale du project
    ├── 📄 README.md               → Fichier de documentation
```

---

## 🏗️ Structure de l’Ontologie

### 🏷️ Classes Principales

- `Medecin`, `Infirmier`, `Patient`, `Service`, `Consultation`, `Specialite`, `Hopital`

### 🔗 Propriétés

- `aPourSpecialite`, `travailleDans`, `aConsulte`, `prescrit`, `aPourNom`, `aPourPrenom`, `aPourDateNaissance`, `aPourService`

### 🧬 Sous-classes et sous-propriétés

- Exemple : `Medecin` est une sous-classe de `PersonnelMedical`
- Exemple : `aPourSpecialite` est une propriété définie pour `Medecin`

---

## 🧪 Requêtes SPARQL

Les requêtes sont définies dans le fichier [`medica.sparql`](./medica.sparql)

### 🔍 Exemples de requêtes et leurs rôles

1. **Liste des médecins avec leur spécialité**  
   Permet de visualiser les médecins et leurs domaines d’expertise.

2. **Patients ayant consulté un service donné**  
   Identifie les patients associés à un service spécifique.

3. **Nombre total de consultations par service**  
   Donne une idée de la charge de travail par service.

4. **Médicaments prescrits par un médecin**  
   Permet de tracer les prescriptions médicales.

---

## ⚙️ Règles SWRL

Les règles SWRL enrichissent l’ontologie en permettant des inférences logiques. Exemples :

- **Règle 1** : Si une personne est médecin et travaille dans un service, alors elle est affectée à ce service.
- **Règle 2** : Si un patient consulte un médecin, alors ce médecin l’a consulté.
- **Règle 3** : Un médecin qui a plus de 10 consultations dans un service est un médecin expérimenté.
- **Règle 4** : Un patient ayant plus de 5 médicaments prescrits est un patient à surveiller.

---

## 📌 Phases du Projet

| Phase | Description |
|-------|-------------|
| 🧠 Phase 1 | Choix du domaine & concepts clés |
| 🛠️ Phase 2 | Modélisation en RDF/RDFS |
| 🔎 Phase 3 | Requêtes SPARQL |
| 🧬 Phase 4 | Développement en OWL |
| 🧠 Phase 5 | Définition de règles SWRL |

---

## 📝 Conclusion

Ce projet a permis de :

- Appréhender les outils de modélisation sémantique (Protégé, RDF, OWL, SPARQL)
- Structurer un domaine complexe (la santé)
- Effectuer des inférences avancées grâce à SWRL
- Mettre en place un projet collaboratif et documenté via GitHub

🌐 Grâce aux technologies sémantiques, les données deviennent **interopérables**, **intelligentes** et **exploitables** pour l’avenir du Web des données.

---

## 🚀 Ressources

- 🔗 [Protégé Ontology Editor](https://protege.stanford.edu/)
- 🔗 [Wikidata SPARQL Query Service](https://query.wikidata.org/)
- 📖 [W3C RDF Primer](https://www.w3.org/TR/rdf-primer/)
- 📖 [OWL 2 Overview](https://www.w3.org/TR/owl2-overview/)

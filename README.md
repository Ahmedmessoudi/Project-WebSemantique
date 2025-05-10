
# 🏥 Ontologie de la Santé - Mini Projet Sémantique

## 📘 Description Générale

Ce projet s'inscrit dans le cadre de l'exploration du Web sémantique, en utilisant les standards **RDF**, **RDFS**, **OWL**, **SPARQL** et **SWRL**. L’ontologie développée modélise des concepts liés au **domaine médical**, notamment la gestion des professionnels de santé, des patients, des services hospitaliers, des consultations et prescriptions. Elle offre des outils d’analyse basés sur des requêtes SPARQL et des inférences automatiques.

L’ontologie est développée avec **Protégé** et publiée sur GitHub

## 🌐 Justification des Namespaces

| Préfixe | URI |
|--------|-----|
| `xsd` | `http://www.w3.org/2001/XMLSchema#` |
| `dc`  | `http://purl.org/dc/elements/1.1/` |
| `foaf`| `http://xmlns.com/foaf/0.1/` |
| `skos`| `http://www.w3.org/2004/02/skos/core#` |
| `rdfs`| `http://www.w3.org/2000/01/rdf-schema#` |
| `owl` | `http://www.w3.org/2002/07/owl#` |

## 🧠 Modèle Conceptuel Utilisé

### 🔹 Classes Principales

- 👨‍⚕️ **Médecins** : `Medecin` (Type : owl:Class)
- 👩‍⚕️ **Infirmiers** : `Infirmier` (Type : owl:Class)
- 🧑‍🤝‍🧑 **Patients** : `Patient` (Type : owl:Class)
- 🏥 **Services hospitaliers** : `Service` (Type : owl:Class)
- 🧪 **Spécialités médicales** : `Specialite` (Type : owl:Class)
- 🩺 **Consultations** : `Consultation` (Type : owl:Class)
- 🧾 **Dossiers médicaux** : `DossierMedical` (Type : owl:Class)
- 💊 **Médicaments** : `Medicament` (Type : owl:Class)
- 🏨 **Hôpitaux** : `Hopital` (Type : owl:Class)

### 🔸 Sous-classes et Hiérarchies

- `Medecin`, `Infirmier` ⊂ `PersonnelMedical` (Type : owl:Class)
- `Consultation` liée à `Medecin` et `Patient` (via propriétés)

### 🔗 Propriétés et Sous-Propriétés

| Propriété              | Domaine               | Type                |
|------------------------|------------------------|---------------------|
| `aPourNom`             | Personne               | `xsd:string`        |
| `aPourPrenom`          | Personne               | `xsd:string`        |
| `aPourDateNaissance`   | Personne               | `xsd:date`          |
| `travailleDans`        | PersonnelMedical → Service | `owl:ObjectProperty` |
| `aPourSpecialite`      | Medecin → Specialite   | `owl:ObjectProperty` |
| `prescrit`             | Medecin → Medicament   | `owl:ObjectProperty` |
| `aConsulte`            | Patient → Medecin      | `owl:ObjectProperty` |
| `aPourService`         | Consultation → Service | `owl:ObjectProperty` |

## 🧪 Requêtes SPARQL

Les requêtes définies dans [`medica.sparql`](./queries/medica.sparql) permettent de réaliser les opérations suivantes :

| Objectif | Description |
|---------|-------------|
| 👨‍⚕️ Liste des médecins et leurs spécialités | Identifier les domaines d’expertise |
| 😷 Patients diagnostiqués COVID-19 | Suivi des consultations par service |
| 💊 Traitements prescrits par le Dr. Aymen |  Vérifier les traitements prescrits par un médecin spécifique. |
| 🏨 Établissements du Dr. Hicham | Localiser les établissements dans lesquels exerce un médecin. |
| 🧪 Examens médicaux et réalisateurs | Associer les actes médicaux aux professionnels responsables. |
| 🧑‍🤝‍🧑 Relation médecin-patient | Visualiser les liens directs entre praticiens et patients. |


## 🔍 Inférences dans l'Ontologie

- 🧠 Tout médecin travaillant dans un service est implicite membre du personnel du service.
- 📁 Lien implicite entre patient, dossier et service.
- 🧬 Déductions via `rdfs:subClassOf`, `owl:equivalentClass`, etc.

## ⚙️ Règles SWRL

### 1. 🧠 Règle pour les patients nécessitant un IRM
```
Patient(?p) ^ aPourDiagnostic(?p, Diagnostique_cerveau) -> estPrescritPar(ExamenIRM, DrMedAli)
```
- Automatise la prescription d'IRM pour les pathologies cérébrales
- Identifie tout patient avec un diagnostic cérébral
- Attribue l'examen IRM au Dr Med Ali (neurologue)

### 2. 🏥 Règle pour les médecins travaillant dans plusieurs établissements
```
Medecin(?m) ^ TravailleDans(?m, ?e1) ^ TravailleDans(?m, ?e2) ^ differentFrom(?e1, ?e2) -> Specialiste(?m)
```
- Détecte les médecins travaillant dans ≥2 établissements
- Classe ces médecins comme "Spécialistes"
- Utile pour la gestion des consultants externes

### 3. 😷 Règle pour les patients avec COVID-19
```
Patient(?p) ^ aPourDiagnostic(?p, Diagnostique_COVID19) -> prescrit(DrAymen, Traitement_Paracetamol)
```
- Déclencheur : diagnostic COVID-19
- Action : prescription automatique de paracétamol par Dr Aymen

### 4. 📋 Règle pour lier les examens médicaux à leurs patients
```
ExamenMedical(?e) ^ estRealisePar(?e, ?prof) ^ ProfessionalDeSante(?prof) ^ aPourPatient(?med, ?p) ^ Medecin(?med) -> aPourDiagnostic(?p, ?e)
```
- Automatise l’enregistrement des examens en diagnostics
- Valide le lien entre patient, examen, médecin et personnel

### 5. 🧬 Règle pour détecter les médecins Neuro
```
Medecin(?m) ^ aPourSpecialite(?m, Pathologie_Neuro) -> ProfessionalDeSante(?m)
```
- Classe tout médecin neurologue comme professionnel de santé
- Assure la hiérarchie des spécialités


## 🧾 Architecture du Projet

```
📦 sante-ontologie/
 ├── docs/
 ├── ontology/
 │   ├── sante ontologie.rdf
 │   └── sante ontologie.owl
 ├── queries/
 │   └── medica.sparql
     └── SWRL queries.txt
 ├── schemas/
 └── README.md
```

## ✅ Apports de l’Ontologie

- 🧱 Structuration du domaine santé.
- 🔄 Inférences automatiques utiles pour l’analyse.
- 🔎 Interrogation précise via SPARQL.
- 🌍 Base pour des systèmes intelligents d’aide à la décision.

## 📤 Déploiement

- 📅 Projet publié sur GitHub .
- 🗃️ Fichiers RDF/OWL, SPARQL et doc partagés.

## 📚 Ressources Utiles

- 🛠️ [Protégé](https://protege.stanford.edu/)
- 📘 [W3C OWL Guide](https://www.w3.org/TR/owl2-overview/)
- 🔎 [Wikidata SPARQL Service](https://query.wikidata.org/)
- 📄 [SWRL Rules Overview](https://www.w3.org/Submission/SWRL/)

---

*🧬 Vers une médecine sémantique plus intelligente et connectée...*

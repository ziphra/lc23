- [Day 1](#day-1)
  - [Genomics England long-read cancer whole-genome sequencing pilot, Helenn Webb](#genomics-england-long-read-cancer-whole-genome-sequencing-pilot-helenn-webb)
  - [A single-cell approach to cancer mutation discovery and CRISPR phenotypic modelling, Hanlee Ji](#a-single-cell-approach-to-cancer-mutation-discovery-and-crispr-phenotypic-modelling-hanlee-ji)
  - [Real-time genomics for One Health, Lara Urban](#real-time-genomics-for-one-health-lara-urban)
  - [Breakout Session: methylation and phasing](#breakout-session-methylation-and-phasing)
  - [Update from the Applications team, Dan Turner, SVP, Applications](#update-from-the-applications-team-dan-turner-svp-applications)
  - [The Emirati Genome Project: where long reads became an integral part of large genome projects (a first!), Tiago R. Magalhães](#the-emirati-genome-project-where-long-reads-became-an-integral-part-of-large-genome-projects-a-first-tiago-r-magalhes)
  - [RNA update](#rna-update)
  - [Update fron ONT](#update-fron-ont)
- [Day 2](#day-2)
  - [Data for breakfast](#data-for-breakfast)
  - [scNanoATAC-seq: a long-read single-cell assay to simultaneously detect chromatin accessibility and genetic variants, Fuchou Tang](#scnanoatac-seq-a-long-read-single-cell-assay-to-simultaneously-detect-chromatin-accessibility-and-genetic-variants-fuchou-tang)
  - [Population-scale nanopore sequencing to further understand the genetics of Alzheimer’s disease and related dementias, Kimberley Billingsley](#population-scale-nanopore-sequencing-to-further-understand-the-genetics-of-alzheimers-disease-and-related-dementias-kimberley-billingsley)
  - [Data Analysis Tool: variant analysis](#data-analysis-tool-variant-analysis)
  - [Galapagos Genetic Barcode: a model for island economic resilience during the COVID-19 pandemic, Jaime Chaves](#galapagos-genetic-barcode-a-model-for-island-economic-resilience-during-the-covid-19-pandemic-jaime-chaves)
  - [The future of clinical genomics](#the-future-of-clinical-genomics)
- [workshop: an introduction to machine learning](#workshop-an-introduction-to-machine-learning)
  - [coder un basecaller](#coder-un-basecaller)
  - [coder un machine learning based variant caller](#coder-un-machine-learning-based-variant-caller)












## Day 1
### Genomics England long-read cancer whole-genome sequencing pilot, Helenn Webb
Genomics England mène actuellement une étude pilote pour examiner l'utilisation du séquençage long read Nanopore pour l'analyse à grande échelle du génome entier en clinique, pour le cancer. Ce projet pilote est réalisé en collaboration avec le NHS England.

Les objectifs :

- Diagnostics rapides
Données complètes : un LR-WGS au lieu de plusieurs tests (WGS, panels, méthylation et CNV arrays) et en moins de deux semaines.
- L'évaluation concurrentielle des outils de séquençage et d'analyse
- Accès démocratisé et équitable au WGS 

En préparation de ce projet pilote, de vastes cohortes ont été séquencées pour permettre d'optimiser les protocoles de séquençage sur des PromethIONs 48 et les pipelines d'analyse.
L'appel des variants de structure a été optimisé suite à l'évaluation comparative de plusieurs algorithmes.

Ce benchmarking a été effectué sur des échantillons de cancer, et la précision a été calculée par rapport aux résultats obtenus en FISH. 

| **SV Caller**       | Runtime (min/median/max) | Recall for SVs in clinically relevant gene | FP rate in clinically relevant gene |
|---------------------|--------------------------|--------------------------------------------|-------------------------------------|
| **NanomonsSV v0.4** | 6/17/41                  | 99                                         | low                                 |
| **Sniffles2.2**     | 12min/19min/56min        | 79                                         | moderate high                       |
| **CuteSV v1.0.13**  | 1/4/5.5                  | 48                                         | moderate                            |
| **SAVANA V0.2.4**   | 36min/1/3                | 96                                         | low                                 |

Bonne couverture dans des régions de low copy repeat et dans des SINES, ce qui permet la détection de variants de fusion détectables en LR mais pas en SR:


Pour des échantillons tumoraux avec une pureté supérieure à 80%, la sensibilité du calling des SNVs est de 90% avec **ClairS** - ce qui semble faible en clinique.

Pour le calling des CNVs, ils utilisent **CNVpytor**.

### A single-cell approach to cancer mutation discovery and CRISPR phenotypic modelling, Hanlee Ji
<https://genomebiology.biomedcentral.com/articles/10.1186/s13059-021-02554-1#Sec13>    
D'abord, il identifie les mutations somatiques sur un MinION par adaptive sampling nanopore d'ARNc grâce aux reads couvrant toute la longueur du transcrit.
Puis, avec CRISPR, il transfecte ces mutations pour caractériser leur phénotype en utilisant également le séquençage SR couplé au LR. Il utilise des barcodes correspondants entre LR et SR pour multiplexer à grande échelle. (2 \$ par échantillon...)
Utilise [LongShot](https://github.com/pjedge/longshot) pour le variant calling des SNVs. LongShot appelle seulement les SNVs, pas les indels. 

### Real-time genomics for One Health, Lara Urban
*One Health* est un concept montrant que la santé publique et la situation environnementale sont intimement liées. Lara Urban présente comment ONT, en permettant le séquençage rapide en temps réel, permet la mise en place de stratégies d'intervention rapide en matière de santé environnementale.
Par exemple:

- Le monitoring de pathogènes
- La sécurité alimentaire
- La conservation des espèces
- ...

Son équipe a utilisé la méthylation de l'ADN pour distinguer, dans un cours d'eau, les microorganismes morts des vivants, permettant ainsi d'identifier la réelle diversité d'un microbiome à un moment précis.

### Breakout Session: methylation and phasing 
#### Nanomix: methylation-based cell-type deconvolution for low-pass nanopore sequencing
[GitHub](https://github.com/Jonbroad15/nanomix)
Nanomix est un outil qui permet d'assigner à chaque read son type cellulaire en utilisant les informations de méthylation. Une couverture de 1X suffit pour faire fonctionner le modèle.
Cet outil permet de décomposer la composition en ADN d'un échantillon, par exemple pour tester la pureté d'un échantillon tumoral ou analyser l'ADN circulant. 

#### Genome-wide single-molecule analysis of DNA methylation by nanopore sequencing reveals heterogeneous patterns at heterochromatin, Lindsay Kerr
<https://www.biorxiv.org/content/10.1101/2022.11.15.516549v2>    
Lindsay Kerr étudie la méthylation de l'ADN par molécule (et non en moyennant la présence ou l'absence de méthylation à une position en vrac de l'ADN). Pour cela, elle utilise des ultra-LR (~25 kb). Ainsi, elle a pu mettre en évidence la présence de motifs périodiques de méthylation dans les régions d'hétérochromatine.

#### MeOW: genome-wide identification of differentially methylated regions using Oxford nanopore long-read sequencing data, Miranda Galey
MeOW est un outil permettant d'identifier les DMRS (differentially methylated regions) à partir des fichiers BAM d'alignement de LR nanopore.
Le minimum de couverture requis est de 30X.
L'outil semble permettre de générer une base de données des îlots CpGs et de leur fréquence de méthylation.
Il permet l'application de tests statistiques et génère des graphiques des DMRs. 

#### MethPhaser: automated methylation-based haplotype phasing of human genomes with Oxford Nanopore sequencing, Fritz Sedlazeck
[MethPhaser](https://gitlab.com/treangenlab/methphaser) est un outil utilisant les SNPs et la méthylation de l'ADN pour le phasing de l'haplotype. 
Cette méthode ne peut être utilisée que pour le phasing des autosomes. 

### Update from the Applications team, Dan Turner, SVP, Applications
- Le séquençage nanopore permet de détecter precisement les variants :    

| SNVs | Indels dans les régions codantes* | SVs  |
|------|-----------------------------------|------|
| 99.8 | 99.2                              | 96.2 |

\* concentrent 96.4% des variants pathogènes. 
F1 mesuré à 60X. 

- SkimSeq: WGS à faible couverture    
Le low pass sequencing (~ 0.5-5X) couplé à des méthodes d'imputation bioinformatique (voir [QUILT](https://github.com/rwdavies/QUILT), permet de prédire le génotype à partir d'un large panel de références. Les reads les plus courts donnent les meilleurs résultats (500 pb) car des reads plus courts augmentent les chances de séquencer les deux allèles en faible couverture.
Ainsi, il est possible de prédire certains risques polygéniques à moindre coût en multiplexant à grande échelle.

 
### The Emirati Genome Project: where long reads became an integral part of large genome projects (a first!), Tiago R. Magalhães
Ce projet a pour ambition de séquencer les 1 million d'Émiratis en utilisant la technologie Nanopore avec une profondeur de 30X, et de construire un génome de référence émirati.
Leur infrastructure comprend notamment 41 PromethIONs.

### RNA update 
Présentation du nouveau kit de séquençage ARN, SQK-RNA004   

- nouveau pore RP4, avec une meilleure durée de vie 
- protéine motrice deux fois plus rapide (augmente le débit)
- plus de précision

### Update fron ONT
- Annonce du séquençage du génome humain à 200 dollars, avec des flow cells capables de produire 400 Gb de données (100 Gb actuellement) et une capacité de séquençage de +9 900 génomes par an sur un P24...
- Jusqu'à 85% de taux de duplex reads avec les high duplex flow cells (développer release en cours), et séquençage à Q32 à 5 kHz.
- Le dernier basecaller Dorado sera intégré dans MinKNOW courant juillet, ce qui permettra de faire le basecalling en temps réel sur le PromethION.
- Présentation d'une nouvelle stratégie pour le séquençage des homopolymères :
- Modifier certaines bases de l'homopolymère (A -> A*) permet de créer une copie qui ne soit plus homopolymérique. En ajoutant des informations à la séquence, cela va permettre de décoder le signal d'origine.
- Nouveau kit RNA-0004.
- P2 (PromethION à 2 flow cells) : 10 000 dollars.
- De nouveaux buffers de séquençage sont en développement. Leur composition est connue pour affecter le séquençage en bloquant les pores. Cela permettra d'améliorer le débit (+30%).
Séquençage sur MinION bientôt possible sur iPad.
- Nouvelle puce ASIC permettra la mise en place de nouveaux séquenceurs encore plus petits (séquençage sur iPhone...).
- Le Traxion : petit appareil contenant tous les réactifs pour la préparation d'une librairie, à charger avec son échantillon et à brancher directement sur la flow cell.
Séquençage de protéines...

## Day 2
### Data for breakfast
#### Dorado
- Dorado produit désormais des BAM alignés avec Minimap2.
- Produit un sequencing_summary.txt, comme avec Guppy.
- Intégré à MinKNOW en juillet, donc utilisable en temps réel sur le séquenceur.
- Duplex basecalling fait automatiquement par l'intermédiaire d'une seule commande.
Plus rapide, plus précis.

#### Nextflow and Epi2me 
- Il semble possible de faire tourner son propre workflow sur Epi2me Labs. Cela permettrait d'automatiser le pipeline. 

### scNanoATAC-seq: a long-read single-cell assay to simultaneously detect chromatin accessibility and genetic variants, Fuchou Tang
<https://www.nature.com/articles/s41422-022-00730-x>

### Population-scale nanopore sequencing to further understand the genetics of Alzheimer’s disease and related dementias, Kimberley Billingsley
<https://www.biorxiv.org/content/10.1101/2023.01.12.523790v1>
K. Billingsley et son équipe ont développé un pipeline d'analyse pour le WGS de larges cohortes en utilisant conjointement une approche d'alignement et une approche d'assemblage de novo.

Le workflow CARD Terra permet ainsi de :

- Détecter les SNPs avec un score F1 meilleur qu'avec les SR Illumina.
- Le calling des indels dans les régions d'homopolymères et de tandem repeat reste complexe, mais il est comparable aux SR Illumina.
- Identifier les SV avec un score F1 comparable à ce qui est réalisé en PacBio, mais à moindre coût. 


### Data Analysis Tool: variant analysis 
#### Spectre, CNV caller, Luis Paulin
- Basé sur la couverture.
- Spécialisé pour détecter les larges CNVs avec des breakpoints imprécis, par exemple dans les régions télomériques ou centromériques manquées par Sniffles2.
- Utilise des bins de 1 kb et supprime les régions "blacklistées".

#### SAVANA: a computational method to characterise structural variation in human cancer genomes using nanopore sequencing, Hillary Elrick
- Sniffles2 à l'air très mauvais pour les cancers

#### Precise characterization of somatic complex structural variations from paired long-read sequencing data using nanomonsv, Yuichi Shiraishi
<https://github.com/friend1ws/nanomonsv>
- 'Paired' signifie ici avec des échantillons de tumeurs et des échantillons contrôles.
- 
#### Ultra-rapid nanopore sequencing: computational pipeline 2.0, Sneha Goenka (from the ultra rapid Nature paper)
- Peut générer une liste de variants 2h après le séquençage, pour 180Gb de données.
- La sélection des variants est automatisée avec le programme GEM de Fabric Genomics.
N'utilise pas de GPU pour le variant calling avec PMDV (rapport coût/vitesse peu intéressant).

### Galapagos Genetic Barcode: a model for island economic resilience during the COVID-19 pandemic, Jaime Chaves
Galapagos Genetic Barcode est un projet qui vise à former les habitants locaux de l'île aux techniques de séquençage pour mesurer sa biodiversité. 

### The future of clinical genomics 
#### Empowering NHS rapid diagnostic testing with long-read DNA sequencing, Emma Baple
Le service de séquencage complet pour les enfants aux Royaume-Uni permet le diagnostic de 41% de ces patients en moins de 10 jours.

#### Nanopore sequencing as a potential diagnostic tool for genetic diseases in the Middle East, Ahmad Abou Tayoun

#### Potential use of nanopore sequencing in clinical cancer genomics, Janessa Laskin
Le programme Personalized OncoGenomics (POG) au Canada intègre l'analyse du génome entier et du transcriptome pour les patients atteints de cancers avancés. Une étude a démontré les avantages du séquençage LR et son application prospective dans le cadre du programme POG.









_______





## workshop: an introduction to machine learning 
### coder un basecaller 
- à partir d'un fichier signal json
- et de la kmer_table qui associe l'intinsité du signal avec chaque dimère: 
```
{"AA": 0.0, "AC": 0.0625, "AG": 0.125, "AT": 0.1875, "CA": 0.25, "CC": 0.3125, "CG": 0.375, "CT": 0.4375, "GA": 0.5, "GC": 0.5625, "GG": 0.625, "GT": 0.6875, "TA": 0.75, "TC": 0.8125, "TG": 0.875, "TT": 0.9375}
```

#### étapes
- Identifier les transitions dans le signal
- Calculer la valeur moyenne du signal
- Calculer la distance euclidienne entre chaque événement et chaque dimer, et selectionner le dimer à la distance la plus faible
- Associer chaque événement avec son dimer 


### coder un machine learning based variant caller
- avec un pytorch convulotional network 


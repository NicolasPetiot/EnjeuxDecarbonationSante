# Enjeux de la Décarbonation en Santé

Le design de protéines est un domaine en pleine expansion qui repose sur la compréhension des principes du repliement et de la stabilité des protéines. L’émergence des outils bioinformatiques, combinée aux avancées en ingénierie génétique, a transformé une discipline essentiellement expérimentale en un champ où la conception assistée par ordinateur et l’édition génomique jouent un rôle central. L’étude des protéines a d’abord reposé sur des approches expérimentales. La cristallographie aux rayons X, qui a révélé les premières structures tridimensionnelles (myoglobine en 1958, hémoglobine en 1960), a posé les bases de la compréhension des interactions qui stabilisent les protéines. Dans les années 1970, Christian Anfinsen a notamment étudié la thermodynamique du repliement et a montré que la structure d’une protéine est déterminée par sa séquence d’acides aminés. Dès les années 1980, les premières tentatives de modélisation par ordinateur ont émergé avec des outils basés sur la dynamique moléculaire (CHARMM, AMBER) et des approches  énergétiques visant à prédire la structure d’une protéine à partir de sa séquence. Cependant, ces méthodes restaient limitées par la puissance de calcul et la complexité du repliement des protéines. Dans les années 1990, les premiers outils spécifiquement dédiés au design de novo des protéines ont été développés. Un tournant majeur a été l’apparition du logiciel ROSETTA, conçu par David Baker et son équipe, qui a permis la conception de protéines totalement nouvelles (Top7 en 2003). Ce logiciel, en combinant des approches de modélisation énergétique et de minimisation conformationnelle, a ouvert la voie à la création de protéines avec des fonctions ciblées.

En parallèle, l’essor de la biologie de synthèse a été accéléré par le développement du système CRISPR-Cas9 qui permet de modifier, insérer ou supprimer des gènes avec une précision inégalée, facilitant ainsi l’ingénierie de protéines in vivo. Il est, entre autres, utilisé aujourd’hui pour optimiser des protéines conçues grâce à la bioinformatique, accélérant leur validation et leur intégration dans des cellules modifiées. 

Depuis les années 2010, le design de protéines a connu une accélération spectaculaire grâce aux avancées en intelligence artificielle et en apprentissage profond. L’apparition d’AlphaFold2 (DeepMind, 2020), capable de prédire des structures avec une précision comparable à celle des méthodes expérimentales, a bouleversé le domaine. Plus récemment, des modèles de design génératif, comme ProteinMPNN ou RFdiffusion, permettent désormais de concevoir des protéines aux fonctions inédites, ouvrant des perspectives en santé, biotechnologie et matériaux bio-inspirés. L’intégration de l’IA, de CRISPR et des outils de bioinformatique crée aujourd’hui un écosystème où la conception et l’application de nouvelles protéines se font à une vitesse inégalée.

Les Glutathion Transferase (GST) forment une super-famille de protéines  omniprésentes et multifonctionnelles. Leur rôle principal est de catalyser la réaction de conjugaison entre le Glutathion (GSH) et un xénobiotique pour l’éliminer. L’interaction entre les insectes et composés phytochimiques crée une pression de sélection très importante qui favorise le développement de protéines de détoxication très efficaces et versatiles. Par exemple, la *Drosophila melanogaster* possède 36 GST différentes réparties en 6 classes, ce qui fait de ce protéome un ensemble de choix pour la création d’enzymes aux propriétés catalytiques nouvelles ou améliorées. Ce travail pratique vise donc à présenter une analyse d’une GST de la classe Delta à travers divers outils d’analyse bioinformatique ainsi qu’une procédure d’optimisation de la séquence dans le but de créer une nouvelle GST. 

# Travail Pratique:
## 1. Relation Séquence-Structure

L'ensemble des structures de protéine résolues expérimentallement est répertorié dans la base de donnée [Protein Data Bank](https://www.rcsb.org/) et contient à peu près 240 000 structures tandis que l'ensemble des centaines de millons de séquences connues est répertorié dans la base de données [Uniprot](https://www.uniprot.org/). Dans un premier temps:

- Identifiez la séquence d'acide aminé de la GSTD1 de la *Drosophila melanogaster* ainsi que la/les éventuelles structures expérimentales

- Réalisez à l'aide d'[AlphaFold](https://alphafoldserver.com/) une prédiction de structure pour cette séquence de protéine. 

**Attention**, la GSTD1 est homodimérique. Celà signifie que sa structure contient deux copies de la même chaine protéique.

- À l'aide du logiciel de visualisation PyMOl, comparez globalement votre prédiction de structure avec la structure [*3EIN*](https://www.rcsb.org/structure/3EIN) téléchargeable au format **PDB**. Que remarquez-vous ?

- Où se situe le Glutathion ? Donnez un ensemble d'acides aminés en contact avec ce dernier.

![image](img/3EIN_Gsite.png)

**Aide**: On peut dans un premier temps essayer d'identifier les acides aminés avec PyMol, puis utiliser les script `contacts.ipynb` qui permets d'identifier les acides aminés de manière automatique.

## 2. Affinité Protéine-Ligand

En principe, une enzyme fonctionelle doit être capable de capter ses réactifs avec une bonne affinité pour faciliter la rencontre entre les réactifs. La prédiction de cette affinité est aujourd'hui un facteur déterminant pour la conception *in silico* d'enzyme artificielle. Le logiciel de modélisation moléculaire ROSETTA contient un ensemble de fonctionalité qui permettent justement un tel calcul. On appelle **Affinité de Liaison** la quantité

$$
    \Delta G = G_{\text{lié}} - G_{\text{séparé}}
$$

où $G$ est l'énergie du système, prenant en compte la protéine et le ligand. Dans l'état lié, le ligand se trouve dans son site de fixation tandis que dans l'état séparé, le ligand n'interagit plus du tout avec la protéine. La quantité $\Delta G$ s'interprête alors comme la quantité d'énergie à apporter au système pour arracher le ligand de son site de fixation. Si $\Delta G \ge 0$, le système dans son état séparé est plus stable, ce qui signifie que la protéine repousse son ligand. On observe en général des $\Delta G < 0$ et l'affinité Protéine-Ligand est d'autant plus forte que $\Delta G$ est négatif. 

- À partir du script `rosetta_affinity.ipynb`, calculez l'énergie de la structure `GSTD1+GSH.pdb`.
- À l'aide du logiciel PyMol et de la commande [drag](https://pymol.org/dokuwiki/doku.php?id=command:drag), créez une structure `GSTD1+GSH_split.pdb`.
- Estimez ainsi l'affinité GSTD1-GSH

**Aide**: Par la suite, on pourra utiliser la fonction `binding_affinity` qui implémente cette même logique et retourne directement la valeur d'affinité en Unité d'Energie de Rosetta (REU).

- Vérifiez que la fonction `binding_affinity` donne une valeur similaire à celle obtenue précédemment.

## 3. Exploration dans l'espace des Séquences de la GSTD1

Additionellement, les GSTs possèdent un acide aminé dit "actif" (Serine n°10 pour la GSTD1) qui interagit avec l'Hydrogène du GSH pour faciliter sa supture de liaison covalente avec le Souffre. Le rôle des autres acides aminés du site actif est aujourd'hui beaucoup moins documenté 

![image](img/GSH_conjuguation.svg)



# Practical Session #1: Introduction

1. Find in news sources a general public article reporting the discovery of a software bug. Describe the bug. If possible, say whether the bug is local or global and describe the failure that manifested its presence. Explain the repercussions of the bug for clients/consumers and the company or entity behind the faulty program. Speculate whether, in your opinion, testing the right scenario would have helped to discover the fault.

2. Apache Commons projects are known for the quality of their code and development practices. They use dedicated issue tracking systems to discuss and follow the evolution of bugs and new features. The following link https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-794?filter=doneissues points to the issues considered as solved for the Apache Commons Collections project. Among those issues find one that corresponds to a bug that has been solved. Classify the bug as local or global. Explain the bug and the solution. Did the contributors of the project add new tests to ensure that the bug is detected if it reappears in the future?

3. Netflix is famous, among other things we love, for the popularization of *Chaos Engineering*, a fault-tolerance verification technique. The company has implemented protocols to test their entire system in production by simulating faults such as a server shutdown. During these experiments they evaluate the system's capabilities of delivering content under different conditions. The technique was described in [a paper](https://arxiv.org/ftp/arxiv/papers/1702/1702.05843.pdf) published in 2016. Read the paper and briefly explain what are the concrete experiments they perform, what are the requirements for these experiments, what are the variables they observe and what are the main results they obtained. Is Netflix the only company performing these experiments? Speculate how these experiments could be carried in other organizations in terms of the kind of experiment that could be performed and the system variables to observe during the experiments.

4. [WebAssembly](https://webassembly.org/) has become the fourth official language supported by web browsers. The language was born from a joint effort of the major players in the Web. Its creators presented their design decisions and the formal specification in [a scientific paper](https://people.mpi-sws.org/~rossberg/papers/Haas,%20Rossberg,%20Schuff,%20Titzer,%20Gohman,%20Wagner,%20Zakai,%20Bastien,%20Holman%20-%20Bringing%20the%20Web%20up%20to%20Speed%20with%20WebAssembly.pdf) published in 2018. The goal of the language is to be a low level, safe and portable compilation target for the Web and other embedding environments. The authors say that it is the first industrial strength language designed with formal semantics from the start. This evidences the feasibility of constructive approaches in this area. Read the paper and explain what are the main advantages of having a formal specification for WebAssembly. In your opinion, does this mean that WebAssembly implementations should not be tested? 

5.  Shortly after the appearance of WebAssembly another paper proposed a mechanized specification of the language using Isabelle. The paper can be consulted here: https://www.cl.cam.ac.uk/~caw77/papers/mechanising-and-verifying-the-webassembly-specification.pdf. This mechanized specification complements the first formalization attempt from the paper. According to the author of this second paper, what are the main advantages of the mechanized specification? Did it help improving the original formal specification of the language? What other artifacts were derived from this mechanized specification? How did the author verify the specification? Does this new specification removes the need for testing?

## Answers


1.
Source : https://www.theregister.com/2015/01/17/scary_code_of_the_week_steam_cleans_linux_pcs/
En 2015 un bug de l'application Steam de Valve sur Linux pouvait supprimmer tous les fichiers de l'ordinateur.
Les repercussions vers l'utilisateur sont trés grande (perte de documents).
La cause de l'erreur vient de  :
```
STEAMROOT="$(cd "${0%/*}" && echo $PWD)"


rm -rf "$STEAMROOT/"*
```

Il aurait fallu mieux encadrer la valeur STEAMROOT car si elle est vide rm -rf est lancé à la racine de l'ordinateur.
Un simple test aurait pu alerter sur la dangerosité d'une telle commande.


2.  Bug :
https://issues.apache.org/jira/projects/COLLECTIONS/issues/COLLECTIONS-775?filter=doneissues

Le bug a l'air local, il venait d'une erreur de compréhension de l'Iterateur de Collection de JAVA

Dans les commentaires nous pouvons voir qu'un nouveau test à été mis en place pour repérer cette erreur.


3. Le papier présente le Chaos Engineering, le but est de stopper des instances de machines virtuelles contenant des services grâce à des Chaos Monkeys et de montrer la fiabilité de l'infrastructure même en cas de pannes. Pour ces expérimentations il faut une infrastructure solide et une automatisation des pannes et des transferts de charges.
Ce principe peut être interessant dans plusieurs domaines, nottament dans le cas d'un groupe d'ordinateurs d'un véhicule si un appareil vient à s'interrompre il pourrait être remplacé par d'autres le temps qu'un arrêt sécurisé ou une réparation est faite.


4.  La spécification formelle permet de simplifier l'utilisation d'un outils mais il faut tout de même tester et vérifier sa bonne utilisation/implémentation.

5.  la spécification mécanisée permet la construction de preuves pour tester le bon fonctionnement de l'outil.

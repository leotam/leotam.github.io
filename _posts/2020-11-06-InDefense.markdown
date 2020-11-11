---
layout: post
title: "In defense of Wittgenstein's conception of language in the age of AI"
date: 2020-11-06 16:19:00
categories: general
---
![pain]({{ site.url }}/assets/pain.png)
*Querying OpenAI's 345M parameter GPT-2 model, [courtesy AllenNLP](https://demo.allennlp.org/next-token-lm?text=What%20did%20you%20do%20before%20you%20felt%20pain%3F).  Wittgenstein has extensive discussions of pain vis-à-vis the possibility of private sensations.  For a significant part of history, infants were not deemed to feel pain in a significant way as they could not express it in language<sup>1</sup>.*

In the measures of AI, Turing's criterion on intelligence, the Turing test, and related computational foundations, the Turing machine, loom large over progress towards a general intelligence.  Given satisfaction for some of Turing's requirements in [recent work](https://arxiv.org/abs/1807.03819), Turing's philosophical contributions may be lateral as contrasted with Wittgenstein's philosophy of language.  In particular, we focus on Wittgenstein's later *Philosophical Investigations*, a manuscript that reads as a collection of first principles koans than a traditional logical elucidation (superseding his earlier *Tractatus Logico-Philosophicus*). As first described by Hofstadter's *Gödel, Escher, Bach*, koans act as a paradigm-shattering inducement to break through the (Gödel) Incompleteness of axiomatic thought, such as the language dimensions that form our experience of the world.  Wittgenstein's work prescribes a path forward for the development of one pillar of general intelligence (in concert with the External World problem and Other Minds paradigm)<sup>2</sup>.

> What is your aim in philosophy? –To show the fly the way out of the fly bottle.

*§309. Philosophical Investigations*

As a precocious genius, Wittgenstein was raised with the cultural elite of Vienna as afforded by a captain of industry patriarch.  He continued seeking the best teachers, landing on Bertrand Russell's doorstep to launch his philosophy career as an undergraduate. Like the personage who first inspired koans, Wittgenstein gave up family fortune to think deeply by retreating to the desolate Norwegian landscape.  Publishing a master work on language posthumously, his most famous results spring from the repeated characterization of the *language-game*, in short the context of words, life, and actions that surround the real use of language that define humanity and the human experience. Such results are especially relevant in lieu of recent advances in natural language processing, in the specific and general, i.e. named entity recognition and negation cast in light of categorization and representation learning faculties. Wittgenstein's investigations delineate some successes of the neural network approach, cast the Turing test as perhaps a paper tiger, and recenter progress towards the language game as a pillar of general intelligence.

![glue]({{ site.url }}/assets/supergluetop3.png)
*The top 3 NLP language models as evaluated on a collection of tasks ([SuperGLUE](https://super.gluebenchmark.com/leaderboard)) involving logic. Does each task represent a language game as described by Wittgenstein?*

> Yet, strange to say, the word "this" has been called the only genuine name; so that anything else we call a name was one only in an inexact, approximate sense.

*§38. Philosophical Investigations*

NLP algorithms excel at named entity recognition *in situ* as evidenced by the lexical task of coreference resolution (WSC) in the above figure. Yet tasks more characteristic of language games would bring us to Question and Answering in Context <https://quac.ai/>, which surveys multi-round interactions centered on learning.  Modern algorithms still fall short in the interactive learning tasks of language use. Wittgenstein provides an assistive metaphor describing language games in relation to each other as recursive and adjacent (§64), perhaps such as cities and towns growing to form a vital nation.  Work from Berkeley <https://arxiv.org/abs/2010.11967> explicitly renders an open knowledge graph from language models, a natural consequence of the language game paradigm.  Recent analyses of language models for task transfer decompose into primary functions such as lexical and syntactical <https://arxiv.org/abs/1906.04341>. Again, Wittgenstein predicted these primary elements (§46).  Wittgenstein further conceives the act of reading as guiding (§171-178), a form that meshes well with sequence processing of text modulating neural network weights.  Language games capture structural aspects of modern NLP.

> To understand a sentence means to understand a language. To understand a language means to be master of a technique.

*§199. Philosophical Investigations*

In concert with corroborative predictions, Wittgenstein has prescriptive items underlined by language games. Some emerging work has focused on language games ringed by motivation.  The work from Georgia Tech <https://arxiv.org/abs/2010.00685> involves a "system that (1) incorporates large-scale language modeling-based and commonsense reasoning-based pre-training to imbue the agent with relevant priors; and (2) leverages a factorized action space of action commands and dialogue, balancing between the two."  How would Wittgenstein conception of language guide such research?  His concluding thoughts in §630 demarcate:

> Examine these two language-games:
(a) Someone gives someone, else the order to make particular movements with his arm, or to assume particular bodily positions (gymnastics instructor and pupil). And here is a variation of this language-game: the pupil gives himself orders and then carries them out.
(b) Someone observes certain regular processes—for example, the reactions of different metals to acids—and thereupon makes predictions about the reactions that will occur in certain particular cases.
There is an evident kinship between these two language-games, and also a fundamental difference. In both one might call the spoken words "predictions". But compare the training which leads to the first technique with the training for the second one.

His analysis indicates inspection of the games and their relation when training as the herald of the next level of human-like performance.  Further there's a particular stress on domain-specific problems. The difference Wittgenstein marks is that task-level evaluations may obscure granular and game-centric approaches towards successful performance.

§551 delves into the subtleties of negation – "Does the same negation occur in: 'Iron does not melt at a hundred degrees Centigrade' and 'Twice two is not five'?"  Wittgenstein intimates even though the examples are of two different domains, one reconciled by factual world knowledge and the other by axiomatic arithmetic, the resolution of negation is in the playing of the language game. Work on [domain specific language models](http://leotam.github.io/general/2020/04/16/A-Simple-Query-Target-Knowledge-Discovery-Method-on-CORD-19.html) implicates negation emerging from domain corpus is required for successful performance. §556 describes an almost vector quantity for negation, which a transformer query-target NLP model captures well via the strength of associated attention mechanisms.

## Criticisms

A critical examination of Wittgenstein's ideas isolates his definition and rejection of a private language, which in his thought experiments run contrary to the notion of the language game.  In one popular example §293, his thought experiment of the beetle box, a simulacrum of an internal processes labeled by the individual as a 'beetle' would not hold correspondence across individuals in the way an actual 'beetle' would.  The strongest empirical criticism arrives via [Majid et. al.](https://www.cambridge.org/core/journals/natural-language-engineering/article/uncovering-the-language-of-wine-experts/9BF0A599B49230297FD6DBA01F07C0DD) probing the diverse olfactory palette as labeled by the language of expert palates.  The evidence ostensibly contradicts Wittgenstein's analysis as olfaction precedes and supersets language.  Here more modern understanding of anatomical and evolutionary differences suggests a way out.  Olfaction is a unique sense in that it impinges directly on a singular structure, the olfactory bulb, its function tracing as old as living cells performing chemotaxis. The olfactory bulb then impinges directly on the amygdala (emotion) and hippocampus (memory) to induce the unique effect captured eloquently by Proust's madeleine. Olfaction may predate the structures of higher intelligence animated by language.

Does the rejection of a private language match the results from AI language models? The distinction lies on a continuum of weak to strong inferences on whether the internal processes constitute the programming language, the neural network architecture, or the relation of the network parameters themselves once trained on a dataset.  Only the strongest definition of a private language in terms of parameter gradients flows shrug off easily definable aspects.  In the end, Wittgenstein's emphasis on the language game obviates the detour into semantics by focusing on results.

Results-based behaviorist reductionism is addressed directly by Wittgenstein in §307.  His argument hinges on while his statements walk in line with a behaviorist interpretation, the argument precedes behaviorist thought in structure. Wittgenstein writes, "Aren't you at bottom really saying that everything except human behavior is fiction? –If I do speak of a fiction, then it is of a grammatical fiction." (§307)  The behaviorist statement is the pith of the Turing test, and Wittgenstein's language games go a step beyond.

<div style="text-align:center"><img src="{{ site.url }}/assets/markov.svg.png" /></div>
*Pre-language infants and many non-human intelligences more resemble state machines governed by markov processes than rational individuals.<sup>3</sup>*

## Outlook
In §250, Wittgenstein asks if a dog could simulate pain, "Perhaps it is possible to teach him to howl on particular occasions as if he were in pain, even when he is not. But the surroundings which are necessary for this behavior to be real simulation are missing."  Engendering general intelligence is transmuting the common intelligence into human.  If Wittgenstein's language games are taken at face value, it means socializing intelligence. In §650, Wittgenstein expounds the mainstay of child development as we transition from state machines to beings tempered by temporal expectation, and prior in §649, hinting at language as instrumental in the conclusion of infant amnesia.  An amazing result in neural networks use is that [language models "forget"](https://ieeexplore.ieee.org/abstract/document/9206891?casa_token=BE7y3xU-qKIAAAAA:hSn1KJkP6DuyZMnk-kAtJKzZ0B5ATvPE_2Rg4j-xKYRolIZq3V8iJM2OMRVVihNOce4EofMWOECV) just as humans do (in parlance of §57, the instrument of the language game is lost).  General intelligence may happen in a singularity, but Wittgenstein's prediction is that advances bounded by language happen in an interactive, constructive format. As is the case with humans, scalability is countered by Malthusian obstacles within players of the game.  Even with massive computational abilities, the External World (sensation transmutation for the individual) and Other Minds conception are lockstep requisites for general intelligence to play the language game. General intelligence, as wrought by language advances, may be more human than we think.




<sup>1</sup> "Scientist in the Crib." Gopnik, A., et. al.

<sup>2</sup> <https://pubmed.ncbi.nlm.nih.gov/17381794/>

<sup>3</sup> H. Karp, 2002.

NB.

1. [Techcrunch first reported Wittgenstein's theory influencing Google search results by emphasizing context](https://web.archive.org/web/20140417182620/http://www.wired.com/2010/02/ff_google_algorithm/2/)

2. [Additional annotations on *Philosophical Investigations*](https://www.pdfdrive.com/download.pdf?id=186579219&h=8224149cb39300735eae1b4a1bde45f6&u=cache&ext=pdf)

3. [Some counterpoint](https://medium.com/the-sophist/wittgenstein-intelligence-is-never-artificial-51933315d1bd)

4. 11.7.2020 – [A professional treatment of Wittgenstein's remarks applied to AI](https://books.google.com/books?id=WeGJAgAAQBAJ&printsec=frontcover&source=gbs_atb#v=onepage&q&f=false) Some arguments presented are similar to the ones here, albeit without the various simplifications for readability, and applications more towards psychology. The treatment dates to the last epoch in AI, though the epistemological arguments hold.

5. 11.11.2020 – [Interesting work from Hinton's group on better teacher methods](http://arxiv.org/pdf/2011.03037v1.pdf)
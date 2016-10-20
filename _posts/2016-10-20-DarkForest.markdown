---
layout: post
title:  "Dark Forest Theory of Machine Learning"
date:   2016-10-20 08:00:00
categories: general
---

In Liu CiXin's novel, "The Dark Forest" he devises a solution to [Fermi's paradox][fermi] based on three axioms of extraterrestrial contact.

<img src="http://leotam.github.io/assets/darkForest.jpg" width="300" height="432" align="middle"/>

1. The Universe is a dark forest where many civilizations reside, unaware of the others' location.

2. Each civilization with sufficiently advanced technology for interstellar travel has experienced an (exponential) technological explosion. 

3. Upon discovering another civilization, a civilization must necessarily annihilate the discovered population, in fear of (2) and the possibility of destruction (being left behind).

With minimal adaptation, the axioms apply to adversarial machine learning.  Namely:

1. Machine learning models, when exposed, are subject to adversarial probing. <https://arxiv.org/abs/1312.6199>

2. When ML models are subject to adversarial probing, it's possible to improve the robustness of the model. <https://arxiv.org/abs/1412.6572>

3. Through probing, one may increase the model robustness of a similar model, for example through: <https://arxiv.org/abs/1412.6572> or <http://papers.nips.cc/paper/5423-generative-adversarial>. 

The result is a Dark Forest equilibrium for machine learning.  For a foundational treatment of adversarial game theory, please refer to [John Nash's thesis][nashThesis] (yes, it's that short).  Some implications are summarized.

The world of ML is subject to the Dark Forest situation.  Web crawlers as employed by hyperscale web companies (Google, Baidu, Yahoo (maybe), Tencent, etc.) become hunters in cyberspace searching for ML models.  When discovering ML models, their reasonable course of action is to adversarially mine information from the ML model to increase the robustness of one's own model.

There are two solutions to 'survive' the Dark Forest situation.  The obvious solution is through isolation, i.e. for each company an internal ML model may be deployed.  The second solution is the traveler's model, i.e. to continuously adjust parameters through active learning (retraining) of the network.

A cogent description of the Dark Forest solution to Fermi's paradox is here <http://philosophy.stackexchange.com/questions/18127/dark-forest-postulate-used-to-explain-the-fermi-paradox>.  

This blog post is solely my own and does not necessarily represent the views of NVIDIA corp.

Note, Ian Goodfellow notes that the analogy is imperfect as not every model is in conflict (ecological niche addendum?).

[fermi]: https://en.wikipedia.org/wiki/Fermi_paradox
[nashThesis]: http://www.princeton.edu/mudd/news/faq/topics/Non-Cooperative_Games_Nash.pdf
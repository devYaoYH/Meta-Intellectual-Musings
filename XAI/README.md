> Alice and Bob are driving along a road in the city. The sky was dark and visibility was poor. Flashes of lightning occasionally lit up the foreboding cityscape, painting sawtooth patterns along the road ahead. The staccato of raindrops on the windshield gradually turned into a lullaby. Suddenly, a few meters ahead, an irregular shadow stepped into view, jolting Alice into full alertness. On reflex, Alice spins the wheel around and narrowly avoids the shadow. The wheels skidded along the wet road and for a moment the car spins out of control, crashing headfirst into the sidewalk. Right behind Alice in another car, Bob continued on without pause and the irregular shadow dissipated into a mist of water as the car drove over a puddle. So sets the scene for our hypothetical parable.

# Introduction

*“Science gathers knowledge faster than Society gathers wisdom” – Isaac Asimov.*

Aphorisms catch on precisely because it abstracts a wealth of acute observations behind few words, exemplifying the voluminous content possible with comparatively limited tokens. Penned in the 1980s, with the menace of the Cold War hanging heavy in the air, technological advances threatened to mark an end to life as we knew it. The spectre of improperly wielded scientific advances throughout history has plagued humanity’s quest to better its conditions. Yesterday (arguably still), unrestrained forces of the atomic nucleus sought freedom through annihilation. Today, widespread employment of Artificial Intelligence models provide convenience through oppression.

To be clear, we have yet to succumb to the folly of entrusting AIs with too much today and have been actively fighting back as a community from researchers to policy makers against the non-judicious application of AI technology. It is worth highlighting a key step in this fight: NeurIPS, a prominent conference at the forefront of AI development, has introduced a necessary “Impact Statement” for all paper submissions stating the “broader impact of their work, including its ethical aspects and future societal consequences” [cite NeurIPS]. This article is a look behind the scenes of this fight to ensure the ethical application of AI technologies from the perspective of the Explainable AI (XAI) movement, and attempts to show how the battlelines are always hazier than we think.

# What, Why and How is XAI?

Broadly construed, XAI seeks to develop methods for prying into the black boxes of AI models. In doing so, one seeks to understand how the AI model works to inform an explanation for why it provides certain outputs. The motivation and growing investment into XAI are in no small part due to the recent surge in development of deep neural networks in this past decade. As opposed to traditional symbolic AI models, neural networks operate with a distributed representation of activations spread across many nodes in a network. This distributed nature of meaning within deep neural network models presents us with a very alien form of reasoning than that which we are used to.

Deep neural networks would not have attracted as much attention without the impressive and promising results it has shown thus far. DeepMind’s AlphaGo presented a general model to learn many diverse games and perform better than human players (in Go, Atari, and most recently StarCraft 2). Generative Adversarial Networks can edit video and generate images and text that consistently fool human observers. Such achievements have inched the ability of artificial systems closer to human ability. Consequently, many AI models have found their way into our everyday lives and could come to influence key decision-making positions in our society.

The current rate at which AI gains competence vastly outstrips the rate at which we are formulating guidelines and policies surrounding their use. Our lack of understanding how such systems operate further slows down the latter. How should we then approach understanding this alien yet all-too-familiar system? It is against this backdrop that the XAI movement come into focus in recent years. DARPA states that the goal of XAI is to “enable human users to understand, appropriately trust, and effectively manage the emerging generation of artificially intelligent partners” and that such “systems will have the ability to explain their rationale, characterize their strength and weaknesses, and convey an understanding of how they will behave in the future.” [cite DARPA].

From the above DARPA definition of XAI, we can extract two broad thrusts of the movement:

1. Develop tools to interact intelligibly with AI models
2. Bake into AI models an awareness of its internal processes

Furthermore, it highlights some general approaches to achieving these goals:

1. Produce [text-based] explanations alongside model output
2. Identify limits of AI models (when guarantees break down)
3. Predict model behavior for novel test data

Given the broad overview of what, why and how XAI is conducted, we will next examine instances where AI models require explanations as well as what are the current products from the XAI movement.

# What require explaining? - When Models Fail

Present AI models fall broadly into 4 categories: Classification, Generation, Prediction, and Search. Classification models are predominantly implemented with Convolutional Neural Networks (CNNs), and generative models are the flip side of classification. Rather than extracting a set of hidden features from the input to seperate the set of given inputs to some set of output labels (think of image classification), generative models such as Generative Adversarial Networks (GAN) fills in the gaps and produces output similar to inputs from some hidden set of features (think of GPT-2/3 and Deepfake). Predictive models approximates some resultant state given rules and initial parameters. Examples include DeepMind's protein folding model as well as a neural network simulation of solutions to three-body problems in physics (cite paper Brutus-trained ANN). Search models see widespread use in Game-Playing agents such as AlphaGo and the venerable DeepBlue chess AI. These typically explore and assess actions with an value function in mind to optimize the final outcome of a series of chosen actions. More sophisticated search models typically would require a predictive assessment of the possible values of permissible actions, in fact, a key contributor to the success of AlphaGo is the use of a deep neural network to approximate the value of board positions.

There are general issues pertaining to these classes of AI models which requires us to provide an explanation for their output. For a classification or generation model using deep neural networks, nowhere can we find explicit rules that govern the decision processes leading to their outputs. Similarly, when prediction results deviate from empirical findings, an explanation is warranted as to why there is this difference which could help in corrective measures to further improve results. Searching assumes that one has a good fit for the value function utilized in assessing actions and states which is not guaranteed. In addition, there is the ugly issue of the Value Alignment Problem: how can we ensure that AI holds our values in its best interest? Below, we shall outline a few examples of such issues in recent literature.

## The case of the misidentified panda

<p align="center">
  <img src="/XAI/img/figure1_panda_gibbon.png">
</p>
<p align="center"><strong>Figure 1:</strong> Panda obfusicated with noise produces Gibbon. <a href="https://openai.com/blog/adversarial-example-research/">Source</a></p>

## The case of the inappropriate chatbot

[Microsoft's AI chatbot producing racist tweets](https://www.theverge.com/2016/3/24/11297050/tay-microsoft-chatbot-racist)

## The case of the spasmodic goalie

[Adversarial attacks on RL agents](https://bair.berkeley.edu/blog/2020/03/27/attacks/)


# XAI State-of-the-Art (SotA)

## Tracing important parameters through model

## Attending to specific regions of input

<p align="center">
  <img src="/XAI/img/figure2_selective_attention.gif">
</p>
<p align="center"><strong>Figure 2:</strong> Overlay of selected input regions model attends to <a href="https://ai.googleblog.com/2020/06/using-selective-attention-in.html">Source</a></p>

## Learning to provide explanatory [text]

# What is an Explanation? - Perspectives from Philosophy

# Where Philosophy can help XAI

# Distinguishing between Diagnostics and Explanation

# Explanations exist outside AI Models

# Current tools of Command Responsibility

# XAI not merely as a way of looking back, but looking forwards

XAI does not only serve the purpose of examining presently available systems in an effort to *make sense of* how and why they function but could further serve the purpose of pushing us towards truely intelligent systems. [Rosenberg ratiocinative constraint here]

# The Future of XAI

# References

1. [AlphaFold] https://www.nature.com/articles/d41586-020-03348-4
2. [3-Body Problem ANN simulation] https://arxiv.org/pdf/1910.07291.pdf
3. [panda-gibbon image adversary] https://openai.com/blog/adversarial-example-research/
4. [racist twitter chatbot] https://www.theverge.com/2016/3/24/11297050/tay-microsoft-chatbot-racist
5. [RL goalie adversarial attack] https://bair.berkeley.edu/blog/2020/03/27/attacks/
6. [Selective Attention Agent] https://ai.googleblog.com/2020/06/using-selective-attention-in.html
7. [Command Responsibility Doctrine] https://www.oxfordbibliographies.com/view/document/obo-9780199796953/obo-9780199796953-0088.xml

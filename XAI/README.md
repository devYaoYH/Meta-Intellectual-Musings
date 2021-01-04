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

There are general issues pertaining to these classes of AI models which requires us to provide an explanation for their output. For a classification or generation model using deep neural networks, nowhere can we find explicit rules that govern the decision processes leading to their outputs. Similarly, when prediction results deviate from empirical findings, an explanation is warranted as to why there is this difference which could help in corrective measures to further improve results. Searching assumes that one has a good fit for the value function utilized in assessing actions and states which is not guaranteed. In addition, there is the ugly issue of the Value Alignment Problem: how can we ensure that AI holds our values in its best interest? Below, we shall outline a few examples of errors in AI models that require an explanation.

## The case of the misidentified panda

The class of tasks surrounding image classification has received much attention over the years as the basis for numerous applications: Object identification and tracking, Image segmentation, and Face recognition to name a few. Face recognition as part of biometrics registration at international customs is already widely deployed in many countries. Driverless cars also requires a robust assessment of its surroundings using some visual system. The correct functioning of image classification models is thus paramount to the success of this wide range of solutions. However, recent literature has identified that it is not difficult to fool AI image classifiers into providing an incorrect output using images that are slightly changed. Furthermore, modifications in such adversarial images are imperceptible to the human eye, rendering their detection harder.

<p align="center">
  <img src="/XAI/img/panda_gibbon.png">
</p>
<p align="center"><strong>Figure 1:</strong> Panda obfusicated with noise produces Gibbon. <a href="https://openai.com/blog/adversarial-example-research/">Source</a></p>

In the above example, a distributed pattern of noise is overlayed onto the original image and tricks the model into classifying the modified image as a high-probability gibbon. Furthermore, it is possible to print out such adversarial images or construct an adversarial 3D model and robustly trick models from different angles ([case of a turtle model misidentified as a gun](https://www.theverge.com/2017/11/2/16597276/google-ai-image-attacks-adversarial-turtle-rifle-3d-printed)).

There is also growing concern that Deep CNNs used in most image classifiers are not sufficiently robust for current applications. A study by Michael et. al highlighted that Deep CNNs are unable to generalize pose of image objects when they differ from canonical poses that the CNN has been trained on.

<p align="center">
  <img src="/XAI/img/pose_adversarial_attacks.png">
</p>
<p align="center"><strong>Figure 2:</strong> Different poses of a recognizable object in its canonical pose elicits incorrect classification. <a href="https://arxiv.org/pdf/1811.11553.pdf">Source</a></p>

Such problems pose a pressing concern for the application of Deep CNN image classification models out in the wild. For instance, driverless cars could be fooled by roadsigns modified via an adversarial attack with disastrous consequences, or be unable to identify obstacles or pedestrains in novel poses (an example pointed out in the paper was a fatal accident involving a Tesla due to the car's autopilot failing to identify a white truck).

## The case of the inappropriate chatbot

Another high profile case occured a few years ago when chatbots were gaining traction and finding increased usage in customer service domains. Framed as an experiment in "conversational understanding", Microsoft released a Twitter bot called Tay which posted tweets and replied to user's tweets in the public domain. Although initially innocuous, it quickly learned to parrot inappropriate tweets from users resulting in Microsoft shutting the experiment down within 24hours.

<p align="center">
  <img src="/XAI/img/tay_ai_twitter_bot.png">
</p>
<p align="center"><strong>Figure 3:</strong> Tweet responding to Tay AI's increasingly inappropriate tweets <a href="https://www.theverge.com/2016/3/24/11297050/tay-microsoft-chatbot-racist">Source</a></p>

In the previous case of the misidentified panda, no modifications were made to the AI model's internal structure, such panda-gibbon attacks merely amplifies already present edge-cases within the model. However, with this case of the inappropriate chatbot, it is the learning mechanism that has been hijacked and exploited to produce undesired results from the AI model. Such an 'attack', although possibly unintentional, highlights the importance of training data in model construction. Machine learning AI models are shackled by the curse of scale. More data and more processing power has drastically improved their ability but they are nonetheless still limited by the quality of data that goes into training them. Here, we observe that by poisoning the data from which an AI model learns, it is possible to control the output from such models and for a malicious party, bias such models towards undesirable outcomes.

## The case of the spasmodic goalie

Similar to Classifier Deep CNNs, Reinforcement Learning Search agents have been recently shown to be vulnerable to the same class of attacks by modifying their inputs. Two simulated robots face-off each other in a soccer game of penalty kick. The blue player is able to score quite freqeuntly when playing against normal simulated opponents, but fails consistently against the red adversarial player which employs a novel strategy of contorting itself on the floor rather than anticipating and attempting to block the oncoming shot.

<p align="center">
  <img src="/XAI/img/spasmodic_goalie.png">
</p>
<p align="center"><strong>Figure 4:</strong> An adversarial opponent goalie contorts on the floor to prevent scoring. <a href="https://bair.berkeley.edu/blog/2020/03/27/attacks/">Source</a></p>

Beyond showing that a different class of AI models are susceptible to the same adversarial attacks as Deep CNNs, this example also highlights that AI models may produce wildly unexpected ways of 'solving' the problems posed to it. Here, the adversarial agent is also a machine learning model. Given the task of 'optimally' defeating the normal agent, it employs novel strategies which violate our expectations. Here, the concern is two-fold: Firstly, is the problem a lack of sufficient constraints in the environment (thus enabling such adversarial strategies)? Secondly, how can we prevent undesirable novel strategies?

The AI philosopher Nick Bostrom states that one of the key problematic outcome of achieving the singularity is that such a superintelligent system will always find ways to outsmart its human creators. For our red adversarial goalie, it appears unlikely that we will be able to fully specify constraints to its actions such that novel unexpected strategies do not occur. This failure reduces the likelihood that we would be able to further prevent undesirable strategies produced by AI models all in the name of 'optmially' fulfiling its goal. A pessimistic worry here by Nick Bostrom is that "we might make a mistake and give [AI models] goals that lead it to annihilate humankind".

# Function of explanations

Against this background of increasingly pressing problems with today's AI models, the XAI movements hopes to provide solutions to these problems by generating explanations for model outputs as well as increasing the transparency of such models.

# XAI State-of-the-Art (SotA)

## Tracing important parameters through model

## Attending to specific regions of input

<p align="center">
  <img src="/XAI/img/selective_attention.gif">
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

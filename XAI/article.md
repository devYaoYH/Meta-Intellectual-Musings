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

[brief introduction to the problems with AI models today]

# Function of explanations

Against a background of increasingly pressing problems with today's AI models, the XAI movements hopes to provide solutions to these problems by generating explanations for model outputs as well as increasing the transparency of such models. In a recent review of research in XAI, Giulia and Luca surmises that there are four main purposes XAI sees in explanations [cite Giulia et.al 2020: Systematic Review]:

- Explain to *justify*: explanations increase justifiability of decisions based on model output
- Explain to *control*: explanations should enhance transparency, allowing its debugging and identification of potential flaws
- Explain to *improve*: explanations help with improving the accuracy and efficiency of models
- Explain to *discover*: explanations support extraction of novel knowledge and learning of relationships and patterns

For the earlier examples of adversarial attacks, it is clear that the role of explanations in those cases would be to improve our ability to detect such possible flaws in our models as well as make improvements to defend against these adversarial attacks. Furthermore, in such cases as the unfortunate Tesla incident, the ability to offer explanations as to why its autopilot made the decisions it did could add weight in a legal setting. Lastly, explanations could elucidate AlphaGo's famous 37th move against Lee Sedol that expert commentators saw as a "very strange move" and one not within human playbooks [cite WIRED article].

Crucially, we observe that the review identified roles of explanations which are mostly post-hoc and focused around the actions and workings of the model. This is a first indication of the limits of what we can come to expect from the XAI movement, it is very much an engineering field that currently looks inwards to produce tools which help to better such models. Contrasted against the problems it attempts to position itself to solve, such an engineering focus appears lacking. This is not to dismiss the importance of such tools currently produced by XAI, rather, it is a call to reign back some of our expectations for this emerging field.

# Case study: Google Cloud Explainable AI

Google's Cloud Explainable AI offers 3 main services: AI Explanations, What-If Tool and Continuous evaluation. It should be pointed out that this product is model-agnostic, meaning that there is no modification to the underlying model, rather it is a tool to be applied on-top of a trained model. In other words, a post-hoc approach. AI Explanation service offers 'Feature Attributions': "signed per-feature attribution score proportional to the feature's contribution to the model's prediction" [cite Whitepaper]. This is similar to the first class of saliency maps we reviewed. More interesting are the What-If and Continuous evaluation tools.

<p align="center">
  <img src="/XAI/img/google_explainable_ai.png">
</p>
<p align="center"><strong>Figure 9:</strong> An overview of the features Google's Cloud Explainable AI service offers <a href="https://cloud.google.com/explainable-ai#features">Source</a></p>

Rather than simply statically identifying the salient features in a model's prediction, the [What-If Tool](https://pair-code.github.io/what-if-tool/index.html#demos) allows one to modify datapoints and introduce what-if sample points to observe the examined model's predictions. This is an interactive tool that can be deployed after a model has been trained and serve as a way of visualizing how the model performs on different datasets. Lastly, the [Continuous evaluation tool](https://cloud.google.com/ai-platform/prediction/docs/continuous-evaluation) monitors a deployed model by sampling datapoints against human-evaluated results. For example, a model can be queried with a image classification request and the same image is sent to the deployed AI model as well as human evaluators. The results from the model is then compared against human evaluation responses and reported intermittently.

Although the methodology underlying extracting of metrics and pertinent information from AI black boxes is similar to the first class of XAI (saliency maps), Google's Explainable AI takes a promising step by shifting focus from the raw numbers to interaction with human evaluators of the model. Explanations as per this tool is driven not only by mathematical tools employed to extract pertinent features relevant to model predictions but through interactions with human questioners.

# Alice and Bob

# Distinguishing between Diagnostics and Explanation

# Explanations exist outside AI Models

# XAI not merely as a way of looking back, but looking forwards

XAI does not only serve the purpose of examining presently available systems in an effort to *make sense of* how and why they function but could further serve the purpose of pushing us towards truely intelligent systems. [Rosenberg ratiocinative constraint here]

# References

1. [AlphaFold] https://www.nature.com/articles/d41586-020-03348-4
2. [3-Body Problem ANN simulation] https://arxiv.org/pdf/1910.07291.pdf
3. [panda-gibbon image adversary] https://openai.com/blog/adversarial-example-research/
4. [racist twitter chatbot] https://www.theverge.com/2016/3/24/11297050/tay-microsoft-chatbot-racist
5. [RL goalie adversarial attack] https://bair.berkeley.edu/blog/2020/03/27/attacks/
6. [Selective Attention Agent] https://ai.googleblog.com/2020/06/using-selective-attention-in.html
7. [Command Responsibility Doctrine] https://www.oxfordbibliographies.com/view/document/obo-9780199796953/obo-9780199796953-0088.xml
8. [Explanable Artificial Intelligence: a Systematic Review] https://arxiv.org/pdf/2006.00093.pdf
9. [Move 37 by AlphaGo] https://www.wired.com/2016/03/two-moves-alphago-lee-sedol-redefined-future/
10. [SotA Saliency Map] https://arxiv.org/pdf/1904.00605.pdf
11. [NAM interpretable architecture] https://arxiv.org/pdf/2004.13912.pdf
12. [Google Cloud XAI Whitepaper] https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf
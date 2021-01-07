> Alice and Bob are driving along a road in the city. The sky was dark and visibility was poor. Flashes of lightning occasionally lit up the foreboding cityscape, painting sawtooth patterns along the road ahead. The staccato of raindrops on the windshield gradually turned into a lullaby. Suddenly, a few meters ahead, an irregular shadow stepped into view, jolting Alice into full alertness. On reflex, Alice spins the wheel around and narrowly avoids the shadow. The wheels skidded along the wet road and for a moment the car spins out of control, crashing headfirst into the sidewalk. Right behind Alice in another car, Bob continued on without pause and the irregular shadow dissipated into a mist of water as the car drove over a puddle. So sets the scene for our hypothetical parable.

# Introduction

*“Science gathers knowledge faster than Society gathers wisdom” – Isaac Asimov.*

Aphorisms catch on precisely because it abstracts a wealth of acute observations behind few words, exemplifying the voluminous content possible with comparatively limited tokens. Penned in the 1980s, with the menace of the Cold War hanging heavy in the air, technological advances threatened to mark an end to life as we knew it. The spectre of improperly wielded scientific advances throughout history has plagued humanity’s quest to better its conditions.

To be clear, we have yet to succumb to the folly of entrusting AIs with too much today and have been actively fighting back as a community from researchers to policy makers against the non-judicious application of AI technology. It is worth highlighting a key step in this fight: NeurIPS, a prominent conference at the forefront of AI development, has introduced a necessary “Impact Statement” for all paper submissions stating the “broader impact of their work, including its ethical aspects and future societal consequences” [[NeurIPS 2020 blogpost](https://neuripsconf.medium.com/getting-started-with-neurips-2020-e350f9b39c28)]. This article is a look behind the scenes of this fight to ensure the ethical application of AI technologies from the perspective of the Explainable AI (XAI) movement, and attempts to show how the battlelines are always hazier than we think.

# What, Why and How is XAI?

Broadly construed, XAI seeks to develop methods for prying into the black boxes of AI models. In doing so, one seeks to understand how the AI model works to inform an explanation for why it provides certain outputs. The motivation and growing investment into XAI are in no small part due to the recent surge in development of deep neural networks in this past decade. As opposed to traditional symbolic AI models, neural networks operate with a distributed representation of activations spread across many nodes in a network. This distributed nature of meaning within deep neural network models presents us with a very alien form of reasoning than that which we are used to.

Deep neural networks would not have attracted as much attention without the impressive and promising results it has shown thus far. DeepMind’s AlphaGo presented a general model to learn many diverse games and perform better than human players (in Go, Atari, and most recently StarCraft 2). Generative Adversarial Networks can edit video and generate images and text that consistently fool human observers. Such achievements have inched the ability of artificial systems closer to human ability. Consequently, many AI models have found their way into our everyday lives and could come to influence key decision-making positions in our society.

The current rate at which AI gains competence vastly outstrips the rate at which we are formulating guidelines and policies surrounding their use. Our lack of understanding how such systems operate further slows down the latter. How should we then approach understanding this alien system? It is against this backdrop that the XAI movement come into focus in recent years. DARPA states that the goal of XAI is to “enable human users to understand, appropriately trust, and effectively manage the emerging generation of artificially intelligent partners” and that such “systems will have the ability to explain their rationale, characterize their strength and weaknesses, and convey an understanding of how they will behave in the future.” [[DARPA XAI](https://www.darpa.mil/program/explainable-artificial-intelligence)].

From the above DARPA definition of XAI, we can extract two broad thrusts of the movement:

1. Develop tools to interact intelligibly with AI models
2. Develop AI models which are more transparent and interpretable

The two broad thrusts align with the two stages of XAI methods as identified by a review of research literature in XAI by Giulia and Luca: post-hoc and ante-hoc [[Giulia et.al, 2020](https://arxiv.org/pdf/2006.00093.pdf)]. Post-hoc meaning *after the matter* of model output and Ante-hoc meaning *before the matter* of model output. Explanatory methods aligning with post-hoc stage are tools which attempts to review and explain in hindsight why the model has produced the outputs that it has. In contrast, Interpretable methods are focued around designing models which utilize inherently interpretable methods to arrive at their outputs. An example is designing simplier, more linear network architectures instead of an obfusicated architecture such as Deep Convolutional Neural Networks.

Performance and domain-specificity are two main challenges in this direction as identified by Rudin in her paper arguing for the use of interpretable AI over explanatory AI methods [[Rudin, 2019](https://arxiv.org/pdf/1811.10154.pdf)]. Developing simplier, more interpretable models that perform with the same accuracy of Deep CNNs may require intensive effort which coporations employing AI models may not be inclined to invest in. Furthermore, ante-hoc methods by their nature cannot be model-agnostic, what is interpretable depends on the problem that the model is employed to solve, further adding to development costs. This difficulty concurs with the relatively sparse research into interpretable methods as compared with explanatory methods (20% of all research on methods in XAI) [[Giulia et.al, 2020, Figure 4](https://arxiv.org/pdf/2006.00093.pdf)].

For both directions, there is a focus on unveiling the mechanistic details of processes within AI models. Understanding of the mechanistic details of a model would be most helpful in understanding the output from such models. However, against the problems that we encounter in a social setting through the employment of AI models, perhaps our notion of explanations needs to be broadened beyond merely illuminating mechanisms.

# What requires explaining? - When Models Fail

The class of tasks surrounding image classification has received much attention over the years as the basis for numerous applications: Object identification and tracking, Image segmentation, and Face recognition to name a few. Face recognition as part of biometrics registration at international customs is already widely deployed in many countries. Driverless cars also requires a robust assessment of its surroundings using some visual system. The correct functioning of image classification models is thus paramount to the success of this wide range of solutions. However, recent literature has identified that it is not difficult to fool AI image classifiers into providing an incorrect output using images that are slightly changed. Furthermore, modifications in such adversarial images are imperceptible to the human eye, rendering their detection harder.

<p align="center">
  <img src="/XAI/img/panda_gibbon.png">
</p>
<p align="center"><strong>Figure 1:</strong> Panda obfusicated with noise produces Gibbon. <a href="https://openai.com/blog/adversarial-example-research/">Source</a></p>

In the above example, a distributed pattern of noise is overlayed onto the original image and tricks the model into classifying the modified image as a high-probability gibbon. Furthermore, it is possible to print out such adversarial images or construct an adversarial 3D model and robustly trick models from different angles ([case of a turtle model misidentified as a gun](https://www.theverge.com/2017/11/2/16597276/google-ai-image-attacks-adversarial-turtle-rifle-3d-printed)).

Another high profile case occured a few years ago when chatbots were gaining traction and finding increased usage in customer service domains. Framed as an experiment in "conversational understanding", Microsoft released a Twitter bot called Tay which posted tweets and replied to user's tweets in the public domain. Although initially innocuous, it quickly learned to parrot inappropriate tweets from users resulting in Microsoft shutting the experiment down within 24hours.

<p align="center">
  <img src="/XAI/img/tay_ai_twitter_bot.png">
</p>
<p align="center"><strong>Figure 2:</strong> Tweet responding to Tay AI's increasingly inappropriate tweets <a href="https://www.theverge.com/2016/3/24/11297050/tay-microsoft-chatbot-racist">Source</a></p>

In the previous case of the misidentified panda, no modifications were made to the AI model's internal structure, such panda-gibbon attacks merely amplifies already present edge-cases within the model. However, with this case of the inappropriate chatbot, it is the learning mechanism that has been hijacked and exploited to produce undesired results from the AI model. Such an 'attack', although possibly unintentional, highlights the importance of training data in model construction. Machine learning AI models are shackled by the curse of scale. More data and more processing power has drastically improved their ability but they are nonetheless still limited by the quality of data that goes into training them. Here, we observe that by poisoning the data from which an AI model learns, it is possible to control the output from such models and for a malicious party, bias such models towards undesirable outcomes.

# Function of explanations

Against a background of increasingly pressing problems with today's AI models, the XAI movements hopes to provide solutions to these problems by generating explanations for model outputs as well as increasing the transparency of such models. In the recent review of research in XAI, Giulia and Luca surmises that there are four main purposes XAI sees in explanations [[Giulia et.al, 2020](https://arxiv.org/pdf/2006.00093.pdf)]:

- Explain to *justify*: explanations increase justifiability of decisions based on model output
- Explain to *control*: explanations should enhance transparency, allowing its debugging and identification of potential flaws
- Explain to *improve*: explanations help with improving the accuracy and efficiency of models
- Explain to *discover*: explanations support extraction of novel knowledge and learning of relationships and patterns

For the earlier examples of adversarial attacks, it is clear that the role of explanations in those cases would be to improve our ability to detect such possible flaws in our models as well as make improvements to defend against these adversarial attacks. Furthermore, in such cases as the unfortunate Tesla incident, the ability to offer explanations as to why its autopilot made the decisions it did could add weight in a legal setting. Lastly, explanations could elucidate AlphaGo's famous 37th move against Lee Sedol that expert commentators saw as a "very strange move" and one not within human playbooks [[WIRED](https://www.wired.com/2016/03/two-moves-alphago-lee-sedol-redefined-future/)].

Crucially, we observe that the review identified roles of explanations which are mostly post-hoc and focused around the actions and workings of the model. This is a first indication of the limits of what we can come to expect from the XAI movement, it is very much an engineering field that currently looks inwards to produce tools which help to better such models. Contrasted against the problems it attempts to position itself to solve, such an engineering focus appears lacking. This is not to dismiss the importance of such tools currently produced by XAI, rather, it is a call to reign back some of our expectations for this emerging field.

# Case study: Google Cloud Explainable AI

Google's Cloud Explainable AI offers 3 main services: AI Explanations, What-If Tool and Continuous evaluation. It should be pointed out that this product is model-agnostic, meaning that there is no modification to the underlying model, rather it is a tool to be applied on-top of a trained model. In other words, a post-hoc approach. AI Explanation service offers 'Feature Attributions': "signed per-feature attribution score proportional to the feature's contribution to the model's prediction" [[Google, AI Explanations Whitepaper](https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf)]. This is a service focused towards exposing the inner workings of model predictions based on input features. More interesting are the What-If and Continuous evaluation tools.

<p align="center">
  <img src="/XAI/img/google_explainable_ai.png">
</p>
<p align="center"><strong>Figure 3:</strong> An overview of the features Google's Cloud Explainable AI service offers <a href="https://cloud.google.com/explainable-ai#features">Source</a></p>

Rather than simply statically identifying the salient features in a model's prediction, the [What-If Tool](https://pair-code.github.io/what-if-tool/index.html#demos) allows one to modify datapoints and introduce what-if sample points to observe the examined model's predictions. This is an interactive tool that can be deployed after a model has been trained and serve as a way of visualizing how the model performs on different datasets. Lastly, the [Continuous evaluation tool](https://cloud.google.com/ai-platform/prediction/docs/continuous-evaluation) monitors a deployed model by sampling datapoints against human-evaluated results. For example, a model can be queried with a image classification request and the same image is sent to the deployed AI model as well as human evaluators. The results from the model is then compared against human evaluation responses and reported intermittently.

Google's Explainable AI takes a promising step by shifting focus from the raw numbers to interaction with human evaluators of the model. Explanations as per this tool is driven not only by mathematical tools employed to extract pertinent features relevant to model predictions but through interactions with human questioners. However, at its core, such a product is still driven by a post-hoc approach: treating models as something aking to an engine and examining mechanistic details within them to produce 'explanations'.

There is pressure for XAI to move away from asking post-hoc questions to modifing our models themselves to function in a way that is 'self-explanatory'. This approach is typically referenced as interpretable AI rather than explanable AI. In her widely cited 2019 paper, Cynthia Rudin writes that "trying to *explain* black box models, rather than creating models that are *interpretable* in the first place, is likely to perpetuate bad practices and can potentially cause catastrophic harm to society". She points out 2 main reasons for her assessment [[Rudin, 2019](https://arxiv.org/pdf/1811.10154.pdf)]:

1. Explainable ML methods provide explanations that are not faithful to what the original model computes
2. Explanations often do not make sense, or do not provide enough detail to understand what the black box is doing

The first point highlights the pitfall that by constructing tools which help reveal *some* inner working of the black box model, we are not guaranteed to find *the* inner workings which are pertinent in the model's decision processes. There are many ways in which salient features can be identified from model output and inputs. Google's product utilizes a Sampled Shapley measure, many alternatives exist in research literature and it has been pointed out that we currently do not have a good way to evaluate which saliency measure should be preferred [[Giulia et.al, 2020](https://arxiv.org/pdf/2006.00093.pdf)].

The second point is hinted at within Google's whitepaper: "Similar to how model predictions are prone to adversarial attacks, attributions are prone to the same". Even with attributions at hand, comparing between attributions given for a correct classification versus an incorrect classification may reveal no useful differences in what salient features have been identified. Alternatively, two differrent sets of salient features may be identified for the same classification problem instance. Once again this makes us question just what such saliency information provides us with other than perhaps confirming some preconceived human bias as to what should have been pertinent features our decision process needs to take into account.

# Alice and Bob

# Distinguishing between Diagnostics and Explanation

# Explanations exist outside AI Models

Giulia and Luca observed in their review of XAI that "very few scholars have proposed approaches for evaluating such layer of explainability, either proposing formal, objective metrics or involving human-centered evaluation with model designers and end-users." [[Giulia et.al, 2020](https://arxiv.org/pdf/2006.00093.pdf)].

# XAI not merely as a way of looking back, but looking forwards

2. Bake into AI models an awareness of its internal processes

XAI does not only serve the purpose of examining presently available systems in an effort to *make sense of* how and why they function but could further serve the purpose of pushing us towards truely intelligent systems. [Rosenberg ratiocinative constraint here]

# References

1. [NeurIPS 2020 Blogpost] https://neuripsconf.medium.com/getting-started-with-neurips-2020-e350f9b39c28
2. [DARPA XAI] https://www.darpa.mil/program/explainable-artificial-intelligence
3. [panda-gibbon image adversary] https://openai.com/blog/adversarial-example-research/
4. [racist twitter chatbot] https://www.theverge.com/2016/3/24/11297050/tay-microsoft-chatbot-racist
5. [Giulia et.al: Explanable Artificial Intelligence: a Systematic Review] https://arxiv.org/pdf/2006.00093.pdf
6. [Move 37 by AlphaGo] https://www.wired.com/2016/03/two-moves-alphago-lee-sedol-redefined-future/
7. [Google Cloud XAI Whitepaper] https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf
8. [Rudin 2019: Stop Explaining Black Box ... and use Interpretable Models instead] https://arxiv.org/pdf/1811.10154.pdf
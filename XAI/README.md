# Thoughts on Explanable AI (XAI)

This document is a collection of thoughts on proposal that XAI can solve many of the problems we encounter during the usage of AI models. I first outline the current trajectory of XAI, the problems in the field where explanations are proposed to help with, and the present products of XAI. Next, I introduce disambiguations on the purpose and form of explanations from a perspective of Philosophy, in particular a Philosophy of explanations in Science and justifications in Ethics. Finally, I argue that the form of explanations we seek to help with the problems in using AI models ultimately do not consist of that which lies within our Models. We have to seek explanations from outside the black-box rather than peering within. Although making transparent the inner workings will be helpful, it cannot be treated as a silver-bullet in helping us resolve issues surrounding the use of AI models in society.

This is the verbose version of the document, for a more concise take along a similar direction, see [Article](/XAI/article.md).

## Table of contents:

- [What, Why and How is XAI?](/XAI#what-why-and-how-is-xai)
- [What requires explanining? - When Models Fail](/XAI#what-requires-explaining---when-models-fail)
  - [The case of the misidentified pand](/XAI#the-case-of-the-misidentified-panda)
  - [The case of the inappropriate chatbot](/XAI#the-case-of-the-inappropriate-chatbot)
  - [The case of the spasmodic goalie](/XAI#the-case-of-the-spasmodic-goalie)
- [Function of explanations](/XAI#function-of-explanations)
- [XAI State-of-the-Art](/XAI#xai-state-of-the-art-sota)
  - [Tracing important parameters through model](/XAI#tracing-important-parameters-through-model)
  - [Learning to provide explanatory [text]](/XAI#learning-to-provide-explanatory-text)
  - [Employing self-attention masking](/XAI#employing-self-attention-masking)
  - [Case study: Google XAI Whitepaper](/XAI#case-study-google-xai-whitepaper)
- [What is an Explanation? - Perspectives from Philosophy](/XAI#what-is-an-explanation---perspectives-from-philosophy)
- [Where Philosophy can help XAI](/XAI#where-philosophy-can-help-xai)
- [Distinguishing between Diagnostics and Explanation](/XAI#distinguishing-between-diagnostics-and-explanation)
- [Explanations exist outside AI Models](/XAI#explanations-exist-outside-ai-models)
- [Current tools of Command Responsibility](/XAI#current-tools-of-command-responsibility)
- [XAI not merely as a way of looking back, but looking forwards](/XAI#xai-not-merely-as-a-way-of-looking-back-but-looking-forwards)
- [The Future of XAI](/XAI#the-future-of-xai)
- [References](/XAI#references)

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

# What requires explaining? - When Models Fail

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

Similar to Classifier Deep CNNs, Reinforcement Learning Search agents have been recently shown to be vulnerable to the same class of attacks by modifying their inputs. Two simulated robots face-off each other in a soccer game of penalty kick. The blue player is able to score freqeuntly when playing against normal simulated opponents, but fails consistently against the red adversarial player which employs a novel strategy of contorting itself on the floor rather than anticipating and attempting to block the oncoming shot.

<p align="center">
  <img src="/XAI/img/spasmodic_goalie.png">
</p>
<p align="center"><strong>Figure 4:</strong> An adversarial opponent goalie contorts on the floor to prevent scoring. <a href="https://bair.berkeley.edu/blog/2020/03/27/attacks/">Source</a></p>

Beyond showing that a different class of AI models are susceptible to the same adversarial attacks as Deep CNNs, this example also highlights that AI models may produce wildly unexpected ways of 'solving' the problems posed to it. In this example, the adversarial agent is also a machine learning model. Given the task of 'optimally' defeating the normal agent, it employs novel strategies which violate our expectations. Here, the concern is two-fold: Firstly, is the problem a lack of sufficient constraints in the environment (thus enabling such adversarial strategies)? Secondly, how can we prevent undesirable novel strategies?

The philosopher Nick Bostrom states that one of the key problematic outcome of achieving the singularity is that such a superintelligent system will always find ways to outsmart its human creators. For our red adversarial goalie, it appears unlikely that we will be able to fully specify constraints to its actions such that novel unexpected strategies do not occur. This failure reduces the likelihood that we would be able to further prevent undesirable strategies produced by AI models all in the name of 'optmially' fulfiling its goal. The pessimistic worry here by Nick Bostrom is that "we might make a mistake and give [superintelligence] goals that lead it to annihilate humankind". A more likely present-day consequence is that we may find our AI models deviate from the values we hold to high importance when seeking actions that optimize some poorly-constrained value function. This is essentially the value alignment problem hinted at earlier.

# Function of explanations

Against this background of increasingly pressing problems with today's AI models, the XAI movements hopes to provide solutions to these problems by generating explanations for model outputs as well as increasing the transparency of such models. In a recent review of research in XAI, Giulia and Luca surmises that there are four main purposes XAI sees in explanations [cite Giulia et.al 2020: Systematic Review]:

- Explain to *justify*: explanations increase justifiability of decisions based on model output
- Explain to *control*: explanations should enhance transparency, allowing its debugging and identification of potential flaws
- Explain to *improve*: explanations help with improving the accuracy and efficiency of models
- Explain to *discover*: explanations support extraction of novel knowledge and learning of relationships and patterns

For the earlier examples of adversarial attacks, it is clear that the role of explanations in those cases would be to improve our ability to detect such possible flaws in our models as well as make improvements to defend against these adversarial attacks. Furthermore, in such cases as the unfortunate Tesla incident, the ability to offer explanations as to why its autopilot made the decisions it did could add weight in a legal setting. Lastly, explanations could elucidate AlphaGo's famous 37th move against Lee Sedol that expert commentators saw as a "very strange move" and one not within human playbooks [cite WIRED article].

Crucially, we observe that the review identified roles of explanations which are mostly post-hoc and focused around the actions and workings of the model. This is a first indication of the limits of what we can come to expect from the XAI movement, it is very much an engineering field that currently looks inwards to produce tools which help to better such models. Contrasted against the problems it attempts to position itself to solve, such an engineering focus appears lacking. This is not to dismiss the importance of such tools currently produced by XAI, rather, it is a call to reign back some of our expectations for this emerging field.

# XAI State-of-the-Art (SotA)

It will become clear that present products fall short of the goal of "[enabling] human users to understand, appropriately trust, and effectively manage the emerging generation of artificially intelligent partners". I propose that one key issue is that such XAI products as we will next review concern themselves with a mechanistic explanation of a model's inner workings. However, the originally stated goal is one which is broader and revolves around our human *understanding* and *trusting* such models. Simply illuminating what's inside the black-box and expecting the reflection to satisfy human understanding is wholly insufficient.

## Tracing important parameters through model

<p align="center">
  <img src="/XAI/img/saliency_maps.png">
</p>
<p align="center"><strong>Figure 5:</strong> Saliency maps of image classification results from VGG-16 Deep CNN model <a href="https://arxiv.org/pdf/1904.00605.pdf">Source</a></p>

One type of approach to illuminating the AI black box is to identify what are the important features in the presented input or important weights within a model that contributes to the final output. In other words, what are salient features that produces the model output. In Figure 5, a novel "RAP" algorithm for computing saliency maps for Deep CNNs is proposed and compared against other common algorithms. What one hopes to achieve here is an indication for what went on in the processing of the AI model such that the result is what it is. Saliency maps are post-hoc attempts to identify contributing factors to a model's final determination based on some measure of 'relevance'.

Such an approach is representative of the first broad thrust of the XAI movement: developing tools that allows us to interact intelligibly with our AI models. This approach attempts to answer a very human question: What factored into your decision? Furthermore, as engineers, it also allows us to identify processes happening within our models and fulfil the role of *control* or *improve*-type explanations. However, as can be seen with the non-RAP methods of computing saliency maps in this example, how are we to evaluate the results from such saliency maps? It appears that we may judge such output with preconceived notions of object-dependent classification and prefer the RAP method as it concurs with the foreground object having most relevance in the determination of image label. It is unclear what such saliency maps offer as explanation in incorrect cases where it is likely that the highlighted highly relevant foreground object has been incorrectly classified. 

## Learning to provide explanatory [text]

<p align="center">
  <img src="/XAI/img/productive_visual_explanations.png">
</p>
<p align="center"><strong>Figure 6:</strong> Training a model to generate explanatory text alongside classification output <a href="https://arxiv.org/pdf/1603.08507v1.pdf">Source</a></p>

Rather than examining what input features were relevant to the model output, some efforts have instead focused on the generation of explanations alongside model output. In this example, the paper proposes an additional model layer which generates texts as an explanation for why the image is classified thusly. Although this approach appears initially to be intuitive, it has not picked up much traction in recent years (the paper was published in 2016). Here, we can offer 2 reasons why this is so:

1. Learning to produce explanatory text in addition to classified label for images requires a labeled training dataset with proper explanations which is a highly intensive process without much available big-data to train on.
2. Although the explanations in the example appears to match with the model output, we cannot be sure that the process used to output the explanations actually cohere with whatever processing occurred to procude the model classification output. It could very well be the case that some independent part of the trained model was utilized in producing explanations entirely separate from the part of the model that produces a classification output.

## Employing self-attention masking

<p align="center">
  <img src="/XAI/img/selective_attention.gif">
</p>
<p align="center"><strong>Figure 7:</strong> Overlay of selected input regions model attends to <a href="https://ai.googleblog.com/2020/06/using-selective-attention-in.html">Source</a></p>

With the success of selective attention in Natural Language Processing models using the Transformer architecture, this technique has been applied to reinforcement agents as well in a recent study by Google Research, Tokyo. Here, an additional step is introduced to select sections of the input image before it is presented to the reinforcement agent. The paper reports that not only is the trained Attention Agent out-performing existing models, it can also generalize to unseen environments better than existing methods.

An alternative to asking post-hoc questions is to modify our models themselves to function in a way that is 'self-explanatory'. This approach as applied in the Attention Agent example is typically referenced as interpretable AI rather than explanable AI. There is pressure for XAI to move away from problematic post-hoc explanations. In her widely cited 2019 paper, Cynthia Rudin writes that "trying to *explain* black box models, rather than creating models that are *interpretable* in the first place, is likely to perpetuate bad practices and can potentially cause catastrophic harm to society". She points out 2 main reasons similar to what we have criticized the above two approaches for [cite Rudin 2019 paper]:

1. Explainable ML methods provide explanations that are not faithful to what the original model computes
2. Explanations often do not make sense, or do not provide enough detail to understand what the black box is doing

<p align="center">
  <img src="/XAI/img/gam_interpretable_architecture.png">
</p>
<p align="center"><strong>Figure 8:</strong> This paper introduces the Neural Additive Model, a more interpretable network architecture for classification <a href="https://arxiv.org/pdf/2004.13912.pdf">Source</a></p>

Even though utilizing attention to limit the input given to models reduces the domain under which models make their decision, it is still unclear what goes on within the model's decision processes. Agarwal et.al proposes a deep neural network take on a classic General Additive Model architecture for more interpretable classification models. Each input feature is transformed with a function approximated by a deep neural network before getting summed to determine a binary label. In this architecture, it is easy to separate the contribution of each feature by plotting the function estimated for it: "The [functions] learned by NAMs are not just an explanation but and exact description of how NAMs compute a prediction" [cite Agarwal et.al 2020 paper]. One main reason we find it difficult to trace the processes within a deep neural network is that the different input features interact with one another in complex ways at each layer of the neural network. In the NAM architecture, we know exactly how those features interact: a simple linear sum in the last layer.

## Case study: Google XAI Whitepaper

Now that we have reviewed some of the different types of approaches in research literature, we can apply the same critical lens to today's commercial offerings. Google offers a Cloud Explainable AI service (beta) alongside its AutoML and AI Platform products. We will use the accompanying [whitepaper](https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf) and [product site](https://cloud.google.com/explainable-ai) as references to its product offerings.

<p align="center">
  <img src="/XAI/img/google_explainable_ai.png">
</p>
<p align="center"><strong>Figure 9:</strong> An overview of the features Google's Cloud Explainable AI service offers <a href="https://cloud.google.com/explainable-ai#features">Source</a></p>

Google's Cloud Explainable AI offers 3 main services: AI Explanations, What-If Tool and Continuous evaluation. It should be pointed out that this product is model-agnostic, meaning that there is no modification to the underlying model, rather it is a tool to be applied on-top of a trained model. In other words, a post-hoc approach. AI Explanation service offers 'Feature Attributions': "signed per-feature attribution score proportional to the feature's contribution to the model's prediction" [cite Whitepaper]. This is similar to the first class of saliency maps we reviewed. More interesting are the What-If and Continuous evaluation tools.

Rather than simply statically identifying the salient features in a model's prediction, the [What-If Tool](https://pair-code.github.io/what-if-tool/index.html#demos) allows one to modify datapoints and introduce what-if sample points to observe the examined model's predictions. This is an interactive tool that can be deployed after a model has been trained and serve as a way of visualizing how the model performs on different datasets. Lastly, the [Continuous evaluation tool](https://cloud.google.com/ai-platform/prediction/docs/continuous-evaluation) monitors a deployed model by sampling datapoints against human-evaluated results. For example, a model can be queried with a image classification request and the same image is sent to the deployed AI model as well as human evaluators. The results from the model is then compared against human evaluation responses and reported intermittently.

Although the methodology underlying extracting of metrics and pertinent information from AI black boxes is similar to the first class of XAI (saliency maps), Google's Explainable AI takes a promising step by shifting focus from the raw numbers to interaction with human evaluators of the model. Explanations as per this tool is driven not only by mathematical tools employed to extract pertinent features relevant to model predictions but through interactions with human questioners.

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
8. [Explanable Artificial Intelligence: a Systematic Review] https://arxiv.org/pdf/2006.00093.pdf
9. [Move 37 by AlphaGo] https://www.wired.com/2016/03/two-moves-alphago-lee-sedol-redefined-future/
10. [SotA Saliency Map] https://arxiv.org/pdf/1904.00605.pdf
11. [NAM interpretable architecture] https://arxiv.org/pdf/2004.13912.pdf
12. [Google Cloud XAI Whitepaper] https://storage.googleapis.com/cloud-ai-whitepapers/AI%20Explainability%20Whitepaper.pdf
13. [Rudin 2019: Stop Explaining Black Box ... and use Interpretable Models instead] https://arxiv.org/pdf/1811.10154.pdf
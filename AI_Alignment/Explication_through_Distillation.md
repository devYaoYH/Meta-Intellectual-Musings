## Explicating model outcomes using distillation with sparse autoencoders - A review of "Towards Monosemanticity"

The paper "Towards Monosemanticity"[^1] presents a novel approach to understanding the internal mechanisms of neural networks through the use of a sparse autoencoder. One challenge of understanding the inner workings of neural networks and rendering their outputs explicable is the complexity of the relation between individual neurons (or groups of neurons) to commonsense notions of concepts which are unitary (or monosemantic to use the paper’s terminology). The paper presents exciting initial findings for applying expansion factors to the number of ‘monosemantic features’ a neural network can learn and notes their observations of Universality, Feature Splitting, existence of FSM-like recurrent structures.

I feel a key insight of this paper is to use feature expansion to attempt to dis-entangle the many learned features of a neural network. This approach is echoed by recent findings in neuroscience wherein rapid neural code switches were found for the task of face recognition[^2]. When macaque monkeys were presented with objects and face stimuli, and neuron activations within the inferotemporal cortex recorded at a short interval <20ms, two broad clusters of neural firing patterns were observed, one prototypical for face identification, and one for object classification. Note that these were the same group of cells recorded but exhibiting very different patterns of activation for different stimuli. It is not surprising that the number of things a system of neurons can encode for is larger than the number of neurons within that system. One example are our memories, the amount of memories which humans can store appears unbounded or to some degree, far larger than the number of neurons within the Hippocampus (which is largely associated with memory formation).

What’s exciting about this paper is the regularity of features extracted using the sparse autoencoder and the claim of ‘universality’ and ‘feature splitting’ which are the sort of desiderata a cognitive scientist may have on the function of concepts. Furthermore, the way in which the paper attempts to compare similarity of features across different transformer models is interesting and takes a functionalist perspective (looking at impact on final prediction logits, and similarity of influence of input activations). In addition, the observation of some recurrent structure of FSM-ish behavior could potentially help to explain the logical/reasoning capabilities in LLMs. However, whether the ‘universality’ of extracted monosemantic features are simply an artefact of the chosen sparse auto-encoder training hyperparameters and architecture is an open question. Another straightforward methodological extension to examine is how well these results apply when we scale up the transformer models studied to multiple layers as well as potentially other neural network architectures as well. Finally, would running the sparse autoencoder on the training datasets themselves be able to derive similar insights as per running them on the transformer MLP layers? Are the monosemantic features learnable through distilling the dataset itself?

On the whole, there may also be concerns to this broad approach of employing yet another neural network to help distil and explain that of one more complicated. Theoretically, the information entropy of the transformer model to be explained is far greater than that of the autoencoder used to explain it. Granted, much of the weight of explanations and what makes a candidate explanation good is that it helps to reduce or simplify a more complex explanandum, we wonder if it fails to capture important aspects of the transformer model. In particular, how well does the auto-encoder help us predict or place bounds on the behavior of the transformer model it is applied upon? An explanatory force behind rendering neural networks interpretable is also to help us better align our expectations to that of model behavior.

[^1]: https://transformer-circuits.pub/2023/monosemantic-features

[^2]: Rapid, concerted switching of the neural code in inferotemporal cortex
Yuelin Shi, Dasheng Bi, Janis K. Hesse, Frank F. Lanfranchi, Shi Chen, Doris Y. Tsao
bioRxiv 2023.12.06.570341; doi: https://doi.org/10.1101/2023.12.06.570341
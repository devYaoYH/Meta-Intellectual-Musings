# Thoughts on AI Alignment literature (Stanford CS362 Autumn '24)

A collection of short-form responses to the different perspectives on AI Alignment research as part of the course requirements for CS362.

Organized into broadly the following categories:

1.  Control: expanding abilities over AI systems
    -   [RLHF](choice_set_misspecification_reward_learning.md): potential issues of mis-specifying intentions.
    -   [Regulatory Frameworks](sb1047_vs_aiAct.md): how might regulations exert a degree of control over model development and deployment.
3.  Verification: knowing what the system does
    -   [Singular Learning Theory](SLT_implications.md): bounding model output expectations from input dataset characteristics.
    -   [Autoencoders for Dictionary Learning](Explication_through_Distillation.md): applying sparse autoencoders to transformer-architecture models to unveil interpretable 'feature vectors'.
5.  Values: Human stance towards what AI systems should do
    -   [AI as Aliens](merkwelt.md): how can we ever hope to understand an alien? What limitations does adopting this stance have towards AI Alignment efforts? Is it all doom?
    -   [Cyber Animism](Cyber_Animism.md): what is the place of consciousness in all this?
    -   [Capability-Value relation](obliqueness_thesis.md): what relation (if any) do values of a system have with its capabilities? Can we bound the accessible set of values based on a system's capabilities?
  
Overall thoughts:
-   Control (insofar as technically feasible) appears to be largely a AI governance/regulatory question, what are the kinds of knobs and levers we wish to have in place for responsible risk-aware development and deployment of AI systems?
-   Verification is where the majority of technical literature is focused on and where short-term pragmatic advancements in AI Alignment research will likely be. Results will inform what is feasible to control.
-   The space of value discussion is very noisy, the issue is not really so much as to what AI systems should value, but what we as humans value. The literature would better benefit from the humanities here instead of having more technical discussions. For example, the crucial questions to me in this area do not yield to mechanistical explanations of the sort best advanced by the sciences. Do AI systems have a moral responsiblity? Does this entail we need to first treat AI systems as agents? What does this mean for our judiciary apparatus and moral frameworks? In what cases is the use of AI systems unacceptable to society? How can we structure incentives to prevent such applications? If one merely focuses on the technically-inclined discussions, one tends to miss these important questions. I feel there is a tendency to theorize about the idealized outcomes of AI systems (the poster child being concerns about superintelligence/singularity) in a vacuum apart from the social structure within which such systems will operate and be developed in.

# Responsible AI

Trust, between human and machines, between consumer and business, is the core driver for Responsible AI. 

Azure Machine Learning (AML) offers tools for practitioners to incorporate Responsible AI practices into the development cycle. 
The 3 main pillars currently offered as part of AML are *Understand*, *Protect*, *Control*. 

- *Understand*: **Model transparency** focus on Intepretability, Explainability and Fairness
- *Protect*: **Privacy protection** by means of Encryption and Differential Privacy
- *Control*: **Auditable trail** by documentation

![AML Responsible AI 3 Pillars](/assets/aml-responsible-ai/responsible-ml-pillars.png)

# Azure ML Responsible AI
AML made available technical tools for **Model transparency** and **Privacy protection**. 

Note that such technical tools should not be seen as the sole solution to addressing issues related to Responsible AI, 
but rather tools to aid practitioners to gain understanding of system limitations and take informed steps to address those issues. 

Responsbile AI requires human involvment, and *can not* rely on technical tools alone. 

Diagram below shows the 3 main pillars, with associated tools and techniques made available within AML. 

![AML Responsbile AI](/assets/aml-responsible-ai/responsible-ai-L2.png)

Below is an expanded view of the map, and an interactive map can be found [here](https://gitmind.com/app/doc/a038840848). 

![AML Responsbile AI Expanded](/assets/aml-responsible-ai/responsible-ai-expanded.png)

# 1. Model transparency
## 1.1. Intepretability and Explainability
There is no industry-wide concensus on the definition of Intepretability and Explainability. 
However, the following definitions seem to have been adopted in recent years:

- **Intepretability**: Extent to which a cause and effect can be observed within a system. 
In other words, the extent to which someone is able to predict what is going to happen, given a change in input or algorithmic parameters. 
This is not to be confused between causation and correlation.

- **Explainability**: Extent to which the internal mechanics of the system can be explained in human terms.

**Tool**: [InterpretML](https://github.com/interpretml/interpret) is available as `azureml-interpret`, that allows model agnostics and model specific approaches to tabular data. Note that other types of data, such as time-series, is still an active research area. 
An interactive visualisation tool has been made available as part of AML.

![AML Model tranparency Tool](/assets/aml-responsible-ai/interpretability.png)

- Model Agnostic: 
    - [SHAP](https://github.com/slundberg/shap) 
        - Kernal Explainer
    - [Mimic (Global Surrogate Model) ](https://github.com/SMTorg/smt)
        - Linear regression
        - Decision Tree
        - LightGBM
        - Stochastic Gradient Decent
    - Permutation Feature Importance (PFI)
- Model Specific:
    - [SHAP](https://github.com/slundberg/shap)
        - Tree Explainer
        - Deep Explainer
        - Linear Explainer

> [SHAP (SHapley Additive exPlanations)](https://shap.readthedocs.io/en/latest/index.html) is a game theoretic approach to explain the output of any machine learning model. 
It connects optimal credit allocation with local explanations using the classic Shapley values from game theory and their related extensions
(see [papers](https://github.com/slundberg/shap#citations) for details and citations).

> [Global Surrogate Model](https://christophm.github.io/interpretable-ml-book/global.html#global) 
is based on the idea of training an interpretable model to mimic, i.e., approximate the predictions of a black box model, 
so that, one can interpret the surrogate model to draw conclusions about the black box model. 

> [Permutation Feature Importance](https://christophm.github.io/interpretable-ml-book/feature-importance.html#feature-importance) 
measures the increase in the prediction error of the model after feature values are permuted. 
Therefore the importance of a feature is calculated by the amount of model's prediction error. 

## 1.2. Fairness
Artificial intelligence and machine learning systems can display unfair behavior. One way to define unfair behavior is by its harm, or impact on people. 
Unfairness in AI systems can result in the following unintended consequences, for example, reinforcing biases and stereotypes that already reflected in the data itself could result in, say, 
ithholding opportunities or resources from individuals. It could also mean that a system work well for one group of people, and not as well for another. 
Many aspects of fairness can’t be captured or represented by metrics. There are tools and practices that can improve fairness in the design and development of AI systems.

The two key steps are [assess](https://docs.microsoft.com/en-us/azure/machine-learning/concept-fairness-ml#assess-fairness-in-machine-learning-models) and 
[mitigate](https://docs.microsoft.com/en-us/azure/machine-learning/concept-fairness-ml#mitigate-unfairness-in-machine-learning-models). 
Similar to the above, Fairness be solely *can not* be solved by technical method, rather human will need to be involved in assessment and mitigation. 

**Tool**: [FairLearn](https://github.com/fairlearn/fairlearn) is adopted and has made interactive visualisation tool as part of AML

![AML Fairness Tool](/assets/aml-responsible-ai/fairness.png)

- **Assess**
    - 2-class parity metrics   
        - accuracy
        - error rate 
        - precision
        - recall
        - MEA
        - ...
- **Mitigate**
    - Parity constraints by
        - demographic
        - equalised odds
        - equal opportunity
        - bounded group loss
    - Algorithms available
        - Reduction: re-weighting traing datasets
        - Post-Processing: derive transformation from model predictions

# 2. Privacy protection
AML has 2 concepts of Privacy Protection, they are **Differential Privacy** and **Data Encryption**

![AML Privacy Tool](/assets/aml-responsible-ai/privacy.png)

**Differential Privacy** approach add randomness to the original data so that it is marginally different from the original data,
so that users of the data can't identify the true individual data points. This may be required for regulatory compliance, depending on jurisdiction. 

**Tool**: [`SmartNoise`](https://github.com/opendifferentialprivacy/smartnoise-core)

**Data Encryption** Homomorphic encryption allows for computations to be done on encrypted data without requiring access to a secret (decryption) key. 
The results of the computations are encrypted and can be revealed only by the owner of the secret key. 
Using homomorphic encryption, cloud operators will never have unencrypted access to the data they're storing and computing on. 

**Tool**: [`MicrosoftSEAL`](https://pypi.org/project/encrypted-inference/)

# 3. Auditable Trails
Documenting the right information in the model development process is key to making responsible decisions at each stage; this allow an auditable trail. 
While AML captures details of each ML experiment and its associated information, such as data version used, performance metrics, model parameters etc, 
it is strongly advisable to have documentation to include contents such as:
- Intended use
- Model architecture
- Training data used
- Evaluation data used
- Training model performance metrics
- Model understanding
- Fairness assessments, mitigation
- ...

![AML Auditable Tool](/assets/aml-responsible-ai/auditable-trail.png)

# References
- https://docs.microsoft.com/en-us/azure/machine-learning/concept-responsible-ml
- https://docs.microsoft.com/en-us/azure/machine-learning/concept-fairness-ml
- https://docs.microsoft.com/en-us/azure/machine-learning/how-to-machine-learning-interpretability
- https://docs.microsoft.com/en-us/azure/machine-learning/concept-differential-privacy

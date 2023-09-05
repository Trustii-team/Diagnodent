![trustii logo](/HeroImage.png)

# Diagnodent data challenge introduction
This repository contains the [Diagnodent](https://www.trustii.io/post/diagnodent) data challenge result including best notebooks source code and documentation.

The Diagnodent Data Challenge is led by Pr Agnès Bloch-Zupan (PU-PH professor, clinician, rare disease expert, coordinator of the Strasbourg University Hospital, Reference center for rare oral and dental diseases and associated network, researcher at IGBMC, Université de Strasbourg, CNRS- UMR7104, INSERM U1258) and supported by the D-IA-GNO-DENT consortium. This consortium (members below), in partnership with the Health Data Hub, proposes a Data Challenge on the theme of rare dental diseases. 

Oral pathologies or anomalies are often the little known expression of rare diseases of genetic origin. These anomalies are receiving increasing attention because of their diagnostic or even predictive character. They are classified into dental anomalies of number, shape, size, structure, root formation and eruption and correspond to specific developmental and genetic problems. They are fixed in time by mineralisation. They are isolated or associated with other symptoms in syndromes.

900 rare diseases have a dento/oro/facial component. Clinical diagnoses and identification of the genes involved are difficult to make and to implement, leading patients and their families into diagnostic wandering. However, there are diagnostic signatures recognised by experts in the field and supported by phenotype/genotype correlations (D4/phenodent database/NGS GenoDENT panel).

The goal of the competition is to develop an AI solution to aid in the diagnosis of rare dental diseases based on the analysis of photographs and X-rays of the mouth and teeth. These genetic diseases, which affect multiple organs and systems, are recognised through abnormalities in teeth fixed over time by mineralisation.

# The Challenge Results

#### Note : According to the organizer's rules, the challenge was limited to European Union citizens.
* 84 participants from multiple countries around Europe
* 1451 submissions during the 3 months of the challenge
* Best F1 Macro score 0.848 on the private portion of the test set

# The Development Environment 

All the models of the Diagnodent challenge were built on trustii.io hosted Jupyterhub environnement, each team had access to a notebook session holding 3 vCPUs, 25GB of RAM, 20GB of persistent storage and 12 GB GPU hardware accelerator (nVidia Tesla k80)

# Best Notebooks

##### Note : To determine the final scores, a weighted average was used: 80% of the score came from the F1 Macro generated by trustii.io platform, while 20% was based on subjective criteria such as code interpretability and inference speed decided by the organizer of the challenge. A basic model, "DummyClassifier", which predicts the most frequent label for each target, was established as a baseline. This reference allowed for recalibration of the F1Score between 0 (performance equivalent to the DummyClassifier) and 20 (if the Classifier predicts all observations perfectly). This recalibration was done using a MinMaxScaler.

| Ranking    | Team               | Score Public Leaderboard | Score Private Leaderboard | Final Score | Winning model summary |
|:----------:|:------------------:|:-------------------:|:-------------------:|:-----------------:|:-------------------------------------------:|
| 2          | EISBM             | 0.7729301468421065  | 0.7861260189304708  | 14.3295/20 | The team employed libraries like skLearn, pyTorch, OpenCV, and GRADcam due to familiarity and reproducibility. Upon analyzing the dataset's target columns, genes appearing in fewer than four patients were deemed unpredictable and set to "None," retaining five genes. The team adopted ResNet and EfficientNet models, with the final layer modified to have four separate heads for multi-class classification tasks. Using the cross-entropy loss function and normalization techniques, they divided the dataset into a 90-10 train-validation split. To counter overfitting, image augmentations were applied, except for the Normal Cohort. Best results were achieved with the EfficientNetV2L model, a 400x400 image resolution, and a batch size of six. A learning rate of 0.0001 ensured smooth convergence. After evaluating individual heads, the losses for Cohort and AI_Type were doubled for optimal performance. |
| 1          | Unistra    | 0.7708679388728454       | 0.7748704702609973        | 14.6555/20 | The team undertook an extensive exploration of the dataset, identifying 34 unique target combinations with notable imbalances. Rather than employing a singular model for all targets, the approach was to use individual sequential models to improve both robustness and explainability. The modeling process consisted of a three-step approach: first predicting the Cohort target, followed by AI Type and isolated/syndromic predictions, and concluding with a statistical method for Responsible Gene prediction. During CNN training, the team employed custom data augmentation techniques. The DenseNet121, a pretrained model, was chosen due to its architecture and ability to recognize features. Additionally, the team applied a sigmoid activation function and the binary_crossentropy loss function to treat each class as an independent binary classification, thus assisting in medical diagnostics. In their closing remarks, the team provided several recommendations for the future, such as fostering deeper collaboration with dental professionals, exploring potential modifications to the models, and emphasizing the value of increasing the dataset with more images. |
| 3          | IQVIA             | 0.7670351199543314       | 0.7719777154823506        | 12.5696/20 | The team crafted their model through rigorous trials and exploration, with in-depth explanations available in their notebook. Noting the scarcity of images, they leveraged state-of-the-art encoders pre-trained on the ImageNet dataset. Specifically, for image data, a ResNext model with 1000 output neurons was employed as the encoder. Subsequent custom layers, termed classifiers, funneled outputs into four distinct categories. Each category took inputs from 64 neurons, barring AI_Type which also utilized neurons from the Cohort output. In the case of Panoramics, a similar architecture was used, but with the DEIT encoder being more apt for smaller datasets like panoramics. For visual clarity, a model diagram was attached. The strategy involved using two distinct models for photos and panoramics, ensuring predictions could be given even if only one image type was available. Further technical details are available in their notebook in the repository above. |

For more details check out each winning solution report and source code in the 'repository' above.

# The Dataset

The dataset has been provided by HUS (Hopitaux Universitaires de Strasbourg) and prepared with Trustii.io data scientists. 

Participants have been provided with a dataset of oral images, each annotated with labels indicating the presence or absence of specific symptoms of AI under different severity levels.

The dataset has the following caracteristics :
* Amelogenesis imperfecta --> 166
* Dentine anomalies --> 50
* Control --> 100
* Intraoral colour photographs (4 to 10/individuals)
* Panoramic radiographs
* Colour
* Surface
* texture
* Shape/size

If you are interested by accessing the dataset or collaborating with Trustii.io and HUS on this project, please reach out to us at contact@trustii.io.

# More information

To access the challenge forum discussions and the dataset description, check out the Diagnodent challenge webpage at https://app.trustii.io.



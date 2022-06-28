# Aragon Conviction Voting

This cadCAD model and notebook series is a collaboration between <a href="https://aragon.org" target="_blank">Aragon Project</a>, <a href="https://1hive.org" target="_blank">1Hive</a>, <a href="https://block.science" target="_blank">BlockScience</a>, and <a href="https://commonsstack.org" target="_blank">The Commons Stack</a>. A brief table of contents follows to explain the file structure of the various documents produced in this collaboration.

You can access the GitHub repo for this project here: <a href="https://github.com/1Hive/conviction-voting-cadcad" target="_blank">GitHub Repo</a>.

## Table of Contents
### 1. Supporting documentation for context
* <a href="https://github.com/BlockScience/Aragon_Conviction_Voting/blob/master/README.md" target="_blank">Readme doc</a> (you are here): For an overview of Conviction Voting and what exactly we're trying to do with this model, start right here
* <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/algorithm_overview.ipynb" target="_blank">Conviction Voting Algorithm Overview</a>: For a deeper understanding of the CV algorithm, including its mathematical derivation, read this document
* <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/models/v3/Deriving_Alpha.ipynb" target="_blank">Deriving the Alpha Parameter</a>: For an in-depth look at the specific considerations around the alpha parameter, which sets the half life decay of conviction, read this notebook
* <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/models/v3/Trigger_Function_Explanation.ipynb" target="_blank">Explaining the Trigger Function</a>: For an in-depth look at the trigger function equation and how proposals pass from candidate to active status, read this notebook



### 2. Simulation Notebooks

* <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/a5bf8accbc832c34e3cc7f206106edd89ea0aa7d/models/v3/Aragon_Conviction_Voting_Model.ipynb" target="_blank">V3 - 1Hive model</a>: The latest notebook iteration of CV, modeling 1Hive's deployment
* <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/models/v2/Aragon_Conviction_Voting_Model.ipynb" target="_blank">V2 - Increased complexity model</a>: a former version of the CV model with increased mechanism complexity over v1
* <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/models/v1/Aragon_Conviction_Voting_Model.ipynb" target="_blank">V1 - Initial model</a>: the simplest version of the CV model. Start here if you are looking to understand and replicate this model in cadCAD
* <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/model_structure.ipynb" target="_blank">Model Structure</a>: a deeper look into the structure of the cadCAD model. Read this document if you are learning how to work with system modelling in cadCAD.
<br>

___
<br>
 

# Background information & concepts addressed

## What does this cadCAD model do?
In cyber-physical systems like international power grids, global flight networks, or socioeconomic community ecosystems, engineers model simulated replicas of their system, called digital twins. These models help to manage the complexity of systems that have trillions of data points and are constantly in flux. These simulations channel the information into pathways that allow humans to understand what is going on in their ecosystem at a high level, so they can intervene where and as appropriate. (Like hitting a breaker switch when a fault is cleared in a power system).

![img](https://i.imgur.com/kb4Tnh6.jpg)

Digital twins can be considered like a flight simulator, which can be used to run your system through a billion different "tests", varying one parameter at a time, to see what effects may throw your system out of balance. As engineers with public safety in mind, we must understand the tipping points of our systems, and ensure mechanisms are in place to push the system back towards balance if and when they enter their boundary conditions of safety.

This cadCAD model is a digital twin of Conviction Voting, as applied in the 1Hive DAO ecosystem. It can be used to provide operational support in decision making both during the design stage, and also in the continuous governance of the 1Hive system, providing <a href="https://medium.com/block-science/computer-aided-governance-cag-a-revolution-in-automated-decision-support-systems-9faa009e57a2" target="_blank">Computer Aided Governance</a> for 1Hive members. 

The notebooks contained here are a mix of code snippets, explainer content, simulations, and a whole lot of background to get you more familiar with CV as a concept, and perhaps even diving into modelling similar systems, or extending this model even further using cadCAD. If you have any questions about this model or how to build with it in cadCAD, feel free to email jeff@block.science.

<br>

## Conviction Voting Basics

<a href="https://medium.com/commonsstack/conviction-voting-a-novel-continuous-decision-making-alternative-to-governance-62e215ad2b3d" target="_blank">Conviction Voting</a> is a novel decision making process used to estimate real-time collective preference in a distributed work proposal system. Voters continuously express their preference by staking tokens in support of proposals they would like to see approved, with the conviction (i.e. weight) of their vote growing over time. Collective conviction accumulates until it reaches a set threshold specified by a proposal according to the amount of funds requested, at which point it passes and funds are released so work may begin. Conviction voting improves on discrete voting processes by allowing participants to vote at any time, and eliminates the need for consensus on each proposal. This eliminates the governance bottleneck of large distributed communities, where a quorum of participants is required to vote on every proposal. 

![img](https://github.com/1Hive/conviction-voting-cadcad/raw/master/images/cv_background_1.PNG)

Legacy voting systems face several difficulties in transforming private, distributed, continuous and time varying individual signals (e.g. desiring our roads to be safer) into public, centralized, discrete and event-based collective outcomes (e.g. filling potholes on streets in your neighbourhood). Conviction Voting is a real-time governance tool designed to aggregate collective preferences, expressed continuously. 

![](https://github.com/1Hive/conviction-voting-cadcad/raw/master/images/cv_background_2.png)

As our governance toolkits continue to expand with novel tools like Conviction Voting, we can consider designing governance systems in the context of the community to which they belong. In the 1Hive community, holding Honey tokens gives you certain rights in the 1Hive organization. Above, we consider the rights granted, how those rights are controlled, the attack vectors they present, and how those vectors can be mitigated.

![](https://github.com/1Hive/conviction-voting-cadcad/raw/master/images/cv_background_3.png)

Conviction Voting offers us new insight into the collective intent of our communities. It offers us a richer signal of the emergent and dynamic preferences of a group, such that we can better understand and discuss important issues as communities. It eliminates attack vectors of ad hoc voting such as last minute vote swings, and reduces user friction by not requiring set times to cast a vote.  

## Different Flavors of Conviction Voting

The design space for this new governance tool is wide and unexplored. From its academic origins in Dr. Zargham's PhD research in multi agent coordination systems, Conviction Voting was called <a href="https://github.com/BlockScience/conviction/blob/master/social-sensorfusion.pdf" target="_blank">Social Sensor Fusion</a> and was a continuous 'fusion' of individual desires into a collective sentiment signal. This suggests there could be multiple "flavors" of Conviction Voting:

* **Discrete proposal CV**: Like the 1Hive or Commons Stack model, this version of CV fuses continuous preferences into a conviction signal, passing the proposal at a specific point in time, when sufficient community support has been reached. 

![img](https://i.imgur.com/cx5pCxH.png)

* **Continuous parameter CV:** A community may wish to have certain aspects of their socioeconomic system to be continuously decided by collective sentiment. Perhaps the rate of a community token entry/exit (Tobin) tax, or the rate of community UBI. 

![img](https://i.imgur.com/5hDgMTk.png)

There are likely to be many more useful applications of this real-time governance tool in community decision making and beyond. We look forward to continuing this research and creating the open source foundations of models which can be iterated towards widely varying scenarios for facilitating collective intelligence.

## Conviction Voting In-Depth
Conviction voting is based on a linear system akin to a capacitor which "charges up" dynamically and proposals pass when a certain level of collective energy is reached. The details are explained and demonstrated throughout this repo but the best place to start is the <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/algorithm_overview.ipynb" target="_blank">Conviction Voting Algorithm Overview</a>. For more details on the charging up mechanics and the alpha parameter see the <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/models/v3/Deriving_Alpha.ipynb" target="_blank">Deriving Alpha Parameter Explainer</a> notebook and for more details on the proposal passing mechanism,  see the <a href="https://nbviewer.jupyter.org/github/BlockScience/Aragon_Conviction_Voting/blob/master/models/v3/Trigger_Function_Explanation.ipynb" target="_blank">Trigger Function Explainer</a> notebook.

<br>

___

# Current CV Experiments

## 1Hive
The <a href="https://www.1hive.org" target="_blank">1Hive</a> community has been actively developing Conviction Voting contracts in collaboration with BlockScience and the Commons Stack since early 2019. They currently have a DAO live on the xDAI network at <a href="https://www.1hive.org" target="_blank">1hive.org</a> that uses a native governance token (Honey) to allocate funds to proposals via Conviction Voting.

To see Conviction Voting deployed in smart contracts with a basic user interface, check out the <a href="https://github.com/1Hive/conviction-voting-app" target="_blank">1Hive Github</a>.

## Commons Simulator

The <a href="https://www.commonsstack.org" target="_blank">Commons Stack</a> has been working on a 'Commons Simulator' to facilitate user understanding of these novel governance tools, by casting them in a futuristic solarpunk storyline. Progress on the simulation and it's Conviction Voting work can be viewed in <a href="https://github.com/commons-stack/coodcad" target="_blank">the Commons Stack Github repo</a>.

<br>

___

## What is cadCAD?
cadCAD (complex adaptive dynamics Computer-Aided Design) is a python based modeling framework for research, validation, and Computer Aided Design of complex systems. Given a model of a complex system, cadCAD can simulate the impact that a set of actions might have on it. This helps users make informed, rigorously tested decisions on how best to modify or interact with the system in order to achieve their goals. cadCAD supports different system modeling approaches and can be easily integrated with common empirical data science workflows. Monte Carlo methods, A/B testing and parameter sweeping features are natively supported and optimized for.




cadCAD links:
* <a href="https://community.cadcad.org/t/introduction-to-cadcad/15" target="_blank">https://community.cadcad.org/t/introduction-to-cadcad/15</a>
* <a href="https://community.cadcad.org/t/putting-cadcad-in-context/19" target="_blank">https://community.cadcad.org/t/putting-cadcad-in-context/19</a>
* <a href="https://github.com/cadCAD-org/demos" target="_blank">https://github.com/cadCAD-org/demos</a>

<br> 

## Model Reproducibility
In order to reperform this code, we recommend the researcher use the following link
<a href="https://www.anaconda.com/products/individual" target="_blank">https://www.anaconda.com/products/individual</a> to download Python 3.7. To install the specific version of cadCAD this repository was built with, run the following code:
`pip install cadCAD==0.4.21`

Then run cd Aragon_Conviction_Voting to enter the repository. Finally, run jupyter notebook to open a notebook server to run the various notebooks in this repository.

Check out the <a href="https://community.cadcad.org/t/python-newbies-setup-for-cadcad/101" target="_blank">cadCAD forum</a> for more information about installing and using cadCAD.

<br>

___

## Further Background Reading

### Systems Thinking
* <a href="https://community.cadcad.org/t/introduction-to-systems-thinking/18" target="_blank">https://community.cadcad.org/t/introduction-to-systems-thinking/18</a>
* <a href="https://community.cadcad.org/t/working-glossary-of-systems-concepts/17" target="_blank">https://community.cadcad.org/t/working-glossary-of-systems-concepts/17</a>

### Token Engineering

* <a href="https://blog.oceanprotocol.com/towards-a-practice-of-token-engineering-b02feeeff7ca" target="_blank">https://blog.oceanprotocol.com/towards-a-practice-of-token-engineering-b02feeeff7ca</a>
* <a href="https://assets.pubpub.org/sy02t720/31581340240758.pdf" target="_blank">https://assets.pubpub.org/sy02t720/31581340240758.pdf</a>

### Complex systems

* <a href="https://ergodicityeconomics.com/lecture-notes/" target="_blank">https://ergodicityeconomics.com/lecture-notes/</a>
* <a href="https://www.frontiersin.org/articles/10.3389/fams.2015.00007/full" target="_blank">https://www.frontiersin.org/articles/10.3389/fams.2015.00007/full</a>
* <a href="https://epub.wu.ac.at/7433/1/zargham_paruch_shorish.pdf" target="_blank">https://epub.wu.ac.at/7433/1/zargham_paruch_shorish.pdf</a>

### Systems Engineering

* <a href="http://systems.hitchins.net/systems-engineering/se-monographs/seessence.pdf" target="_blank">http://systems.hitchins.net/systems-engineering/se-monographs/seessence.pdf</a>

___

## Funding Continued Work

This Conviction Voting model will continue to be iterated and modified to suit varying use cases, with increased functionality (next steps are discussed at the end of the v3 model notebook). If you would like to support this work, please consider voting in support of our proposal in the Aragon Conviction Funding Pilot with your ANT tokens: <a href="https://conviction.aragon.org/#/proposal/7" target="_blank">https://conviction.aragon.org/#/proposal/7</a>

Alternatively, you can contribute ETH or other ERC-20 tokens to this address: 

**[0x422ae3412510d6c877b259dad402ddeaf1fdb28e](https://etherscan.io/address/0x422ae3412510d6c877b259dad402ddeaf1fdb28e)**

All funds will go towards additional work on this model, to continue to build Conviction Voting into a useful tool for collective decision making. 

Thanks very much for your support! 🙏🎉

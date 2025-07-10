---

# 🧬 De Novo Drug Design Using GenAI

This project focuses on de novo molecular design using generative AI, specifically by adapting the **REINVENT4** platform to run within **Google Colab**. Since REINVENT4 is not natively supported in Colab, several adjustments were made to get it working smoothly, including the use of **Miniconda** and modification of REINVENT’s plugin system.

---

## 🚀 Project Overview

The aim of this project is to explore and implement a full pipeline for **drug discovery** using generative models:

* Install and configure REINVENT4 in a restricted Colab environment
* Perform **transfer learning** on REINVENT's pre-trained molecular generator using known inhibitors
* Extend REINVENT to run **reinforcement learning** with a custom **QSAR scoring function**
* Integrate a **Random Forest** QSAR model using **Scikit-learn**, trained on **Morgan fingerprints** (512 bits, radius 3)

---

## 🔧 Colab Compatibility

REINVENT4 is originally built for a local or HPC Linux environment with Conda and specific path dependencies. To make it work in Colab:

* **Miniconda** is installed and configured manually
* A custom environment is created for REINVENT and its dependencies
* The REINVENT source code is patched to support Colab execution
* Custom plugins (such as a QSAR component) are loaded by overriding REINVENT’s strict plugin registration system

---

## 🧠 Transfer Learning Phase

In this phase, we fine-tune REINVENT's SMILES-generating RNN using a dataset of known active inhibitors. The goal is to bias molecule generation toward a particular chemical space relevant to a biological target. This is achieved by updating the weights of the prior model using a log-likelihood-based training loop provided by REINVENT.

---

## 🧪 Reinforcement Learning with QSAR Scoring

The RL phase introduces a custom scoring function that evaluates generated molecules based on predicted bioactivity. For this:

* A **Scikit-learn Random Forest Regressor** is trained on a dataset of known inhibitors
* The input features are **Morgan fingerprints** with a bit length of 512 and a radius of 3
* The trained model is wrapped as a REINVENT-compatible scoring component
* The REINVENT scoring system is patched to load and use this custom model during RL

This allows REINVENT to guide molecule generation based on QSAR predictions rather than docking scores or physicochemical properties alone.

---



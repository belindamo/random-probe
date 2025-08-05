# Distributional Constraints and MMD-based Methods

This section analyzes methods that use Maximum Mean Discrepancy (MMD) and other distributional distance measures for regularizing autoencoders.

## 1. Bridging the ELBO and MMD (μ-VAE) (2019)

### Problem
VAE's ELBO objective, specifically the KL divergence term, leads to posterior collapse when generator has too much capacity, especially with small datasets and high latent dimensions.

### Prior Assumptions in Literature
- ELBO with KL divergence is the optimal objective for variational autoencoders
- KL divergence provides adequate regularization for posterior matching
- Distributional matching can only be achieved through KL-based objectives

### Key Insight
Replace KL term in ELBO with Maximum Mean Discrepancy (MMD) objective, which provides more flexible distributional matching and is less prone to posterior collapse.

### Technical Approach
- Replaces KL divergence term with MMD-based objective
- Introduces "latent clipping" technique to control distances between samples in latent space
- μ-VAE model designed with new objective function
- MMD provides more robust distributional matching than KL divergence

### Evaluation
- Tested on MNIST and Fashion-MNIST datasets
- Outperformed standard ELBO and β-VAE objectives
- Less prone to posterior collapse with better reconstruction and generation quality
- Learned representations effective for downstream classification tasks

### Impact
Demonstrated viability of MMD as alternative to KL divergence in VAEs, showing that different distributional distances can fundamentally improve autoencoder training and preventing posterior collapse.

---

## 2. Cauchy-Schwarz Regularized Autoencoder (2021)

### Problem
VAE's default Gaussian prior choice imposes strong constraints on ability to represent true posterior, degrading performance. Gaussian Mixture Model (GMM) would be richer prior but cannot be handled efficiently within VAE framework due to intractable KL divergence for GMMs.

### Prior Assumptions in Literature
- Gaussian priors sufficient for most VAE applications
- KL divergence necessary for tractable optimization in variational autoencoders
- GMM priors incompatible with efficient VAE training

### Key Insight
Introduce constrained objective based on Cauchy-Schwarz divergence, which can be computed analytically for GMMs, enabling incorporation of richer multi-modal priors into autoencoding framework.

### Technical Approach
- Uses Cauchy-Schwarz divergence instead of KL divergence for GMM priors
- Provides analytical solution for Gaussian mixture priors
- Enables efficient inference with multi-modal prior distributions
- Maintains tractable optimization while increasing prior flexibility

### Evaluation
- Experiments on range of datasets showing improved density estimation
- Better performance in unsupervised clustering and semi-supervised learning
- Enhanced face analysis capabilities
- Demonstrated superior performance over standard VAE objectives

### Impact
Showed that alternative divergence measures can enable richer prior distributions in autoencoders, opening door to more flexible generative models beyond simple Gaussian priors.

---

## 3. InfoVAE: Balancing Learning and Inference (implied from MAE paper)

### Problem
Traditional VAE optimization can completely disconnect reconstruction and regularization objectives, where ELBO maximization doesn't necessarily lead to meaningful latent variable learning.

### Prior Assumptions in Literature
- ELBO optimization naturally balances reconstruction and regularization
- KL term alone provides sufficient regularization for meaningful representations
- Mutual information between data and latent variables doesn't need explicit consideration

### Key Insight
Explicitly incorporate mutual information terms in the objective to ensure meaningful connection between data and latent variables, preventing the disconnect that leads to posterior collapse.

### Technical Approach
- Decomposes ELBO to explicitly show mutual information terms
- Balances mutual information between data and latent variables with regularization
- Provides more principled approach to preventing posterior collapse
- Maintains variational inference framework while improving information flow

### Evaluation
- Demonstrated improved representation learning
- Better balance between reconstruction and regularization
- Showed explicit connection between information theory and VAE objectives

### Impact
Established information-theoretic perspective on VAE training, influencing subsequent work on mutual information maximization and providing theoretical foundation for understanding posterior collapse.

---

## 4. Improving VAEs with Density Gap-based Regularization (2022)

### Problem
Optimizing ELBO often leads to posterior collapse (KL vanishing) and hole problem (mismatch between aggregated posterior and prior distribution). Existing methods make trade-offs between these problems rather than solving both.

### Prior Assumptions in Literature
- Cannot simultaneously solve posterior collapse and hole problem
- Trade-offs between different VAE problems are inevitable
- Aggregated posterior-prior mismatch is secondary concern

### Key Insight
Introduce novel regularization based on probabilistic density gap between aggregated posterior distribution and prior distribution to jointly solve both posterior collapse and hole problem.

### Technical Approach
- Regularization based on density gap between aggregated posterior and prior
- Addresses both posterior collapse and hole problem simultaneously
- Maintains computational tractability while improving distributional matching
- First method to jointly solve both fundamental VAE problems

### Evaluation
- Experiments on language modeling, latent space visualization, and interpolation
- Outperformed existing methods in latent-directed generation
- Demonstrated simultaneous solution to both posterior collapse and hole problems

### Impact
First work to jointly address multiple fundamental VAE problems, showing that comprehensive solutions are possible rather than accepting trade-offs between different issues.

---

## 5. Variational Rank Reduction Autoencoders (VRRAEs) (2025)

### Problem
Deterministic Rank Reduction Autoencoders (RRAEs) provide powerful regularization through truncated SVD but are not suitable for generative purposes due to deterministic nature. VAEs enable generation but lack RRAE's regularization benefits.

### Prior Assumptions in Literature
- Deterministic and probabilistic approaches are fundamentally incompatible
- SVD regularization cannot be combined with variational inference
- Must choose between generation capability and rank reduction benefits

### Key Insight
Combine advantages of RRAEs and VAEs by carefully sampling RRAE latent space and regularizing with KL divergence, showing that SVD regularization reduces posterior collapse while maintaining generative capabilities.

### Technical Approach
- Leverages SVD regularization from RRAEs within VAE framework
- Careful sampling strategy for latent space of RRAEs
- Additional KL regularization similar to VAEs
- SVD regularization inherently reduces posterior collapse possibility

### Evaluation
- Outperformed both RRAEs and VAEs on multiple metrics
- Demonstrated on synthetic dataset showing robustness against collapse
- Superior performance on MNIST, CelebA, and CIFAR-10 for generation and interpolation
- Better FID scores compared to standard VAEs

### Impact
Demonstrates that deterministic regularization techniques can be successfully integrated with probabilistic frameworks, opening new directions for combining different autoencoder paradigms.
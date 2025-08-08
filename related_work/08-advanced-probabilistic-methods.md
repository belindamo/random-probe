# Advanced Probabilistic and Geometric Methods

## Overview

Recent advances in probabilistic methods for autoencoders explore alternative approaches to standard VAE formulations, including spherical geometry, contrastive learning, and advanced sampling techniques.

## Key Papers

### S2WTM: Spherical Sliced-Wasserstein Autoencoder for Topic Modeling (2025)
**Authors**: Suman Adhya, et al.  
**Citation**: Adhya, S., et al. (2025). S2WTM: Spherical Sliced-Wasserstein Autoencoder for Topic Modeling. arXiv preprint arXiv:2507.12451.

#### CS197 Analysis

**Problem**: VAE-based neural topic models suffer from posterior collapse when using hyperspherical geometry, despite theoretical advantages for text modeling.

**Assumption in Prior Work**: von Mises-Fisher priors with KL divergence sufficient for hyperspherical VAE training.

**Insight**: Spherical Sliced-Wasserstein distance provides superior distributional matching on unit hypersphere compared to KL divergence.

**Technical Overview**:
- Uses von Mises-Fisher prior on unit hypersphere
- Replaces KL divergence with Spherical Sliced-Wasserstein distance
- Leverages geometric properties of hyperspherical space
- Addresses posterior collapse through better distance measure

**Proof**: Experimental validation showing improved topic coherence and diversity compared to standard VAE approaches.

**Impact**: Demonstrates that alternative distance measures (beyond KL and standard Wasserstein) can address posterior collapse in specialized geometries.

### Probabilistic Variational Contrastive Learning (VCL) (2025)
**Authors**: Minoh Jeong, Seonho Kim, Alfred Hero  
**Citation**: Jeong, M., Kim, S., & Hero, A. (2025). Probabilistic Variational Contrastive Learning. arXiv preprint arXiv:2506.10159.

#### CS197 Analysis

**Problem**: Contrastive learning methods lack principled uncertainty quantification and suffer from dimensional collapse.

**Assumption in Prior Work**: Deterministic embeddings adequate for contrastive representation learning.

**Insight**: Contrastive objectives can be interpreted as surrogate reconstruction terms in VAE framework, enabling probabilistic embeddings.

**Technical Overview**:
- Interprets InfoNCE loss as surrogate reconstruction term
- Adds KL divergence regularizer to uniform prior on unit hypersphere
- Models posterior as projected normal distribution
- Enables sampling of probabilistic embeddings

**Proof**: Experimental validation showing mitigation of dimensional collapse and improved mutual information with class labels.

**Impact**: Bridges contrastive learning and VAE frameworks, providing alternative perspective on distributional matching in representation learning.

### Preventing Model Collapse in Gaussian Process Latent Variable Models (2024)
**Authors**: Ying Li, Zhidi Lin, Feng Yin, Michael Minyi Zhang  
**Citation**: Li, Y., Lin, Z., Yin, F., & Zhang, M. M. (2024). Preventing Model Collapse in Gaussian Process Latent Variable Models. arXiv preprint arXiv:2404.01697.

#### CS197 Analysis

**Problem**: Gaussian Process Latent Variable Models suffer from model collapse due to inadequate kernel flexibility and improper projection noise selection.

**Assumption in Prior Work**: Standard GP kernels and fixed projection noise sufficient for meaningful latent representations.

**Insight**: Spectral mixture kernels with differentiable random Fourier features can prevent collapse while maintaining computational efficiency.

**Technical Overview**:
- Integrates spectral mixture (SM) kernel
- Uses differentiable random Fourier feature (RFF) approximation
- Learns kernel hyperparameters, projection variance, and latents jointly
- Variational inference framework for scalability

**Proof**: Empirical validation showing superior performance compared to VAEs and other GPLVM variants.

**Impact**: Demonstrates that model collapse is not VAE-specific but affects broader class of latent variable models, supporting Random Probe's general approach.

## Connection to Random Probe Method

These advanced methods provide theoretical and empirical support for Random Probe:

1. **S2WTM's spherical Sliced-Wasserstein** approach shows success of alternative distance measures for distributional matching
2. **VCL's probabilistic contrastive learning** demonstrates that distributional thinking improves representation learning across domains
3. **GPLVM collapse prevention** shows that direct attention to distributional properties prevents collapse across model classes

## Theoretical Connections

1. **Alternative distance measures**: All three papers use non-KL distance measures for better distributional matching
2. **Geometric considerations**: Spherical and projected geometries enable tractable distributional constraints
3. **Random projections**: RFF methods in GPLVM relate to Random Probe's dimensional reduction approach

## Research Gaps

1. **Cross-method comparisons** between different distance measures lacking
2. **Computational complexity** analysis for advanced probabilistic methods incomplete
3. **Theoretical connections** to MMD and optimal transport underexplored
4. **Scalability** to very high-dimensional problems uncertain

---
*Analysis completed using CS197 methodology*
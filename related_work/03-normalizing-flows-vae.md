# Normalizing Flows and VAE Integration

This section analyzes methods that combine normalizing flows with VAEs to improve posterior flexibility and generation quality.

## 1. Improving VAE using Convex Combination Linear Inverse Autoregressive Flow (2017)

### Problem
Standard VAE assumes diagonal covariance matrix for encoder posterior q(z|x) = N(z|μ(x), diag(σ²(x))), which is insufficient and inflexible for matching true posterior distributions.

### Prior Assumptions in Literature
- Diagonal Gaussian posteriors sufficient for VAE performance
- Complex posterior distributions not necessary for most applications
- Normalizing flows require complex, computationally expensive transformations

### Key Insight
Enrich variational posterior using normalizing flows with volume-preserving linear transformations, specifically through convex combinations of lower-triangular matrices with ones on diagonal.

### Technical Approach
- Introduces volume-preserving normalizing flow using convex combinations
- Multiple lower-triangular matrices with diagonal ones combined via convex combination
- Maintains computational efficiency while increasing posterior flexibility
- Preserves volume (determinant = 1) ensuring tractable likelihood computation

### Evaluation
- Outperformed other volume-preserving flows on MNIST and Histopathology data
- Competitive with state-of-the-art linear normalizing flows
- Demonstrated improved posterior flexibility with minimal computational overhead

### Impact
Established foundation for efficient normalizing flow integration in VAEs, showing that simple linear transformations can significantly improve posterior approximation quality.

---

## 2. TarFlow: Transformer-based Normalizing Flows (2024)

### Problem
Normalizing flows haven't achieved the same level of success as diffusion models in high-quality generation, and previous flow architectures lack the scalability and expressiveness needed for complex distributions.

### Prior Assumptions in Literature
- Normalizing flows inherently limited in generation quality compared to diffusion models
- Autoregressive flows cannot achieve competitive performance at scale
- Likelihood-based models fundamentally inferior for generation tasks

### Key Insight
Combine expressive power of normalizing flows with structured modeling capabilities of autoregressive Transformers, enabling scalable high-quality generation while maintaining exact likelihood computation.

### Technical Approach
- Transformer Autoregressive Flow (TARFlow) architecture
- Alternates autoregression direction between layers
- Deep-shallow design: deep Transformer captures capacity, shallow blocks provide efficiency
- Novel guidance algorithm for improved sample quality
- End-to-end normalizing flow without discretization

### Evaluation
- State-of-the-art likelihood estimation results on images
- Sample quality and diversity comparable to diffusion models
- First successful demonstration of normalizing flows at large scale and high resolution
- Superior performance in both class-conditional and text-conditional generation

### Impact
Demonstrates that normalizing flows can compete with diffusion models in generation quality while maintaining unique advantages of exact likelihood computation and efficient sampling.

---

## 3. Normalizing Flow-based Bayesian Optimization (NF-BO) (2025)

### Problem
Latent Bayesian Optimization (LBO) approaches using VAEs suffer from value discrepancy problem due to reconstruction gap between input and latent spaces, propagating errors throughout optimization process.

### Prior Assumptions in Literature
- VAE reconstruction gap acceptable for optimization applications
- Approximate encoder-decoder sufficient for latent space optimization
- Perfect reconstruction not necessary for effective latent optimization

### Key Insight
Use normalizing flows as generative model to establish one-to-one encoding with left-inverse decoding function, completely eliminating reconstruction gap and value discrepancy problem.

### Technical Approach
- SeqFlow: autoregressive normalizing flow for sequence data
- One-to-one mapping eliminates reconstruction gap
- Dynamic candidate sampling strategy adjusting exploration probability per token
- Maintains invertibility guarantees of normalizing flows

### Evaluation
- Superior performance in molecule generation tasks
- Significantly outperformed traditional and recent LBO approaches
- Demonstrated elimination of value discrepancy problem

### Impact
Shows that normalizing flows' invertibility can solve fundamental problems in latent optimization, extending their applicability beyond generation to optimization tasks.

---

## 4. STARFlow: Scaling Latent Normalizing Flows (2025)

### Problem
Normalizing flows struggle to achieve strong performance in high-resolution image synthesis, particularly at scales where diffusion models excel, limiting their practical applicability.

### Prior Assumptions in Literature
- Normalizing flows cannot scale to high-resolution generation effectively
- Latent space modeling inferior to direct pixel-level modeling for flows
- Complex guidance mechanisms necessary for high-quality flow generation

### Key Insight
Combine Transformer architectures with normalizing flows in latent space of pretrained autoencoders, using deep-shallow design and novel guidance for scalable high-resolution generation.

### Technical Approach
- Deep-shallow Transformer design for computational efficiency
- Modeling in latent space of pretrained autoencoders (more effective than pixel-level)
- Novel guidance algorithm boosting sample quality
- End-to-end normalizing flow with exact maximum likelihood training
- No discretization required

### Evaluation
- Competitive performance with state-of-the-art diffusion models in sample quality
- Successful demonstration at unprecedented scale and resolution for normalizing flows
- Effective in both class-conditional and text-conditional generation

### Impact
Establishes normalizing flows as viable alternative to diffusion models for high-resolution generation, proving their scalability and effectiveness at large scales.

---

## 5. Aligning Latent Spaces with Flow Priors (2025)

### Problem
Traditional distributional alignment using KL divergence is restrictive, particularly when target prior is only implicitly defined by samples rather than analytical distributions.

### Prior Assumptions in Literature
- KL divergence optimal for distributional alignment
- Explicit analytical priors necessary for effective regularization
- Likelihood evaluations and ODE solving necessary for flow-based alignment

### Key Insight
Leverage flow-based generative models as priors to align learnable latent spaces to arbitrary target distributions through flow matching objective that treats latents as optimization targets.

### Technical Approach
- Pretrains flow model on target features to capture distribution
- Flow model regularizes latent space via alignment loss
- Reformulates flow matching objective for latent optimization
- Eliminates expensive likelihood evaluations and ODE solving during optimization

### Evaluation
- Theoretical proof that alignment loss provides tractable surrogate for log-likelihood maximization
- Large-scale ImageNet experiments with diverse target distributions
- Demonstrated close approximation to negative log-likelihood landscape

### Impact
Provides new framework for latent space alignment using flows, enabling arbitrary target distributions without analytical tractability requirements.
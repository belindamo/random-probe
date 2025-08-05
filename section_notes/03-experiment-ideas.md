# Experiment Ideas

## Core Research Question
**Bit Flip**: Standard ELBO optimization with KL divergence regularization does NOT adequately ensure that learned posterior distributions conform to the assumed prior distribution N(0,I).

**Hypothesis**: The Random Probe (RP) method will provide superior distributional conformity, better latent space utilization, and improved generation quality compared to standard VAE training.

## Experiment 1: Core Validation - RP vs Standard VAE

### Thesis Statement
The Random Probe method achieves significantly better distributional conformity (measured by KS test p-values on projected latent samples) compared to standard VAE training across multiple datasets.

### Testable Hypotheses
1. **H1**: RP-VAE posterior samples will have p-values > 0.05 on Kolmogorov-Smirnov tests against N(0,1) in >80% of random projections, vs <50% for standard VAE
2. **H2**: RP-VAE will show higher active unit counts (>90% vs <70% for standard VAE)
3. **H3**: RP-VAE will achieve comparable or better reconstruction quality (ELBO scores within 5% of standard VAE)

### Experimental Design
- **Independent Variables**: Training method (Standard VAE vs RP-VAE), dataset (MNIST, CIFAR-10, CelebA)
- **Dependent Variables**: 
  - KS test p-values on 100 random projections per model
  - Active unit percentage (units with variance > 0.01)
  - ELBO scores on test set
  - FID scores for generation quality
- **Controls**: Same architecture, hyperparameters, training epochs, random seeds
- **Sample Size**: 5 independent runs per condition

### Validity Threats & Mitigations
- **Internal Validity**: Confounding architecture differences → Use identical base architectures
- **External Validity**: Dataset-specific effects → Test on 3 diverse datasets
- **Construct Validity**: KS test sensitivity → Supplement with Wasserstein-2 distance measurements

### Resources & Timeline
- **Computational**: 40 GPU-hours (2 methods × 3 datasets × 5 runs × ~1.3 hours each)
- **Timeline**: 2 weeks (1 week implementation, 1 week experimentation)

## Experiment 2: Distributional Conformity Deep Dive

### Thesis Statement
Random Probe method enforces distributional conformity through multiple measurable mechanisms: reduced maximum mean discrepancy, improved marginal distribution alignment, and better joint distribution structure.

### Testable Hypotheses
1. **H1**: RP-VAE will show 50% lower MMD between posterior samples and N(0,I) compared to standard VAE
2. **H2**: RP-VAE marginal distributions will have skewness < 0.5 and kurtosis between 2.5-3.5 (closer to Gaussian)
3. **H3**: RP-VAE will maintain lower correlation between latent dimensions (off-diagonal correlation matrix elements < 0.1)

### Experimental Design
- **Independent Variables**: Training method, RP frequency (every batch vs every 10 batches), number of random projections per batch (1, 3, 5)
- **Dependent Variables**:
  - MMD with RBF kernel between posterior samples and prior
  - Skewness and kurtosis of marginal distributions
  - Correlation matrix of latent dimensions
  - Earth Mover's Distance between distributions
- **Tasks**: Train on MNIST and CelebA, analyze 10,000 posterior samples per model

### Validity Threats & Mitigations
- **Statistical Power**: Multiple comparison corrections → Use Bonferroni adjustment
- **Measurement Error**: Single random projection bias → Use ensemble of 50 projections

### Resources & Timeline
- **Computational**: 60 GPU-hours
- **Timeline**: 3 weeks (1 week implementation, 2 weeks experimentation and analysis)

## Experiment 3: Computational Efficiency Analysis

### Thesis Statement
Random Probe method adds minimal computational overhead (<10% training time increase) while providing substantial distributional benefits.

### Testable Hypotheses
1. **H1**: RP-VAE training time will be <110% of standard VAE training time
2. **H2**: RP-VAE memory usage will be <105% of standard VAE memory usage
3. **H3**: RP loss computation will scale O(k) with latent dimension k, vs O(k²) for full covariance methods

### Experimental Design
- **Independent Variables**: Model size (latent dims: 16, 64, 256, 1024), batch size (32, 128, 512)
- **Dependent Variables**:
  - Wall-clock training time per epoch
  - Peak GPU memory usage
  - Forward pass time with/without RP loss
- **Benchmark**: Compare against β-VAE, WAE, and standard VAE
- **Platform**: Standardized on A100 GPUs for consistency

### Validity Threats & Mitigations
- **Implementation Bias**: Unoptimized RP code → Profile and optimize all methods equally
- **Hardware Variation**: GPU utilization differences → Use dedicated compute nodes

### Resources & Timeline
- **Computational**: 30 GPU-hours
- **Timeline**: 2 weeks

## Experiment 4: Scalability to High-Dimensional Latent Spaces

### Thesis Statement
Random Probe method maintains distributional enforcement effectiveness as latent dimensionality increases, unlike standard regularization methods that degrade.

### Testable Hypotheses
1. **H1**: RP-VAE distributional conformity (KS p-values) will remain stable across latent dimensions 16→1024
2. **H2**: Standard VAE conformity will degrade significantly (p-values dropping by >50%) with increased dimensionality
3. **H3**: RP-VAE will maintain generation quality (FID scores within 10% of optimal) across all dimensions

### Experimental Design
- **Independent Variables**: Latent dimensions (16, 32, 64, 128, 256, 512, 1024), training method
- **Dependent Variables**: KS test statistics, active units, FID scores, training stability (loss variance)
- **Dataset**: CIFAR-10 for controlled comparison
- **Analysis**: Polynomial regression to model conformity vs dimensionality relationship

### Validity Threats & Mitigations
- **Capacity Mismatch**: Different optimal architectures per dimension → Use architecture search for fairness
- **Optimization Difficulty**: High-dimensional training instability → Multiple learning rates and optimizers

### Resources & Timeline
- **Computational**: 80 GPU-hours
- **Timeline**: 4 weeks

## Experiment 5: Theoretical Validation - Connection to MMD

### Thesis Statement
Random Probe method approximates Maximum Mean Discrepancy minimization, providing theoretical foundation for its effectiveness.

### Testable Hypotheses
1. **H1**: Ensemble of RP projections will converge to full MMD computation (correlation > 0.9)
2. **H2**: Number of random projections needed for MMD approximation follows theoretical bounds O(log(d)/ε²)
3. **H3**: RP method will achieve similar distributional matching as explicit MMD-VAE with fewer computations

### Experimental Design
- **Independent Variables**: Number of random projections (1, 5, 10, 25, 50, 100), latent dimensions
- **Dependent Variables**: 
  - Correlation between RP ensemble and full MMD
  - Convergence rate to MMD approximation
  - Computational cost comparison
- **Theoretical Validation**: Compare empirical convergence to theoretical bounds
- **Baseline**: Direct MMD-VAE implementation

### Validity Threats & Mitigations
- **Approximation Quality**: Limited projection samples → Use bootstrap confidence intervals
- **Theoretical Assumptions**: Non-Gaussian data → Test on both synthetic Gaussian and real data

### Resources & Timeline
- **Computational**: 50 GPU-hours
- **Timeline**: 3 weeks

## Cross-Experiment Analysis Plan

### Statistical Framework
- **Power Analysis**: All experiments designed for 80% power at α=0.05
- **Multiple Comparisons**: Bonferroni correction for family-wise error control
- **Effect Sizes**: Cohen's d for continuous measures, Cramér's V for categorical
- **Confidence Intervals**: 95% CIs for all primary outcome measures

### Reproducibility Measures
- **Code**: All experiments in version-controlled repository with environment specifications
- **Data**: Standardized preprocessing pipelines, documented random seeds
- **Analysis**: Automated statistical analysis scripts with logging
- **Reporting**: Pre-registered analysis plan following CS197 evaluation standards

## Expected Timeline Summary
- **Week 1-2**: Experiment 1 (Core Validation)
- **Week 3-5**: Experiment 2 (Distributional Analysis) 
- **Week 6-7**: Experiment 3 (Efficiency Analysis)
- **Week 8-11**: Experiment 4 (Scalability)
- **Week 12-14**: Experiment 5 (Theoretical Validation)
- **Week 15-16**: Cross-experiment analysis and reporting

**Total Resources**: ~260 GPU-hours, 16 weeks

---
*Experiment ideas developed following CS197 research methodology*

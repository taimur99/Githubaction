# TITLE OF SEMINAR PROJECT

## Implementation of a Neural Network-Based Perceptual Loss for Audio

### Objective
Implement and demonstrate an audio perceptual loss function using neural network embeddings (e.g., from VGGish or OpenL3 embeddings).

### Tasks
- Set up embedding-based audio comparison using neural networks.
- Compare neural embeddings to traditional perceptual metrics.
- Analyze and visualize results for similarity assessment.

---

## Student Information
- **Name:** Taimur ul Islam  
- **Matriculation Number:** 64955  
- **Date:** 15.08.2025  
- **Email:** taimur-ul.islam@tu-ilmenau.de  

---

## Abstract
The goal of this project is to measure the difference between noisy audio signal and clean version, using both traditional mathematical metrics and modern perceptual methods. I first applied traditional approaches such as Mean Squared Error (MSE), which calculates the average squared difference between the signals and Signal-to-Noise Ratio (SNR), which measures how much of the signal is clean compared to noise. These methods are simple and widely used but they mainly look at sample by sample difference and not always match how humans actually hear the difference. It is useful for pre subjective testing like before use of human hearing.

To address this, we used VGGish, a deep learning model trained on large audio datasets to extract high-level audio features. We then measured the cosine distance between the clean and noisy audio embeddings as a form of perceptual loss. This allows the comparison to focus on sound characteristics that are more relevant to human perception such as tone, pitch, and timbre. This model behaves almost similar to humans hearing.

Conclusively, the results show that MSE and SNR give difference in numerical format, VGGish-based perceptual loss better reflects the perceived quality difference between clean and noisy audio. This comparison highlights the advantage of perceptual models for audio quality assessment especially in those cases where human perception and simple metrics do not fully agree.

---

## Introduction
This project estimates perceptual loss between paired clean and noisy audio. We first compute traditional signal metrics (MSE, SNR) and then use VGGish embeddings to measure semantic similarity (cosine distance), capturing perceptual differences beyond sample-wise errors.

---

## Literature Review
**Prior work:** Signal-space metrics (MSE, SNR) quantify distortion. Embedding-based methods (VGGish or OpenL3) better track human perception by comparing learned audio representations.

**Gap:** Not many projects directly compare traditional metrics like MSE and SNR with VGGish perceptual scores on the exact same clean–noisy audio pairs. Our work does this comparison, it shows that the MSE and SNR numerical value of the audios are different from what they actually sound like to a human listener.

---

## Methodology

### Algorithm
1. Load (clean, noisy), align, normalize.
2. Compute MSE, SNR.
3. Extract VGGish embeddings; compute cosine distance.

### Pseudocode

#### For MSE
- Load paired clean and noisy `.wav` files.
- If sample rates differ then resample noisy to match clean.
- Trim both to the same length.
- Mathematically `MSE = mean((clean − noisy)²)`.
- Save MSE score for (clean vs clean) and (clean vs noisy).
- Plot results.

#### For SNR
- Load paired files at fixed sample rate (16 kHz).
- `error = clean − noisy`
- `signal_power = mean(clean²)`
- `error_power = mean(error²)`
- `SNR = 10⋅log10(signal_power / error_power)`
- Save SNR score for both (clean vs clean) and (clean vs noisy).
- Plot results.

#### For VGGish Perceptual Loss
- Load VGGish model from TensorFlow Hub.
- Load paired audio files and resample to 16 kHz.
- Pad or trim each audio file to 1 second (16000 samples).
- Pass each audio to VGGish for embeddings extraction.
- Compute perceptual loss as cosine distance between embeddings.
- Plot bar chart of losses.
- Compare VGGish perceptual loss with MSE.

**Tools:** Python, NumPy/Pandas, Librosa, PyTorch/TF (VGGish)  
**Data:** Clean files = 94 `.wav`, Noisy files = 94 `.wav` (paired, resampled, trimmed, normalized).

---

## Evaluation of Metrics
**Strategy:** Report per-pair metrics; analyze correlations like VGGish distance vs SNR.  
**Metrics:** MSE, SNR, and VGGish cosine distance.

---

## Comparative Analysis
- **Benchmarking:** Baseline MSE and SNR.
- **Proposal:** VGGish distance better reflects perceptual quality when noise is spectro-temporally structured.
- MSE and SNR suffice for simple additive noise.

---

## Conclusion
This project compared traditional signal-based metrics (MSE and SNR) with a perceptual embedding-based metric (VGGish cosine distance) to check the similarity between clean and noisy audios. The results showed that MSE and SNR effectively quantify basic amplitude and power differences, but may not fully reflect how humans perceive audio quality, especially when noise changes spectral or temporal characteristics. VGGish-based perceptual loss captured these perceptual differences more effectively, providing a more human-aligned evaluation.

---

## Future Work
- Add more complex data or real-time cases.
- Integrate other embedding models (OpenL3, PANNs) for comparison.
- Add subjective listening tests for validation.
- Experiment with different noise types and intensities for robustness.
- Apply these metrics to evaluate audio denoising/enhancement algorithms.
- Add different algorithms for complex data to improve precision.

---

## References
1. Piczak, K. J. (2015). *ESC: Dataset for Environmental Sound Classification*. Proceedings of the 23rd ACM International Conference on Multimedia, pp. 1015–1018.
2. Hershey, S., et al. (2017). *CNN architectures for large-scale audio classification*. IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP), pp. 131–135.
3. Manocha, P., et al. (2020). *Content-based perceptual audio quality assessment*. IEEE International Conference on Acoustics, Speech and Signal Processing (ICASSP), pp. 911–915.
# Githubaction

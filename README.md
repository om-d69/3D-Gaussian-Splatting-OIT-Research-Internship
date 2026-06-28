# 3D-Gaussian-Splatting-OIT-Research-Internship
Research internship at Osaka Institute of Technology implementing an end-to-end 3D Gaussian Splatting pipeline for photorealistic scene reconstruction.
# 3D Gaussian Splatting Research Internship at Osaka Institute of Technology

## Overview

This repository documents my research internship at the **Visual Information Processing Laboratory, Osaka Institute of Technology (OIT), Japan**, under the supervision of **Prof. Norihiko Kawai**.

The primary objective of this internship was to understand, implement, debug, and successfully execute an end-to-end **3D Gaussian Splatting (3DGS)** pipeline for photorealistic scene reconstruction from real-world images.

Throughout the internship, I worked extensively on configuring the research environment, compiling multiple research codebases, resolving build issues, processing datasets using Structure-from-Motion (SfM), training Gaussian Splatting models, visualizing reconstructed scenes using the SIBR Viewer, and evaluating reconstruction quality through multiple training iterations.

This repository serves as a documentation archive of my internship journey and highlights the complete workflow, challenges encountered, solutions implemented, progress made, and final outcomes.

---

# Internship Details

**Intern:** Om Deshpande

**Institution:** Osaka Institute of Technology (OIT), Japan

**Laboratory:** Visual Information Processing Laboratory

**Supervisor:** Prof. Norihiko Kawai

**Research Area:**
- Computer Vision
- 3D Gaussian Splatting
- Novel View Synthesis
- Photorealistic Scene Reconstruction

---

# Project Objective

The objective of this internship was to successfully implement an end-to-end 3D Gaussian Splatting pipeline capable of reconstructing real-world scenes from photographs.

The internship focused on:

- Setting up the complete research environment on Windows.
- Building Gaussian Splatting from source.
- Understanding Structure-from-Motion using COLMAP.
- Validating the pipeline using publicly available datasets.
- Capturing custom DSLR datasets.
- Performing sparse reconstruction.
- Training Gaussian Splatting models.
- Rendering novel viewpoints.
- Running high-quality training on a higher VRAM workstation.
- Visualizing reconstructed scenes using the SIBR Viewer.

---

# Skills Acquired

During the internship I gained practical experience in:

- Computer Vision
- 3D Gaussian Splatting
- Novel View Synthesis
- Structure-from-Motion (SfM)
- COLMAP
- CUDA
- PyTorch
- CMake
- Visual Studio
- FFmpeg
- MeshLab
- SIBR Viewer
- Dataset Preparation
- Research Software Debugging
- Research Documentation

---

# Software and Tools

The following software and tools were used throughout the internship.

| Tool | Purpose |
|------|---------|
| Python | Training pipeline |
| PyTorch | Deep Learning framework |
| CUDA | GPU acceleration |
| Miniconda | Environment management |
| Visual Studio | C++ compilation |
| CMake | Build system |
| COLMAP | Structure-from-Motion |
| MeshLab | Point cloud visualization |
| FFmpeg | Video generation |
| SIBR Viewer | Interactive visualization |

---

# Hardware

Training and experimentation were performed using NVIDIA GPU workstations available within the laboratory.

Higher quality training was completed using a higher VRAM workstation available at OIT.

---

# Project Workflow

The internship followed the complete research pipeline below.

```

Capture Images

↓

COLMAP Feature Extraction

↓

Sparse Reconstruction

↓

Image Undistortion

↓

Gaussian Splatting Training

↓

Rendering

↓

SIBR Viewer Visualization

↓

Performance Evaluation

```

---

# Repository Structure

```

3DGS-Research-Internship-OIT

│

├── README.md

├── docs

│ ├── Progress_Report_1.pdf

│ ├── Progress_Report_2.pdf

│ └── Final_Progress_Report.pdf

│

├── videos

│ ├── 10000_iterations.mp4

│ ├── 15000_iterations.mp4

│ └── 30000_iterations.mp4

```

---

# Progress Timeline

The internship has been divided into three major milestones corresponding to the progress presentations delivered during the internship.

- Progress Report 1 – Environment setup, installation, debugging, pipeline validation.
- Progress Report 2 – Dataset collection, viewer compilation, higher iteration training.
- Final Progress Report – Completion of 30,000 iteration training, final evaluation, and internship learnings.

Each stage is described in detail below.

---

# Progress Report 1 – Initial Setup and Pipeline Validation

The first phase of the internship focused on understanding the research workflow and successfully configuring the complete software environment required for 3D Gaussian Splatting.

## Goals

- Setup the Gaussian Splatting pipeline.
- Validate training using sample datasets.
- Learn the overall reconstruction workflow.
- Prepare for custom dataset collection.

## Software Installation

The following software packages were installed and configured.

- Miniconda
- PyTorch
- CUDA Toolkit
- Visual Studio Build Tools
- CMake
- COLMAP
- MeshLab
- FFmpeg

The Gaussian Splatting research codebase was then compiled successfully on Windows.

---

# Major Challenges and Debugging

One of the most valuable aspects of this internship was learning how to debug and build research software from source. Unlike standard software development, research repositories often require significant troubleshooting before they become operational.

Throughout the internship, multiple issues were encountered and systematically resolved.

---

## 1. Conda Environment Issues

### Problem

The Conda environment was initially not recognized by the terminal, preventing package installation and execution of the training scripts.

### Solution

- Installed Miniconda correctly.
- Configured environment variables.
- Created dedicated Conda environments.
- Activated the correct environment before installing dependencies.

---

## 2. PyTorch and CUDA Extension Build Failures

### Problem

Several CUDA extensions required by Gaussian Splatting failed to compile due to missing dependencies and incorrect build environments.

Examples included:

- Missing PyTorch during isolated builds
- Missing CUDA headers
- Build dependency conflicts

### Solution

- Installed PyTorch before compiling extensions.
- Rebuilt CUDA modules.
- Verified CUDA compatibility with PyTorch.
- Reinstalled required packages inside the Conda environment.

---

## 3. Camera Model Issues

### Problem

Training failed because only the following camera models are supported by Gaussian Splatting:

- PINHOLE
- SIMPLE_PINHOLE

The original datasets contained unsupported camera parameters.

### Solution

The issue was resolved by:

- Running COLMAP Image Undistorter
- Creating an undistorted dataset
- Generating the required directory structure

```
dense/
├── images/
└── sparse/
    └── 0/
```

Training successfully resumed after converting the datasets.

---

## 4. COLMAP Command Compatibility

### Problem

Several online tutorials used deprecated COLMAP commands which were incompatible with the installed version.

Errors included:

- Unknown command-line options
- Invalid reconstruction commands
- Failed sparse reconstruction

### Solution

The reconstruction pipeline was updated according to the installed COLMAP version, allowing successful feature extraction, matching and sparse reconstruction.

---

## 5. Dataset Structure Problems

### Problem

Training repeatedly failed because the generated sparse reconstruction files were stored inside incorrect directories.

Gaussian Splatting expects a very specific folder structure.

### Solution

- Corrected directory hierarchy.
- Verified existence of all required `.bin` files.
- Copied sparse reconstruction into the correct folder.

---

## 6. SIBR Viewer Build Issues

### Problem

The SIBR Viewer initially failed to compile because of FFmpeg-related dependencies.

### Solution

- Disabled video-related components.
- Rebuilt SIBR without video support.
- Successfully compiled the interactive viewer.

The viewer was later used to inspect reconstructed Gaussian scenes.

---

# Initial Experiments

After successfully configuring the environment, experimentation began using publicly available datasets.

The objective was to verify that the entire pipeline functioned correctly before processing self-captured datasets.

---

## Mip-NeRF360 Dataset

The Mip-NeRF360 Treehill dataset was used as the initial benchmark.

The following experiments were completed:

- Pipeline validation
- Training for 3000 iterations
- Higher quality training for 5000 iterations
- Output verification

Successful reconstruction confirmed that the complete pipeline was functioning correctly.

---

# DSLR Dataset Collection

Once the pipeline had been validated, attention shifted towards collecting custom datasets.

Images were captured using a DSLR camera from multiple viewpoints.

Each scene was photographed from:

- Eye level
- Slightly above
- Slightly below

The captured images were then processed using COLMAP.

The following stages were completed successfully:

- Feature extraction
- Feature matching
- Sparse reconstruction
- Image undistortion

These processed datasets were subsequently used for Gaussian Splatting training.

---

# Initial Quality Evaluation

The first reconstruction attempts revealed several quality limitations.

Observed issues included:

- Blurred reconstructions
- Shallow depth of field
- Soft geometry
- Reduced scene sharpness

These observations highlighted the importance of capturing larger scenes with higher image overlap and improved focus.

As a result, new datasets were collected for subsequent experiments.

---

# Kyoto Dataset Collection

To improve reconstruction quality, multiple real-world datasets were collected during visits to Kyoto.

The datasets contained significantly more image overlap and larger environmental coverage than the initial DSLR experiments.

These datasets became the primary datasets used during the remainder of the internship.

They were processed using COLMAP and used for higher quality Gaussian Splatting training.

---

# Training Progress

The training process gradually progressed through multiple iteration counts to evaluate reconstruction quality.

---

## 7,000 Iterations

This stage served as the first successful validation of the Kyoto datasets.

Achievements:

- Successful Gaussian training
- Stable reconstruction
- Successful viewer visualization

---

## 10,000 Iterations

The next stage focused on improving geometry and scene consistency.

Observed improvements:

- Reduced artifacts
- Improved geometry
- Better camera consistency
- More stable reconstruction

### Demonstration Video

Replace the placeholder below with your uploaded video.

```text
/videos/10000_iterations.mp4
```

---

## 15,000 Iterations

The reconstruction quality continued to improve with higher training iterations.

Observed improvements:

- Sharper scene appearance
- Better surface representation
- Reduced floating artifacts
- Improved rendering stability

### Demonstration Video

```text
/videos/15000_iterations.mp4
```

---

# Progress Report 2

The second progress presentation summarized the successful completion of the complete Gaussian Splatting pipeline.

Major accomplishments included:

- Successful Windows setup
- Successful SIBR Viewer compilation
- Successful COLMAP reconstruction
- Successful training from approximately 7,000 to 15,000 iterations
- Successful visualization using the SIBR Viewer

The presentation also documented the primary challenges encountered during implementation and the corresponding debugging strategies used to resolve them.

---

# Next Research Objectives

Following the successful intermediate experiments, the next objectives were defined:

- Train at higher iteration counts
- Improve reconstruction smoothness
- Capture higher quality datasets
- Utilize a higher VRAM workstation
- Produce higher quality renderings
- Complete the final evaluation
- Present final results

These objectives formed the basis of the final phase of the internship.

---

# Final Phase – 30,000 Iteration Training

Following the successful intermediate experiments, the final phase of the internship focused on producing higher-quality reconstructions using increased training iterations and refined datasets.

Two real-world datasets collected during my visit to Kyoto were selected for the final experiments.

Training was successfully completed for **30,000 iterations** on both datasets using the laboratory's higher VRAM workstation.

The final reconstructions demonstrated significant improvements in scene quality, smoothness, and overall visual consistency compared to earlier experiments.

---

# Final Results

## Dataset 1

Training Iterations

**30,000**

### Results

- Successful Gaussian Splatting reconstruction
- Improved scene geometry
- Higher rendering quality
- Stable visualization using the SIBR Viewer

### Demonstration Video

> Replace the placeholder below with your uploaded video.

```text
/videos/30000_iterations_dataset1.mp4
```

---

## Dataset 2

Training Iterations

**30,000**

### Results

- Successful reconstruction
- Improved point distribution
- Better scene consistency
- Cleaner rendering

### Demonstration Video

```text
/videos/30000_iterations_dataset2.mp4
```

---

# Overall Progress Throughout the Internship

| Stage | Status |
|---------|--------|
| Environment Setup | ✅ Completed |
| Gaussian Splatting Installation | ✅ Completed |
| COLMAP Installation | ✅ Completed |
| CUDA Configuration | ✅ Completed |
| PyTorch Setup | ✅ Completed |
| Windows Build | ✅ Completed |
| Sample Dataset Validation | ✅ Completed |
| DSLR Dataset Capture | ✅ Completed |
| COLMAP Reconstruction | ✅ Completed |
| SIBR Viewer Compilation | ✅ Completed |
| 7,000 Iteration Training | ✅ Completed |
| 10,000 Iteration Training | ✅ Completed |
| 15,000 Iteration Training | ✅ Completed |
| 30,000 Iteration Training | ✅ Completed |
| Final Evaluation | ✅ Completed |

---

# Research Outcomes

During this internship, I successfully implemented an end-to-end pipeline for photorealistic scene reconstruction using 3D Gaussian Splatting.

The work involved:

- Configuring the complete software environment
- Building research repositories from source
- Processing datasets using COLMAP
- Debugging multiple software and dependency issues
- Training Gaussian Splatting models
- Rendering reconstructed scenes
- Visualizing outputs using the SIBR Viewer
- Evaluating reconstruction quality across multiple training iterations

This internship provided valuable practical experience in computer vision research, software debugging, and scientific experimentation.

---

# Key Learnings

Throughout the internship, I gained practical experience in:

- End-to-end 3D Gaussian Splatting workflows
- Structure-from-Motion (SfM)
- Camera calibration
- Dataset preparation
- Research software debugging
- CUDA-based applications
- CMake build systems
- Windows compilation workflows
- Scientific experimentation
- Performance evaluation
- Novel View Synthesis
- Real-world scene reconstruction
- Working in an international research laboratory

---

# Challenges Encountered

Some of the major technical challenges included:

- Conda environment configuration
- CUDA extension compilation
- PyTorch dependency conflicts
- COLMAP version compatibility
- Camera model incompatibilities
- Dataset directory structure issues
- Sparse reconstruction failures
- SIBR Viewer build errors
- FFmpeg dependency problems
- Reconstruction quality optimization

Resolving these challenges significantly improved my understanding of research software development and debugging.

---

# Progress Reports

The complete internship progress was documented through three formal presentations.

```
docs/

├── Progress_Report_1.pdf
├── Progress_Report_2.pdf
└── Final_Progress_Report.pdf
```

These reports document:

- Initial objectives
- Software installation
- Environment preparation
- Technical challenges
- Debugging process
- Dataset preparation
- Training progress
- Final evaluation
- Lessons learned

---

# Video Demonstrations

The repository also contains videos documenting the progression of the reconstruction quality throughout the internship, from intermediate training stages to the final 30,000-iteration results.

```
videos/

├── 10k_iterations_final.mp4
├── 15k_iterations_final.mp4
├── 30k_iterations_final.mp4
└── sibr_3Dgaussian 2026-01-20 19-40-48.mp4
```

### Video Descriptions

**10k_iterations_final.mp4**
- Demonstrates the reconstruction quality after **10,000 training iterations**.
- Shows the initial stable reconstruction with improved scene geometry and reduced artifacts.

**15k_iterations_final.mp4**
- Demonstrates the reconstruction after **15,000 training iterations**.
- Highlights improvements in scene consistency, surface quality, and rendering stability compared to the 10k iteration results.

**30k_iterations_final.mp4**
- Final high-quality reconstruction after **30,000 training iterations**.
- Represents the completed training on the Kyoto datasets with significantly improved visual quality and smoother rendering.

**sibr_3Dgaussian 2026-01-20 19-40-48.mp4**
- Interactive demonstration of the reconstructed scene using the **SIBR Gaussian Viewer**.
- Showcases real-time navigation around the trained Gaussian scene, allowing inspection of the reconstruction from different viewpoints.

---

# References

The following repositories and resources were extensively used throughout the internship.

## Official 3D Gaussian Splatting Repository

https://github.com/graphdeco-inria/gaussian-splatting

---

## Windows Installation Reference

https://github.com/jonstephens85/gaussian-splatting-Windows

---

## COLMAP

https://colmap.github.io/

https://github.com/colmap/colmap

---

## Mip-NeRF360 Dataset

https://jonbarron.info/mipnerf360/

---

## SIBR Viewers

https://sibr.gitlabpages.inria.fr/

---

## PyTorch

https://pytorch.org/

---

## CUDA Toolkit

https://developer.nvidia.com/cuda-toolkit

---

## CMake

https://cmake.org/

---

## FFmpeg

https://ffmpeg.org/

---

# Acknowledgements

I would like to express my sincere gratitude to **Prof. Norihiko Kawai** and the **Visual Information Processing Laboratory, Osaka Institute of Technology**, for providing me with the opportunity to work on cutting-edge research in Computer Vision and 3D Gaussian Splatting.

I am grateful to all the members of the laboratory for their continuous guidance, support, and encouragement throughout the internship.

Working in an international research environment allowed me to strengthen both my technical and problem-solving skills while gaining valuable exposure to real-world computer vision research.

The internship was an invaluable learning experience, and I sincerely appreciate everyone at Osaka Institute of Technology for making my stay both academically rewarding and personally memorable.

---

# License

This repository is intended for educational and portfolio purposes.

The original research code, datasets, and software belong to their respective authors.

Only documentation, demonstration videos, and progress reports related to my internship work are included in this repository.

---

## Contact

**Om Deshpande**

B.Tech. Cyber Physical Systems Engineering

Manipal Institute of Technology, India

GitHub: https://github.com/om-d69

LinkedIn: https://www.linkedin.com/in/om-deshpande-97b400251/

---



## A Review on Video Summarization  
by Preeti Meena, Himanshu Kumar, Sandeep Kumar Yadav

<img width="700" height="800" alt="image" src="https://github.com/user-attachments/assets/1df4677d-e153-4a49-82ea-12c28bce2a84" />

### Introduction

**Problem:** 2.5 quintillion bytes of data is created every day" and "720,000 hours of video are uploaded daily on YouTube.

**Video Summarization** - automatic process of summarizing the video while keeping the key element. Summary of the video can take two forms:
1. **Static video summary (Story Based)**: This is a collection of still images, or key frames, that represent the most important moments of the video
2. **Dynamic video summary (video-skim)**: This is a shorter video composed of sequence of key shots from the original

#### Current Limmitation in teh field
1. Most method work well only on one area (Domain Specific).

This paper talks about using different types of information beyond just video frames such as audio, video, and depth information. Summarization of video using multi-view and multi-modal data, different summary types, and different methodologies. 

### Research Questions
1. What methods are used for video summarization?
2. What characteristics are used to summarize data?
3. What types of multimedia ontent (e.g., 2D, 3D, multi-model) are used as input?
4. How well do existing appraches handle the challenges of different application domains and input data types? 

### Main Goals

1. To analyze how summarization methods and challenges change with advancements in visual data (e.g., from 2D to 3D).
2. To discuss the advantages of using different multimedia attributes (text, audio, depth).
3. To provide details of benchmark datasets.
4. To identify the limitations and gaps in current research.


### Video Summarization 

There are four primary types of video summarization:

1. Static Summary: A collection of key-frames arranges in chronological order, which are computationally efficient but lack audio clues and continuity.
2. Dynamic Summary: Obtained by joining key-shots, this type of summary can include both visual and corresponding audio content, making it more informative due to it's ability to utlize motion and audio.
3. Image summary: A Single static image created by combining various images from the video.
4. Text summary: A textual description of a video in a paragraph format, generated using NLP method. It requires less computational cost but lacks audio and visuals information.
   
<img width="700" height="800" alt="image" src="https://ars.els-cdn.com/content/image/1-s2.0-S0952197622006571-gr1_lrg.jpg" />

#### Four main stages involved in video summarization 

<img width="500" height="1000" alt="image" src = "https://ars.els-cdn.com/content/image/1-s2.0-S0952197622006571-gr2_lrg.jpg"/>

1. Scene Change Detection: This stage segments the input video into shots based on "event detection" or sharp changes. This is done by analyzing modalities like motion, shape, color, and texture.
2. Salient Feature Detection and Key-frame Selection (Section 2.2): Once the video is segmented into shots, this stage focuses on extracting more complex features than in the previous stage. Features are categorized into low-level (e.g., edge, intensity), mid-level (e.g., saliency, motion), and high-level (e.g., deep learning features, object detection). These features are used to select the best representative frames, known as key-frames, by evaluating intra-view (within a video) and inter-view (across different videos) correlations.
3. Summary Generation (Section 2.3): This is the final step where the selected key-frames are used to create the desired summary. The methods used for this can be classified into several categories, including shot-based, clustering-based, sparse dictionary, feature-based, and trajectory-based. These methodologies are often dependent on the application domain, such as surveillance, sports, or news.

<img width="500" height="1000" alt="image" src = "https://ars.els-cdn.com/content/image/1-s2.0-S0952197622006571-gr3_lrg.jpg"/>


### Classes of Video Summarization

<img width= "600" height = "600" src = "https://ars.els-cdn.com/content/image/1-s2.0-S0952197622006571-gr4_lrg.jpg"/>

#### Summarization based on number of views 

* Single-View Video Summarization(SVS): It is popular for creating summaries of videos captured from a single perspective. It rely on single view of a scene and it makes them less effective for scenes recorded by multiple cameras, such as those used in surveillance.
* Multi-View Video Summarization (MVS): MVS techniques address the limitations of SVS by summarizing videos captured from multiple cameras and angles. These methods are becoming more popular in applications where a scene is recorded by multiple cameras, providing a more comprehensive summary.

####  Data Dimension Based Summarization

Classifies summarization method based on the dimensions of the data used.

* 2D Summarization: This refers to summarization methods for standard 2D data like RGB images.
  
* 3D and Beyond Summarization: These methods are designed for data with three or more dimensions, such as meshes, skeleton points, or images with depth information (RGB+D).
      1. Spatial: This approach summarizes information across the spatial dimension, often using techniques like creating a panoramic image. For instance, a method for 3D video summarization might use rate-distortion optimization. Other techniques include using a graph-based approach to select key-frames based on the shortest path in a self-similarity map. Saliency-based algorithms are also adopted to preserve maximum information from the input.
      2. Temporal: Temporal summarization focuses on summarizing information along the temporal dimension. One method involves generating a single image summary with multiple foreground objects using depth information. Another approach uses CNNs to analyze players' movements in sports videos and classify segments as interesting or uninteresting.
      3. Spatio-temporal: This combines both spatial and temporal dimensions to summarize information, often by analyzing the motion trajectories of objects. For example, a method might estimate key-frames of a dance performance by exploiting the dancer's motion trajectories.

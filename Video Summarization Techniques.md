## A Review on Video Summarization  
by Preeti Meena, Himanshu Kumar, Sandeep Kumar Yadav

<img width="700" height="800" alt="image" src="https://github.com/user-attachments/assets/1df4677d-e153-4a49-82ea-12c28bce2a84" />

### Introduction

**Problem:** 2.5 quintillion bytes of data is created every day" and "720,000 hours of video are uploaded daily on YouTube.

**Video Summarization** - automatic process of summarizing the video while keeping the key element. Summary of the video can take two forms:
1. **Static video summary (Story Based)**: This is a collection of still images, or key frames, that represent the most important moments of the video
2. **Dynamic video summary (video-skim)**: This is a shorter video composed of sequence of key shots from the original

#### Current Limitation in the field
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

1. **Scene Change Detection**: This stage segments the input video into shots based on "event detection" or sharp changes. This is done by analyzing modalities like motion, shape, color, and texture.
2. **Salient Feature Detection and Key-frame Selection**: Once the video is segmented into shots, this stage focuses on extracting more complex features than in the previous stage. Features are categorized into low-level (e.g., edge, intensity), mid-level (e.g., saliency, motion), and high-level (e.g., deep learning features, object detection). These features are used to select the best representative frames, known as key-frames, by evaluating intra-view (within a video) and inter-view (across different videos) correlations.
3. **Summary Generation**: This is the final step where the selected key-frames are used to create the desired summary. The methods used for this can be classified into several categories, including shot-based, clustering-based, sparse dictionary, feature-based, and trajectory-based. These methodologies are often dependent on the application domain, such as surveillance, sports, or news.

<img width="500" height="1000" alt="image" src = "https://ars.els-cdn.com/content/image/1-s2.0-S0952197622006571-gr3_lrg.jpg"/>

**More details on Summary Generation methods:**

- **Shot-based methods** → Divide the video into shots, then extract key-frames from each segment.  
- **Clustering-based methods** → Group similar shots (K-means, spectral, DBSCAN).  
  - ⚠ Limitations: K-means often selects repeated segments in static scenes; spectral clustering may over-segment fast-changing scenes.  
- **Sparse dictionary learning** → Learns compact representations of data, useful for monitoring changes, but very time-consuming.  
- **Feature-based methods** → Use motion, objects, colors, or attention cues. Example: summarizing a sports video based on detected goals.  
- **Trajectory-based methods** → Track object paths across frames (e.g., players in sports or moving people in surveillance).  

*Note:* Each method performs differently depending on the domain (e.g., surveillance requires trajectory and motion cues, while news highlights rely more on event and attention cues).



### Classes of Video Summarization

<img width= "600" height = "600" src = "https://ars.els-cdn.com/content/image/1-s2.0-S0952197622006571-gr4_lrg.jpg"/>

#### Summarization based on number of views 

* Single-View Video Summarization(SVS): It is popular for creating summaries of videos captured from a single perspective. It rely on single view of a scene and it makes them less effective for scenes recorded by multiple cameras, such as those used in surveillance. Various SVS methods are mentioned in the table 5. 
* Multi-View Video Summarization (MVS): MVS techniques address the limitations of SVS by summarizing videos captured from multiple cameras and angles. These methods are becoming more popular in applications where a scene is recorded by multiple cameras, providing a more comprehensive summary.

####  Data Dimension Based Summarization

Classifies summarization method based on the dimensions of the data used.

* 2D Summarization: This refers to summarization methods for standard 2D data like RGB images.
  
* 3D and Beyond Summarization: These methods are designed for data with three or more dimensions, such as meshes, skeleton points, or images with depth information (RGB+D).
1. Spatial: This approach summarizes information across the spatial dimension, often using techniques like creating a panoramic image. For instance, a method for 3D video summarization might use rate-distortion optimization. Other techniques include using a graph-based approach to select key-frames based on the shortest path in a self-similarity map. Saliency-based algorithms are also adopted to preserve maximum information from the input.
2. Temporal: Temporal summarization focuses on summarizing information along the temporal dimension. One method involves generating a single image summary with multiple foreground objects using depth information. Another approach uses CNNs to analyze players' movements in sports videos and classify segments as interesting or uninteresting.
3. Spatio-temporal: This combines both spatial and temporal dimensions to summarize information, often by analyzing the motion trajectories of objects. For example, a method might estimate key-frames of a dance performance by exploiting the dancer's motion trajectories.


#### Multi-model data summarization

1. This method creates summaries by using a combination of different data types, or "modalities," such as audio, text, and visual information.
2. The main challenge in using multi-modal data is that the different types of information (images, audio, text) are often inconsistent and can't be simply combined.

This paper explains that a process called modality fusion is necessary to project data from different modalities into a common space so that their correlations can be analyzed. It covers three types of fusion:

1. Feature-level (Early Fusion): This involves combining the raw features from different modalities at an early stage. This is computationally efficient, but it can suffer from time synchronization issues if the data from different sources is not perfectly aligned.

2. Decision-level (Late Fusion): This involves analyzing each modality independently and then combining the results at the final decision-making stage. This is more scalable but may miss crucial correlations that exist at the feature level.

3. Intermediate-level Fusion: This is often done using deep neural networks, which can learn the complex relationships between modalities in a data-driven way, overcoming the limitations of early and late fusion.

Three categories of existing multi-model techniques based on modalities:
1. Audio-Visual Summarization - Combines audio and video signals
2. Textual-Visual Summarization - Combines visual data with text, such as video titles, captions, or transcripts.
3. Textual-Audio-Visual Summarization - Incorporates all three modalities.
   
   
#### Context Based Summarization


* Query-based: In these methods, the summary is generated according to a user's specific query or preference. This can be based on an image/clip query, where web images are used to detect representative frames. Alternatively, a text query-based method summarizes a video based on keywords provided by the user.

Saliency is defined as variance and contrast between a pixel and its surrounding locality. There can be multiple types of saliency such as perception, eye gaze-movement, facial expression, audio saliency, visual saliency, and textual saliency.

* Saliency/No-preference based: These techniques, such as those used for sports and surveillance videos, create a summary without requiring any user input or preference. The summaries are generated by automatically detecting important events or motions within the video.

### Application of Video Summarization

* Surveillance – Extract activities at specific locations (e.g., anomaly detection, suspicious behavior).
* Sports – Summarize multi-camera fast sports (e.g., goals, sixes, kick points).
* Movies/Serials – Capture important scenes, characters, emotions.
* News Highlights – Summarize anchors, debates, or interview segments.
* Rush/TV Videos – Remove duplicates and junk frames from long TV programs.
*Personal Videos – Handle unstructured videos with shaky/uncoordinated camera motion.


### Performance Analysis and Discussion

<img width= "600" height = "600" src = "https://ars.els-cdn.com/content/image/1-s2.0-S0952197622006571-gr7_lrg.jpg"/>

Paper talks about several metrics for assessing the effectiveness of summarization methods:

1. Precision: The accuracy of a method, calculated by comparing the number of correctly identified key-frames to the total number of key-frames extracted.

2. Recall: Measures the proportion of ground truth key-frames that were correctly identified by the method.

3. F-Score: The harmonic mean of precision and recall, providing a single, balanced score for the method's accuracy. The formula is F1=2 × (P+R/P×R).

4. Compression Ratio (CR): The ratio of the total number of frames in the original video to the number of key-frames in the summary. A higher CR indicates a more condensed summary (CR= N_original / N_summary).
   
5. Mean Opinion Score (MOS): A qualitative metric based on human perception. Viewers rate the quality and informativeness of a generated summary on a scale of 1 to 5.


#### Qualitative and Quantitative Comparison

Video from #15 TVSum dataset is used.

A qualitative analysis through visual summaries shows that methods like *AC-SUM-GAN* and *VASNet* produce more effective summaries by capturing the main event of the video while also including diverse visual content. In contrast, other methods often miss the main event or focus on less important graphics. 

The paper uses a table to compare F-score, Precision, Recall, CR, and MOS values. The results show that:

1. AC-SUM-GAN and VASNet achieve the highest F-scores, confirming their superior performance in accurately summarizing content.

2. SUM-GANdpp and Cycle-SUM have the highest Compression Ratios, meaning they produce the shortest summaries.

3. Cycle-SUM receives the highest MOS, suggesting that human viewers find its summaries to be the most diverse and informative, possibly because it includes frames that provide short textual descriptions.



### Conclusion 

The paper provides a comprehensive review of video summarization, covering its core concepts, methodologies, datasets, and performance analysis. The comparative analysis demonstrates the strengths and weaknesses of different state-of-the-art methods.


### Future Direction 

Further research is needed in (Table 15):

1. Clustering Algorithm does not take into account the temporal order.
2. Training of the model is computationally expensive.
3. It does not perform well for videos with high complexity.
4.  It fails in the case of videos that consist of frames with very slow motions and no scene-change.

# Video Summarization: Understanding User Attention 
**"A User Attention Model for Video Summarization"** 
by Yu-Fei Ma, Lie Lu, Hong-Jiang Zhang, and Mingjing Li from Microsoft Research Asia.

## Introduction

* This paper introduces a new way to automatically create summaries of videos. Instead of trying to understand every little detail (the "semantics") of a video, which is       very hard for computers,
* It focuses on **modeling what a person pays attention to** while watching a video. The idea is that if we can predict where a person's eyes and ears will focus, we can       pick out the most important parts for a summary.

Paper talks about A static abstract, also known as a static storyboard which is a collection of key-frames extracted from the original video sequence(Audio is lost) and a dynamic skimming which is collection of associated audio-video sub-clips(Takes long time to process)

## How does it work? (The "User Attention Model")

<img width="466" height="325" alt="image" src="https://github.com/user-attachments/assets/ecef4957-5c55-4cc0-8508-7ea71b86ac82" />


The core of this research is a framework that combines different types of "attention" to figure out what's interesting in a video:

1.  **Visual Attention:** What catches your eye?
    * **Motion Attention Model:** How much things are moving and where.
    * **Statice Attention Model:** Important details in static parts of the video.
    * **Faces Attention Model:** Faces are naturally very attention-grabbing.
    * **Camera Attention Model:** How the camera moves (zooming, panning) can highlight certain things.

2.  **Audio Attention:** What catches your ear?
    * **Audio Saliency Attention Model:** Sudden loud sounds or changes in sound levels.
    * **Speech and Music Attention Model:** Spoken words are usually very important for understanding content.
    * **Music:** Music sets the mood and can signal important moments.
  
3.  **Linguistic Attention:** -> Not discussed in the paper (but more like subtitles)
   
---------------------------------------

All these attentions are combined ---> Attention Curve for entire video ---> Create a graph/wave( smoothing and normalizing) ---> peaks are consider the most important ---> used for summary

--------------------------------------
## Math


w_v,  w_a,  w_l = weights for linear combination

M_v = normalized visual attention

M_a = normaized audio attention 

M_l = normalized linguistic attention


Attention Model = A(t) = w_v  *  M_v  +  w_a  *  M_a  +  w_l  *  M_l 

-------------------------------------

## Motion Attention Model
It uses "Motion Vector Fields" (MVF -> extracted from MPEGF-compressed video)(grid of vectors that describes how parts of images move between frames) -- (MPEG compressied video -- it only stores changes)

Each macroblock(e.g. 16 x 16 pixels) is analyzed using three inductors

1. Motion Intensity(I): Measures the energy of movement at a location
2. Spatial Coherence(Cs): Measures consistency of motion direction(movement of pixel e.g. macroblock) within the window
3. Temporal Coherence (Ct): Measures stability of motion direction over time
4. Output from all three channels (I, Cs, Ct) define the motion attention
   
   Motion Attention = B = I * Ct * (1- I * Cs)

--------------------------------------
A saliency map is a visual representation (usually grayscale or heatmap) that shows which parts of an image or video frame are most likely to attract human attention.
--------------------------------------   

## Static Attention Model
Captures which part of still frame are visually significant(e.g. static background even though there is no motion).  

Users a saliency-based model similar to Illi et al,

A saliency map is generated from each frame by there channels
1. Color
2. Contrasts
3. Intensity Contrasts

Static Attention Model formiuls = <img width="352" height="81" alt="image" src="https://github.com/user-attachments/assets/1e077f3c-9275-403e-ac21-b44ada8f9f52" />


## Face Attention Model
Captures Real time Face information---> face attention value at each frame to generate face attention curve

1. Number of faces
2. Face size and location
3. Face pose

   Face Attention Model = <img width="680" height="208" alt="image" src="https://github.com/user-attachments/assets/7e4c61e2-2728-4cdc-a8ce-dea833bbfb20" />


## Camera Attention Model
Captures the say camera moves like zoom, 

Camera motion is key behaviors:
1. Zooming/Dollying --> Attention increases with speed
2. Panning --> Horizontal fast panning reduces attention
3. After-movement effect --> Attention value increases for certain time


Attention factors caused by camers motion are quantified to the range of [0-2]
<1 = less important 
1 = Neutral
>1 = important
   <img width="738" height="660" alt="image" src="https://github.com/user-attachments/assets/6c12fbd4-ad61-48b3-9265-02c1d6fcc869" />

   
   
## Types of Summaries Created:

* **Static Storyboard:** A collection of important still images (key-frames) from the video.
* **Dynamic Skimming:** A shorter video made up of the most important short clips, keeping both video and audio.

## Conclusion

The researchers found that this "computational attention" approach is an effective way to summarize videos, offering a promising alternative to trying to fully understand the video's content semantically.

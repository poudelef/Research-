# Video Summarization: Understanding User Attention 
[**"A User Attention Model for Video Summarization"**](https://dl.acm.org/doi/abs/10.1145/641007.641116) by Yu-Fei Ma, Lie Lu, Hong-Jiang Zhang, and Mingjing Li from Microsoft Research Asia.

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

Attention Model = A(t) = w_v  *  M_v  +  w_a  *  M_a  +  w_l  *  M_l 

w_v,  w_a,  w_l = weights for linear combination

M_v = normalized visual attention

M_a = normaized audio attention 

M_l = normalized linguistic attention


-------------------------------------


--------------------------------------

## Vocabs 

A saliency map is a visual representation (usually grayscale or heatmap) that shows which parts of an image or video frame are most likely to attract human attention.

salient - most noticable or important 

--------------------------------------   

## VISUAL ATTENTION -> Motion Attention Model
It uses "Motion Vector Fields" (MVF -> extracted from MPEGF-compressed video)(grid of vectors that describes how parts of images move between frames) -- (MPEG compressied video -- it only stores changes)

Each macroblock(e.g. 16 x 16 pixels) is analyzed using three inductors

1. Motion Intensity(I): Measures the energy of movement at a location
2. Spatial Coherence(Cs): Measures consistency of motion direction(movement of pixel e.g. macroblock) within the window
3. Temporal Coherence (Ct): Measures stability of motion direction over time
4. Output from all three channels (I, Cs, Ct) define the motion attention
   
   Motion Attention = B = I * Ct * (1- I * Cs)


## VISUAL ATTENTION -> Static Attention Model
Captures which part of still frame are visually significant(e.g. static background even though there is no motion).  

Users a saliency-based model similar to Illi et al,

A saliency map is generated from each frame by there channels
1. Color
2. Contrasts
3. Intensity Contrasts

   Static Attention Model formiuls = <img width="352" height="81" alt="image" src="https://github.com/user-attachments/assets/1e077f3c-9275-403e-ac21-b44ada8f9f52" />


## VISUAL ATTENTION -> Face Attention Model
Captures Real time Face information---> face attention value at each frame to generate face attention curve

1. Number of faces
2. Face size and location
3. Face pose

   Face Attention Model = <img width="680" height="208" alt="image" src="https://github.com/user-attachments/assets/7e4c61e2-2728-4cdc-a8ce-dea833bbfb20" />


## VISUAL ATTENTION -> Camera Attention Model
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


## Audio Attention -> Audio Saliency Attention Model
Captures Loud or sudden changes

Audio Saliency Model = Mas = Ea * Ep

Ea = normalized loudness
Ep = normalized peak energy
   
## Audio Attention -> Speach and Music Attention Model 
Captures Speach and Music

1. Audio stream is segmented into sub-segments.
2. Set of features are computed from each sub-segment
3. features incude -> mel-frequency cepstral coefficients (MFCCs), short time energy (STE), zero crossing rates (ZCR), sub-band powers distribution, brightness, bandwidth, spectrum flux (SF), linear spectrum pair (LSP), divergence distance, band periodicity (BP), and the pitched ratio.
4. Support vector machine is finally used to classify each audio sub-segment into speech, music, silence, and others.

   <img width="274" height="98" alt="image" src="https://github.com/user-attachments/assets/bdff5db1-aa52-4460-b404-7bab61648556" />

M_speach and M_music denote speach attention and music attention. N denotes number of sub-segments for music and speech 


## Video Summarization Scheme

<img width="683" height="410" alt="image" src="https://github.com/user-attachments/assets/3889b69f-fe3f-4c83-961d-8aa812c3b258" />

1. User Attention Curve A(t) shows attention values per frame (combines visual, audio, and linguistic)
2. Then compute derivative A'(t), Zero crossing points (From + to - shows peak locations on A(t)
3. "Static Summary": Extract frame as keyfreame for each atention peak --> Rank all key framers by attention vlaue --> creates multi-scale summaries (e.g., top 5, 10 frames)
4. "Dynamic Summary": Once a skim ratio is given, skim segments are selected around each key-frame according to skim ratio within a shot.
5. To keep the audio consistent:
      1. Use adaptive sound level detection used to set threshold
      2. Identify pause and non pause frame using energy and ZCR information
      3. Result --> based on minimum pause length and minimum speech length
      4. Sectence boundry is determined my longer pauses duration

6. If segment < minimum length (L_min = 30); it creates annoying effects
7. Total skim length is contolled by skim ratio, One Skil per key frame
   

## Evaluations 

Three things were tested:
1. Single Key Frame Summary
2. Multi Key Frame Summary
3. Dynamic Summary (Skim Video)

Particapants : 20 volunteers (9 male, 11 female)

<img width="658" height="325" alt="image" src="https://github.com/user-attachments/assets/686669cb-396f-497e-a6a1-47d8a7e93214" />

## Static Summarization Evaluation 

A. Single Keyframe (per shot)

<img width="672" height="321" alt="image" src="https://github.com/user-attachments/assets/573cab0c-dd85-4a53-a7a8-871e23db18eb" />

B. Multiple Keyframe (per shot)

<img width="674" height="344" alt="image" src="https://github.com/user-attachments/assets/4ca4b5e4-5131-4f89-915a-7f4442d65370" />


## Dynamic Summarization Evaluation 

<img width="694" height="601" alt="image" src="https://github.com/user-attachments/assets/5a4d7b36-4b99-4e80-afb0-9554304b0b9b" />

30% skim was much better than 15%
       

## Conclusion

The paper finds that this "computational attention" approach is an effective way to summarize videos, compared to understanding the full video's content. A generic and entendable video attention model is created and can be used for other applications. I also talks about further study is needed in fusion scheme.  

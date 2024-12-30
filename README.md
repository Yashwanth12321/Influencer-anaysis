
# Influencer Selection 
                    
# Task
Building a system that can:
- Identify unique influencers appearing across these videos
- Calculate their average performance for each influencer 
to understand influencers consistently drive better engagement

## Assumptions
- Influencers are restricted to either creating videos with faces or without faces but not both.
- Assumption of **all the videos in the dataset** are relevant i.e., videos that are duplicated are considered to be released by same Influencers (reuploads maybe) since other people cannot release the same video due to copyright reasons maybe.
- since videos are characterised whether there is a face or not, for the **videos with faces**, the face that appears in the video(the face that gets captured in frames maximum number of times) is the face of that influencer given that person appears in their videos not the side characters.
- **for faceless videos**, i have classified them to their Influencers instead of considering them as noise(if it is noise, we simply neglect this part, since we have segregated face and facless videos). The classification is based on the Assumption that videos released by the same influencer has **same outro frame** i.e., maps the anoymous influencer based on the outro frame (lets say 10th frame before ending).
## Approach (On a very high level)


- The goal is to first categorise faceless videos and videos with faces.
    
- To categorise video with faces:
    
    => extract frames from videos using opencv (we do that for all the videos in data)
    => now for the frames for each video we use media pipe to detect if there is face or not
    => for that face we extract its embedding vector using Deepface
    => Goal here is for a video we have to capture most frequent face, to achieve that we have to set a counter for each face (embeddings mapped to an id) if we encounter a face , we capture its embedding (some thresshold for comparing the faces.) and increment its mapped id counter. 
    => now we map videos with the same face(embedding) to their videos, that it. and for their scores, i kept it simple average(mean).

    => for faceless videos, simply mapped the outro frame with the videos and categorised the same ones, and as for scores simply mean.
## Results

=> Videos with faces
![image](https://github.com/user-attachments/assets/8f8340d5-7e24-408c-b2cc-54c8c408b406)

=> Videos without faces
![image](https://github.com/user-attachments/assets/eb8892ea-3cd9-4732-b7e6-f062e73674c0)


# Final statements
- Ofcourse this is not even close to a real world solution, as i can spot more edgecases or errors like the algorithm registering faces from a picture frame and labelling as an influencer, and sometimes classifying same person's two different facial expressions as different influencer.
- This was my attempt in 1 + 1/2 days timeframe.



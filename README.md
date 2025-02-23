# A Content-Driven Micro-Video Recommendation Dataset at Scale

# Dataset

Dataset downloader (for Windows): https://github.com/microlens2023/microlens-dataset/blob/master/Downloader/microlens_downloader.exe

Dataset downloader (for Linux): https://github.com/microlens2023/microlens-dataset/blob/master/Downloader/microlens_downloader

For review purposes, we are temporarily releasing a portion of our Microlens dataset.

Through the download tools, you can download 500 randomly sampled videos from the Microlens dataset, including cover images, full-length videos (with audios), and textual captions (including tags) for all 100 videos.

Additionally, we also provide the interaction file for MicroLens-100k (namely "MicroLens-100k_pairs.csv"), in which the three columns are "userID", "videoID" and "timestamp".

For various types of modal data and the interaction pairs of MicroLens-100K and MicroLens, we will release all of them once the paper is accepted.

# Code

We have released the codes for all algorithms, including VideoRec (which implements all 15 video models in this project), IDRec, and VIDRec. For more details, please refer to the following paths: "Code/VideoRec", "Code/IDRec", and "Code/VIDRec". Each folder contains multiple subfolders, with each subfolder representing the code for a baseline.

## Special instructions on VideoRec

In VideoRec, if you wish to switch to a different training mode, please execute the following Python scripts: 'run_id.py', 'run_text.py', 'run_image.py', and 'run_video.py'. For testing, you can use 'run_id_test.py', 'run_text_test.py', 'run_image_test.py', and 'run_video_test.py', respectively. Please see the path "Code/VideoRec/SASRec" for more details.

Before running the training script, please make sure to modify the dataset path, item encoder, pretrained model path, GPU devices, GPU numbers, and hyperparameters. Additionally, remember to specify the best validation checkpoint (e.g., 'epoch-30.pt') before running the test script.

Note that you will need to prepare an LMDB file and specify it in the scripts before running image-based or video-based VideoRec. To assist with this, we have provided a Python script for LMDB generation. Please refer to 'Data Generation/generate_cover_frames_lmdb.py' for more details.

## Special instructions on IDRec and VIDRec

In IDRec, see `IDRec\process_data.ipynb` to process the interaction data.  Execute the following Python scripts: 'main.py'  under each folder to run the corresponding baselines. The data path, model parameters can be modified by changing the `yaml` file under each folder. 

## Environments
```
python==3.8.12
Pytorch==1.8.0
cudatoolkit==11.1
torchvision==0.9.0
transformers==4.23.1
```

# Additional Materials and Results

## Additional Discussion on Feedback Type

Our dataset mainly provides user comments as positive interactions, while other forms of user feedback, such as clicks, watching time, and exposure data, are not included. This limitation arises from the fact that click, watch, and exposure behaviors are considered confidential business data, which can only be accessed through the company's servers. Collecting and providing both raw videos and privacy-sensitive feedback data is practically unfeasible due to privacy concerns and the data protection policy from our local government. As far as we know, there are currently no recommendation datasets available that offer both types of data on a large scale. Moreover, the inclusion of exposure data would enable the inference of various business metrics, which is strictly prohibited. Given that Tenrec and KuaiRec have already provided various user feedback (but they do not include raw video features), we aim to provide the raw video data as the core contribution. In addition, we want to emphasize that the commenting behavior of users on short videos differs from that of e-commerce platforms. Negative comments often target specific events within the short video rather than the item itself. Therefore, we can safely assume that users have engaged with the video through viewing or clicking, as long as we observe their comments. Here, we do not consider extremely special cases.

While comments are widely used as positive interaction signals in many popular recommendation datasets like Amazon, Yelp, etc., there are still some limitations. To be specific, many users may have clicked on an item but did not leave a comment, resulting in the loss of positive feedback on user behavior. However, this is also the reason why recommendation systems are often called one-class collaborative filtering (OCCF), because even if one provides click or viewing behaviors, there are still many items that users like, but have no positive interaction due to lack of exposure. Therefore, from this perspective, although comment data is not perfect, it is still a reliable form of important implicit feedback. We believe that each dataset has its own limitations and that one paper cannot address them all. We look forward to researchers in the community contributing more diverse datasets to further enhance the field.

## Measures to Address Potential Ethical Issues

We have taken strict measures to address all potential ethical issues.

**No Collection of Personal Data or Data from Human Subjects.** Our dataset does not involve the collection or use of any personally identifiable information or data related to human identities. We strictly adhere to privacy protection regulations and do not collect users' personal information such as browsing, favorites, or watch duration. Instead, we only gather publicly available user comments on videos. Furthermore, we have assigned anonymous IDs to both users (commenters) and items, making it impossible to identify the individuals from the commenting behaviors. For example, by an instance like <UserID=1, ItemID=1, ItemID=2, ItemID=3>, we can observe the public behavior of the user with ID=1 (commenting on three videos), but we can not recognize this user's actual identity.

**Protection Measures against Personally Identifiable Information or Inferred Data.** In addition to anonymizing user and item IDs, we have implemented further safeguards to ensure that ``personally identifiable information" or ``data that could infer individuals without their consent" is not included in our dataset. Specifically, we have taken the following measures:
-  We do not disclose the original video links. All videos in our dataset can only be accessed through a provided downloader, which does not expose any URLs. We have also implemented robust security measures to prevent attacks and code decompilation during the download process.
-  By not providing the original links and instead sharing the raw videos without creator watermarks and releasing translated video titles, we ensure that the original video pages cannot be found through the Internet. This protects the anonymity of creators while preventing the reverse retrieval of user information through the commenting page (By searching commenters from the commenting page, people can locate a user by the videos s/he interacted with).

**Offensive Content Filtering.** All videos we collect have already retained a period of time on a public platform, where they have already undergone platform reviews and user scrutiny before collection. Additionally, we have organized a team of volunteers who diligently reviewed all 91,402 videos in the dataset to ensure the absence of offensive content.

**Protection of Individual and Platform Interests.** We provided a license that requires our dataset solely for academic purposes, and have established legally binding usage agreements. These measures ensure that the release of this dataset does not infringe upon the copyrights or commercial interests of video creators or the platform.

**Bias Mitigation and Diversity Assurance.** Our data collection process does not target specific demographic groups. Our dataset represents the diversity of videos and commenters, which ensures inclusivity and fairness in our research.

**Compliance with Ethical Oversight.** We have submitted the dataset, collection process, and adopted security measures to the Institutional Ethics Review Committee for review and we have obtained the necessary approval, which guaranteed that our dataset follows rigorous ethical scrutiny.

**Guarantee of Dataset Integrity.** We take measures to automatically place potentially expired or unavailable videos in a backup directory during the download process to ensure permanent accessibility. Note we only provide this for MicroLens-1M and MicroLens-100K rather than the complete MicroLens dataset, which is too large and is not claimed as a contribution in our paper.

**Guarantee of Creator Rights.** In addition to protecting the information of video creators and ensuring their interests are not compromised, we have implemented other measures to guarantee their legal rights. We maintain open and long-lasting contact channels (e.g., a permanent email address) to address any requests from creators or platforms to remove videos and associated instances. We will promptly take action to delete relevant content and update announcements regarding dataset iterations.

**Consent to Collect Data.** What we collected are publicly available user comments and videos, and we have implemented a series of protective measures on the collected data. Furthermore, we take action to ensure that our dataset is used solely for research purposes. Generally, obtaining consent is not necessary for building such recommendation datasets, which is accepted practice in previous academic literature. However, even in light of this, we have taken comprehensive considerations and obtained permission from the Institutional Ethics Review Committee.

<!--
## Recommendation with Only Cover Images

**Table 1: Recommendation accuracy using cover images to represent videos, with three SOTA image encoders, i.e., ResNet, Swin Transformer and MAE.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/only-images.png"/></div>

## Warm Item Recommendation

**Table 2: Comparison of VideoRec and IDRec in regular and warm settings using SASRec as the backbone. "Warm-20" denotes that items with less than 20 interactions were removed from the original MicroLens-100K.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/warm-item.png"/></div>

The results from Table 2 showcase that VideoRec significantly outperforms IDRec in both regular and warm-up scenarios. Even in the warm-up (200) setting, the difference between the two methods remains pronounced. It is a surprising finding since IDRec is known for its ability to model popular items, and the experiments conducted in earlier work suggest that IDRec should have a slight advantage over modality-based methods in warmer settings. However, it is important to note that the modality content used in that work are covers or titles, instead of video media. The comparison verifies that compared to images or text, video content indeed provides richer item representation information and thus amplifies the advantages of modality-based methods, highlighting the merits of MicroLens. 
-->

## Recommendation in Cold-start Scenarios

**Figure 1: Results in different cold-start scenarios, with the y-axis representing the relative improvement of HR@10, calculated as the ratio of VideoRec to IDRec. The x-axis represents item groups divided by popularity level, the larger number indicates that items in the group are more popular.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/cold-start.png" width="80%"/></div>

The results presented in Figure 1 demonstrate a significant disparity between VideoRec and IDRec in cold-start scenarios. IDRec relies on interactions between users and items to learn their representations, while VideoRec can model items based on the content of videos themselves. This enables VideoRec to provide more pronounced recommendation results even in situations with minimal interactions compared to IDRec. Moreover, as the cold-start problem becomes more severe, the advantage of VideoRec over IDRec becomes increasingly amplified. For instance, as the popularity becomes smaller, the relative improvement of VideoRec to IDRec is larger, especially when the popularity varies from 2 to 1.

## Related Datasets

**Table 1: Dataset comparison. "p-Image" refers to pre-extracted visual features from pre-trained visual encoders (such as ResNet), while "r-Image" refers to images with raw image pixels. "Audio" and "Video" refer to the original full-length audio and video content. Note that MicroLens is the first recommendation dataset that contains raw micro-video data.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/dataset-comparison.png"/></div>

## Video Model Details in Video Understanding and Recommendation

**Table 2: Performance of VideoRec with 15 video encoders. "Pretrain Settings" are the adopted frame length and sample rate from the pre-trained checkpoint. ACC@5 is the accuracy of the video classification task.**

<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/video-details.png"/></div>

## Hyper-parameter Settings for Baselines

**Table 3: Hyper-parameters settings for baselines. The "finetuning rate" denotes the learning rate applied to the video encoder during the finetuning process.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/baseline-settings.png"/></div>

## Details of the Applied Image Encoders

**Table 4: Network architecture, parameter size, and download URL of the vision encoders for image baselines. L: number of Transformer blocks, H: number of multi-head attention, C: channel number of the hidden layers in the first stage, B: number of layers in each block.**

<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/image-details.png"/></div>

## Recommendation with Side Features

We investigate the impact of other features on recommendation performance using the MicroLens-100K dataset. We introduce two types of side features: item popularity level (Pop) and tag categories (Tag). For popularity features, we divide the item popularity into 10 uniform bins. The first bin represents the top 10% of popular items, while the last bin represents the bottom 10%. We assign a Pop ID to each item according to its popularity level. Regarding the tag features, we also handle them as categorical features with a category of 15,580. We conducted experiments on SASRec_{ID} (ID) with different feature combinations: SASRec_ID, SASRec_{ID+Pop}, SASRec_{ID+Tag}, and SASRec_{ID+Pop+Tag}. The "+" symbol denotes feature combinations achieved by summing and averaging them. We report the results in Table 5.

We found that incorporating item popularity level and tag categories as side features did not clearly improve the algorithm's performance. One possible reason is that in typical recommendation scenarios, item ID embeddings have already been extensively trained, implicitly learning latent factors including similarity and popularity. For instance, we observed that many videos recommended in the top-10 recommendation list share similar categories and have relatively high popularity, indicating that ID-based methods can already capture popularity and category information. In such scenarios, incorporating many unimportant features  may have a negative impact on overall performance. It is worth noting that in the very cold-start setting, the item ID feature is very weak and adding other features is necessary for better performance.

**Table 5: Recommendation results with side features on MicroLens-100K.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/side-features.png"/></div>

## Baseline Evaluation and Warm Item Recommendation on MicroLens-1M

**Table 6: Benchmark results on MicroLens-1M.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/benchmark-1m.png"/></div>

**Table 7: Comparison of VideoRec and IDRec in regular and warm-start settings using SASRec as the user backbone. Warm-20 denotes that items with less than 20 interactions were removed from the original MicroLens-1M.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/warm-1m.png"/></div>

## Comparison between Textual Features and Video Content

We used [BERT](https://huggingface.co/prajjwal1/bert-small) as the text encoder and SlowFast16x8-r101 as the video encoder and perform end-to-end training. We fixed the learning rate of recommender model as 1e-4, and searched for the optimal learning rates for the text encoder and video encoder from {1e-3, 1e-4}. The comparison results are reported in Table 8. Our results demonstrate that using only text features yields similar performance to the itemID feature. By analyzing the data, we have observed that some short videos have only a few words in their descriptions, which may contribute to the performance not being particularly competitive. On the other hand, the amount of information contained in the original videos far exceeds that of the video titles. Therefore, we believe that in the future, utilizing more powerful video understanding techniques can lead to better recommendation results.

**Table 8: Comparison results of ID, textual features and video content on MicroLens-100K.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/text-video.png"/></div>

## Computation Cost

**Table 9. The computation cost information for IDRec and VideoRec on the MicroLens-100K dataset, where SASRec is taken as the recommender backbone and top1-block fine-tuning strategy used in this paper is applied for VideoRec. #Param: the size of tunable parameters, FLOPs: computational complexity, Time/E: averaged training time for one epoch, BE: the best epoch in terms of optimal validation results, MU: GPU memory usage, and the GPU configuration used, e.g., ’A40-48G(4)’ denotes that we used 4 A40s with 48G memory. Note that although VideoRec by E2E learning is more expensive than IDRec, it also shows improved performance. The main finding is that there is still much room for improvement in recommendation models by properly leveraging video features. We believe that more effective and efficient VideoRec models, even beyond the VideoRec paradigm, can be developed in the future inspired by MicroLens.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/computation-cost.png"/></div>

## Multi-Modal Recommendation

**Table 10. Recommendation performance of multimodal methods with video features. "V" indicates video features, "MM" indicates multimodal features with video features included.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/multimodal-recommendation.png"/></div>

[1] Zhou, Xin, and Zhiqi Shen. "A tale of two graphs: Freezing and denoising graph structures for multimodal recommendation." Proceedings of the 31st ACM International Conference on Multimedia. 2023.

[2] Yu, Penghang, et al. "Multi-view graph convolutional network for multimedia recommendation." Proceedings of the 31st ACM International Conference on Multimedia. 2023.

[3] Wei, Yinwei, et al. "MMGCN: Multi-modal graph convolution network for personalized recommendation of micro-video." Proceedings of the 27th ACM international conference on multimedia. 2019.

[4] Wei, Yinwei, et al. "Graph-refined convolutional network for multimedia recommendation with implicit feedback." Proceedings of the 28th ACM international conference on multimedia. 2020.

## Transfer Learning

**Table 11. Transferable video recommendation utilizing three types of video encoders. The source datasets comprise MicroLens-100K and MicroLens-1M, while the target dataset is Bili-20K. "PT" stands for pre-trained, indicating that the model has been initially trained on the source dataset and subsequently finetuned on the target dataset.**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/transfer-learning.png"/></div>

## Dataset Analysis of MicroLens-1M

**Figure 2: The statistical information of MIcroLens-1M, i.e., item popularity, user activity and video duration**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/1m-sts.png"/></div>

## Recommendation Scenario of Collected Platform

Figure 3 below illustrates the recommendation scenario of the micro-video platform from which our MicroLens collected data. In this example, a user is recommended a video about trucks. After watching a short segment, the user swipes up to the next video. All these videos allow user engagement through buttons for liking, sharing, and commenting, which are visible on the right side of the videos. On this platform, there are multiple ways to define positive and negative examples. For instance, the duration of video views, presence of likes, comments, or shares can all be considered as different levels of user feedback.  However, among these behaviors, only comment behaviors are public without any access restrictions. Also,  note that the videos and comments are publicly accessible both on the mobile app and the web. In the mobile app, users navigate to the next video by swiping gestures, while on the web, users use mouse scrolling to move to the next video. The web scene is displayed in the same way as the mobile app scene.

In the micro-video application, users are typically presented with a continuous stream of videos. The recommendation process continues uninterrupted through the user swiping up or mouse scrolling, ensuring a seamless flow of video recommendations.

**Figure 3: An illustration of the recommendation scenario in MicroLens. Videos a, b, and c are displayed in landscape format, while videos d, e, and f are displayed in portrait format. Please note that the format of the next video is random and can be either landscape or portrait. The English translation is provided for all video titles**
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/Results/recommendation-scenario.png"/></div>

## Permission for MicroLens Dataset

To ensure anonymous peer review, we have masked the author and affiliation information.
<div align=center><img src="https://github.com/microlens2023/microlens-dataset/blob/master/dataset-permission-mosaic.png"/></div>

### Market Volatility Modelling using Specialized RoBERTa Clusters in Sentiment Analysis of FOMC Texts

#### Overview

This project presents a novel architecture leveraging clustered RoBERTa Large LLMs for efficient, low-latency volatility modelling using sentiment analysis of financial texts from Federal Open Market Committee (FOMC) communications. Our design als focuses on addressing the growing "arms race" in the NLP field towards larger, less cost-effective models. 

#### Problem Statement

The NLP field currently faces a split between open and closed LLMs. Open models that have sufficient associated documentation published publicly offer reproducibility, community support, and fewer regulatory issues concerning data sharing. Closed commercial models, while not reasonably reproducible, offer state-of-the-art performance using APIs with great documentation and support. This approach aims to exploit a market niche for applications like sentiment analysis where smaller, fine-tuned models can perform comparably.

#### Purpose

This project serves a dual purpose:
1. To inform the general public about the inefficiencies in current NLP model development.
2. To demonstrate to students, academics, and researchers a more targeted approach to solving NLP problems, focusing on efficiency and specialization.

#### Proposed Solution
![](https://github.com/yahyahas3an/ClusteredLLMsVolatilityModelling/blob/main/IMG_2566.jpg?raw=true)
Using a dataset of all FOMC correspondences from 2000 to 2024, we employ a cost-effective, granular approach to model training:
1. **Data Labeling**: Instead of Manual labeling by experts, our approach leveraged the Gemini 1.5-flash model using API calls for zero-shot sentiment classification of all sentences from the FOMC correspondences. The first design choice of using a LLM for sentiment classification instead of expert labelling addresses an important inefficiency with LLM training, and in this case, fine-tuning. While finding a customized dataset and comes at the cost of human effort to develop web-scraping algorithms or label data, it does yield a more accurate dataset that is essential for performance. Our second design choice addresses that. By defining the sentiment classification's granularity to sentences, this decreases the error rate significantly and provides sufficient confidence that any errors by Gemini are averaged out. Additionally, this design produces a framework that allows for further scalability. 
2. **Specialized Fine-Tuning**: We fine-tune three RoBERTa Large models for specific sentiments — "volatility," "market confidence," and "hawkishness" — each crucial to understanding FOMC's implications on market stability and economic growth. This can be expanded to include more sentiments easily. To add more sentiments, Gemini can be used again to create a new dataset used to finetune an additional RoBERTa Large model. A flexibility provided by this model is the lack of a need for a "do it all model." Commercial LLMs incorporate vast and varied data sets with extensive generative capabilities. On the other hand, the RoBERTa Large model offers a balance between complexity and performance. Our use of RoBERTa Large is limited to classification, prioritizing the  balance between post-fine-tuning performance and operational speed. Here, the lower paramter size leads to quicker fine-tuning and ensures that the tuning has a more substantial impact on the model's effectiveness compared to larger models.



4. **Modelling Volatility** The volatility of the market is modeled using the following mathematical equation: Hawkishness Measure = (Number of Hawkish Sentences - Number of Dovish Sentences) / Total Number of Sentences. After fine-tuning, the LLM cluster is deployed to classify all sentences from FOMC correspondences between 2000 and 2022 using this measure. This approach effectively quantifies the balance between "dovish" and "hawkish" sentiments. Similarly, a measure for volatility and market confidence is employed, which has proven effective as a multiplier to the hawkishness measure. The results are displayed below, demonstrating the utility of these measures in analyzing market sentiments based on FOMC communications.
![](https://github.com/yahyahas3an/ClusteredLLMsVolatilityModelling/blob/main/IMG_2568.jpg?raw=true)

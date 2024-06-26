# Towards Open-World Recommendation with Knowledge Augmentation from Large Language Models

## Requirements
```
python>=3.8
transformers>=4.22.2
numpy
pytorch>=1.10.0
scikit-learn
```

## Setup

1. Download dataset
   
   Take Amazon-Books for example, download the dataset to folder `data/amz/raw_data/`
2. Preprocessing: in folder `preprocess`
   1. run `python preprocess_amz.py`.
   2. run `generate_data_and_prompt.py` to generate data for CTR and re-ranking task, as well as prompt for LLM.
   
3. Knowledge generation

   You can use any generative LLM and prompts we obtained before to generate knowledge. Here, we don't release the code for knowledge generation but give the knowledge generated by LLM in folder `data/knowledge`.
   1. `data/amz/item.klg`: factual knowledge about books in Amazon-Books. Note that some books are filtered.
   2. `data/amz/user.klg`: preference knowledge about users in Amazon-Books. Note that some users are filtered.
   3. `data/ml-1m/item.klg`: factual knowledge about movies in MovieLens-1M.
   4. `data/ml-1m/user.klg`: preference knowledge about users in MovieLens-1M. 
   
   Above files are all saved in `json`, with each key as the raw id of user/item in the original dataset and each value as the corresponding prompt and knowledge generated by LLM.
   
   To avoid information leakage, we also provide `end_index.json`, where each user has an index n. We sort the interaction sequence of each user by time (in ascending order) and give each interaction an index. Then the first n interactions are used for prompting LLM to get preference knowledge. In our implementation, the first n interaction will not appear in the test set to prevent information leakage.

4. Knowledge encoding: in folder `knowledge_encoding`

   Run `python lm_encoding.py`
5. RS: in folder `RS`

   Run `python run_ctr.py` for ctr task

   Run `python run_rerank.py` for reranking task


If you find this work useful, please cite our paper and give us a shining star 🌟

```
@article{xi2023openworld,
  title={Towards Open-World Recommendation with Knowledge Augmentation from Large Language Models},
  author={Yunjia Xi and Weiwen Liu and Jianghao Lin and Jieming Zhu and Bo Chen and Ruiming Tang and Weinan Zhang and Rui Zhang and Yong Yu},
  journal={arXiv preprint arXiv:2306.10933},
  year={2023}
}
```

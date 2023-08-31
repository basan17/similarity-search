# Product mathiching based on ML algorithms

The project is done by Basang Basangov.
Telegram: [basan4ik](https://t.me/basan4ik)

## Project Description

Data matching is the workflow process of comparing different data values in structured or unstructured format based on similarity or an underlying entity [[1]](https://www.width.ai/post/data-matching-software#:~:text=How%20you%20can%20use%20machine,similarity%20or%20an%20underlying%20entity.). This notebook provides a workflow of how this type of task can be solved using two-staged process: first, FAISS similarity search is used to get 100-200 the most similar products from a database (that could petentially consist of billions of items), then among those 100-200 products get 5 that are even more similar using supervised ML algoritm, which in our case would be LightGBM classification algorithm. The final evaluation metric is accuracy@5.

There are 4 files:
- 'base.csv' is a dataset of anonymized set of products. Each product is presented with a unique id (0-base, 1-base, etc.) and vectors of the shape 1 x 72;
- train.csv is a training dataset. Each row has an id (0-query, 1-query, etc.), a vector (1x72), and id from 'base';
- validation.csv is a dataset of vectors that we need to find the most similar vectors from 'base'.
- validation_answer.csv is a dataset with the right answers to the previous dataset.

This is a project from [Yandex Practicum Masterskaya](https://practicum.yandex.ru/masterskaya/).

## Conslusion

Due to restrictions of RAM capacity on my laptop, the decision was made to use only first 10_000 rows of train and validation datasets. Nevertheless, two-staged similarity search (FAISS + LightGBM classifier) showed that the approach is working. 

There are some quirks that could be changed:
- I used FAISS IndexFlatL2 (Exact Search for L2), as it doesn't take a lot of time, but theoretically should provide the best results in terms of search quality.
- We could use another number of approximate nearest neighbors, I used 100.
- Using cloud solutions with larger RAM, we could perform training on a full dataset.
- I used LightGBM classifier out of the box, other ML algorithms can be tested as well as trying various hyperparameters.
- last but not least, the code is ugly and probably inefficient, change as you wish.

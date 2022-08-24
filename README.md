# Kaggle-Competition-FeedbackPrize2-5th-solution
(Partly) 5th solution of the Kaggle FeedbackPrize Competition

This is a part of the 5th place solution of the Kaggle FeedbackPrize Competition in 2022. Details about the competition could be found [here](https://www.kaggle.com/competitions/feedback-prize-effectiveness).

The non-pseudo-labeling model (v1a) scores **0.576/0.579** (public/private LB), and the one with pseudo-labels (v1b) scores **0.572/0.575** (public/private LB) (after the third stage training, details about the second/third stage training could be found [here](https://www.kaggle.com/competitions/feedback-prize-effectiveness/discussion/347379)). 

Please note that the backbone is DeBERTa-v3-large, which is well-known to be non-deterministic, so the results could be different when you run with your local environment. However, approximately similar results are expected.

Because the data are too large (larger than 25MB), they are uploaded to Kaggle dataset. You can find the processed data (merged, fold spliting, etc.) [here](https://www.kaggle.com/datasets/shinomoriaoshi/feedbackprize2extradata) and the pseudo-labels (derived from model v1a) [here](https://www.kaggle.com/datasets/shinomoriaoshi/feedbackprize2pl-data).

Description of the solution is released [here](https://www.kaggle.com/competitions/feedback-prize-effectiveness/discussion/347369).

## Instruction to run the model
1. `git clone https://github.com/minhtriphan/Kaggle-Competition-FeedbackPrize2-5th-solution.git`
2. Download the competition data from [here](https://www.kaggle.com/competitions/feedback-prize-effectiveness/data) and put it in a folder name `data` (faster if we use the Kaggle API);
3. Download the data from [here](https://www.kaggle.com/datasets/shinomoriaoshi/feedbackprize2extradata) and put it in a folder name `ext_data`;
4. Download the data from [here](https://www.kaggle.com/datasets/shinomoriaoshi/feedbackprize2pl-data) and put it in a folder name `pl_data` (not necessarily for training the no-pseudo-labeling model);
5. Check the training settings in the `Config` object and adjust according to your own environment. Some remarks,
  * `gradient_checkpointing` is enabled to save the cuda memory, but in the real training, I didn't enable it to save time (trained on some A6000);
  * Evaluation are done 10 times per epoch, start evaluating only after 2/5 epochs;
  * Training is done with each fold separately, which means each execution should run with only one fold. If you want to run it with multiple folds, please clone the `.py` files and run each fold with each file.
6. Run `python train.py` to train the model without pseudo-labels and `python train_pl.py` to train the model with pseudo-labels.

Any comments, critiques, questions are welcome. Please reach me out at phanminhtri2611@gmail.com for further discussions.

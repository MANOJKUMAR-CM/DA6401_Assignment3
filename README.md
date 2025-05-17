# DA6401_Assignment3

This repository contains files for Assignment 3 of the course DA6401 - Introduction to Deep Learning at IIT Madras.

## Assignment Overview  
### Objective:
- Part A: To model sequence to sequence learning problems using Recurrent Neural Networks (RNN/ LSTM/ GRU)
- Part B: Understanding how attention networks overcome the limitations of vanilla seq2seq models
- Part C: To visualise the interactions between different components in a RNN based model.

## Links:

## [Wandb Report](https://google.com)

## [Github: Assignment3 - DA6401](https://github.com/MANOJKUMAR-CM/DA6401_Assignment3)

### Part A
To perform the hyper parameter sweep on the RNN model:
- Run `Eng2Kan_wandb_sweep.ipynb` , make sure to update `wandb.sweep()` with your own wandb credentials before running.
- **Hyperparameter Sweeps Configuration:**
  ```python
  sweep_config = {
    "name": "RNN - Hyperparameter Search",
    "metric": {
        "name": "Val_WordAccuracy", 
        "goal": "maximize"
    },
    "method": "random", # options: [bayes, random, grid]
    "parameters" : {
        "char_embedding_dim": {
            "values": [8, 12, 16, 32]
        },
        "encoder_layers" : {
            "values" : [1, 2, 3]
        },
        "decoder_layers": {
            "values": [1, 2, 3]
        },
        "hidden_state_dim":{
            "values": [64, 128, 256, 512]
        },
        "cell_type":{
            "values":["gru", "lstm", "rnn"]
        },
        "dropout": {
            "values":[0.1, 0.2, 0.3, 0.4]
        }
     }
  }
  ```
- To Train the RNN model with the best hyperparameters obtained from sweeps, execute cells of `Eng2Kan.ipynb`. It trains the model, performs inference on test set and saves the predictions of the test set as `prediction_vanilla.csv`.

  

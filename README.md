# DA6401_Assignment3

This repository contains files for Assignment 3 of the course DA6401 - Introduction to Deep Learning at IIT Madras.

## Assignment Overview  
### Objective:
- Part A: To model sequence to sequence learning problems using Recurrent Neural Networks (RNN/ LSTM/ GRU)
- Part B: Understanding how attention networks overcome the limitations of vanilla seq2seq models
- Part C: To visualise the interactions between different components in a RNN based model.

## Links:

## [Wandb Report]([https://google.com](https://wandb.ai/manoj_da24s018-iit-madras/Transliterator_Attention_HyperParameterSweep/reports/DA6401-Assignment-3--VmlldzoxMjgwMDk5NA?accessToken=i7uu6lbu8y8vijq4w0ye9wzhfi8kwzlpo1kdbrd3uj17unbt04lt9a9fvt1hkm6n)

## [Github: Assignment3 - DA6401](https://github.com/MANOJKUMAR-CM/DA6401_Assignment3)

### Part A
To perform the hyper parameter sweep on the RNN model:
- Execute cells of `Eng2Kan_wandb_sweep.ipynb` , make sure to update `wandb.sweep()` with your own wandb credentials before running.
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
#### Update WandB Credentials  
Before running the sweep, update the following command with your own WandB credentials:  

```python
wandb.sweep(sweep_config, entity="<your_name>", project="<your_project_name>")
```

- To Train the RNN model with the best hyperparameters obtained from sweeps, execute cells of `Eng2Kan.ipynb`. It trains the model, performs inference on test set and saves the predictions of the test set as `prediction_vanilla.csv`.

### Part B
To perform the hyper parameter sweep on the Attention based RNN model:
- Execute cells of `Eng2Kan_Attention_wandb_sweep.ipynb`, make sure to update `wandb.sweep()` with your own wandb credentials before running. The sweep parameters are same as that of `Part A`.
- To Train the Attention based RNN model with the best hyperparameters obtained from sweeps, execute cells of `Eng2Kan-Attention.ipynb`. It trains the model, performs inference on test set and saves the predictions of the test set as `predictions_attention.csv`.
- To visualize the attention weights in terms of attention heatmaps execute the cells of `Eng2Kan_Attention_Weights_Plots.ipynb`.

### For the plots to render the `Kannada` words : set the path to the file `NotoSansKannada-VariableFont_wdth,wght.ttf` accordingly

### Part C
Question 6: To Observe the attention of model on the input tokens while its decoding the ith output, execute `Eng2Kan_Attention_Visualization.ipynb`.
Download the file and run it locally with the necessary packages installed.

### Note: If the installed Tensorflow version is 2.10.0
```python
def pad(List, max_length):
    return sequence.data_utils.pad_sequences(List, maxlen=max_length, padding="post")
```
### Else if the version is > 2.10.0
```python
def pad(List, max_length):
    return sequence.pad_sequences(List, maxlen=max_length, padding="post")
```
If the cell throw errors, check the tensorflow version and modify the cell accordingly.

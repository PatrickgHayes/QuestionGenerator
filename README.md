# Question Generator

A text generator for generating CLEVR style questions. Initially a character RNN. 
This is copied from [the Practical PyTorch series](https://github.com/spro/practical-pytorch/blob/master/char-rnn-generation/char-rnn-generation.ipynb).


## Training

Download the [CLEVR dataset](https://s3-us-west-1.amazonaws.com/clevr/CLEVR_v1.0_no_images.zip) without the images. We don't need any of the meta-data so use the script in data cleaning scripts to remove all the meta-data. The result should be a file with one question on each line. 

Run `train.py` with the dataset filename to train and save the network:

```
> python train.py CLEVR_questions.txt

Training for 2000 epochs...
(... 10 minutes later ...)
Saved as CLEVR_questions.pt
```
After training the model will be saved as `[filename].pt`.

### Training options

```
Usage: train.py [filename] [options]

Options:
--model            Whether to use LSTM or GRU units    gru
--n_epochs         Number of epochs to train           2000
--print_every      Log learning rate at this interval  100
--hidden_size      Hidden size of GRU                  50
--n_layers         Number of GRU layers                2
--learning_rate    Learning rate                       0.01
--chunk_len        Length of training chunks           200
--batch_size       Number of examples per batch        100
--cuda             Use CUDA
```

## Generation

Run `generate.py` with the saved model from training, and a "priming string" to start the text with.

```
> python generate.py CLEVR_questions.pt --prime_str "H"

How many metal cubes are there?
```

### Generation options
```
Usage: generate.py [filename] [options]

Options:
-p, --prime_str      String to prime generation with
-l, --predict_len    Length of prediction
-t, --temperature    Temperature (higher is more chaotic)
--cuda               Use CUDA
```


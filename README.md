# Generating Multi-Agent Trajectories using Programmatic Weak Supervision

Code for paper titled [Generating Multi-Agent Trajectories using Programmatic Weak Supervision](https://arxiv.org/abs/1803.07612) by Zhan et al., ICLR 2019.

## Installation & Setup

Code is written using [PyTorch](https://pytorch.org/) version `1.0.0`.

After cloning the repository, you need to download the data.

The basketball dataset is available from [STATS](https://www.stats.com/data-science/). A pre-processed version is available [here](https://drive.google.com/drive/folders/1g6jlyYGH8rIrJfZ7TrGsCyS0Kf2d0lY-?usp=sharing). Simply download the `bball/` folder into `datasets/`.

The Boids dataset can be generated by running:
```
$ python datasets/boids/generate_data.py
```
This may take a while, so a pre-generated Boids dataset is also included in the same [link](https://drive.google.com/drive/folders/1g6jlyYGH8rIrJfZ7TrGsCyS0Kf2d0lY-?usp=sharing) above.

## Running the Code

To train a model, you can edit the parameters in `train_model.sh` and run the script from the command-line:
```
$ ./train_model.sh
```
After training a model,
```
$ python sample.py -t <trial_id> -n <num_samples> -b <burn_in> --run --plot
```
will generate and plot samples from a model and save them in `saved/<trial_id>/experiments/sample/`.

For full usage, use flag `--help`.

### Scripts

To see the parameters of a past experiment (for reproducability), run:
```
$ python scripts/print_params.py -t <trial_id>
```
To visualize examples from a test dataset, run:
```
$ python scripts/show_groundtruth.py -d <dataset> -n <num_examples>
```
which will save them into `datasets/<dataset>/data/examples/`.

To compute and compare domain statistics for basketball, run:
```
$ python sample.py -t <trial_id> -n 1000 -b 10 --run
$ python scripts/compute_bball_stats.py -t <trial_id>
```

## Pretrained Models

Included in this repository in `saved/` are four pretrained models for basketball as discussed in the paper:

| Trial ID |    Model    |
|:--------:|:-----------:|
|    101   |  RNN_GAUSS  |
|    102   | VRNN_SINGLE |
|    103   |  VRNN_INDEP |
|    104   |  MACRO_VRNN |

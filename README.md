## GNN Performance on Long Range Node Classification and Graph Classification

This repository holds the code to test 4 different neural network architectures
on 2 different long range datasets. 

Network architectures can be found under src/models, and test data (Cora) can
be found under the test directory.

To test the model's performance on a small dataset, use the docker repo b6liu/dsc180b (cpu or gpu for tag) and run:
```azure
python run.py --test True --bz (number)
```
IF ON DSMLP: Run a smaller bz if GAN errors, defaults to 32 for test. Also, we recommend using
16+ GB of ram as the networks tend to have large numbers of parameters (especially for GAN/SAN).

We would also recommend a GPU for running these tests/benchmarks, in this case, you should pull
the GPU docker image that has Cuda 11.7 support. (b6liu/dsc180b:gpu)

Different parameters can be run on the file as well.

```--dataset```: Dataset to run, currently only support all LRGB datasets. Defaults to PascalVOC-SP

```--model```: Model to run, currently GNN, GIN, GAT, SAN

```--bz```: Batch size, defaults to 32

```--epoch```: Number of epochs to run the model

```--criterion```: Loss function, defaults to cross entropy 

```--optimizer```: Optimizer to use, defaults to adam

```--lr```: Learning rate, defaults to 0.0005

```--momentum```: Momentum term, defaults to 0.9

```--weight-decay```: Weight decay term, defaults to 5e-6

```--task```: task for network, defaults to node level

```--metric```: Accuracy metric to perform, defaults to macro f1, support for AP

```--gamma```: (SAN only) sparcity of attention, 0 indicates sparse attention while 1 indicates no bias

```--hidden```: Hidden parameters, made after linearly encoding data

Shortcut methods have been added:

```--add_edges```: ratio of edges to be created (fake, random connections between nodes)

```--encode```: Positional encoding, currently only "lap" for laplacian encoding is supported

These are the recommended commands to run both LRGB datasets PascalVOC and peptides-func:

```python run.py --model gin --dataset PascalVOC-SP --metric macrof1  --add_edges 1 --criterion weighted_cross_entropy```
```python run.py --model gin --dataset peptides-func --task graph --metric ap  --add_edges 1```

### Citations
Thank you to Long Range Graph Benchmarks for the SAN implementation and datasets.
```
@article{dwivedi2022LRGB,
  title={Long Range Graph Benchmark}, 
  author={Dwivedi, Vijay Prakash and Rampášek, Ladislav and Galkin, Mikhail and Parviz, Ali and Wolf, Guy and Luu, Anh Tuan and Beaini, Dominique},
  journal={arXiv:2206.08164},
  year={2022}
}
```
And to GraphGPS, for many loss functions, SAN, and encoders:
```
@article{rampasek2022GPS,
  title={{Recipe for a General, Powerful, Scalable Graph Transformer}}, 
  author={Ladislav Ramp\'{a}\v{s}ek and Mikhail Galkin and Vijay Prakash Dwivedi and Anh Tuan Luu and Guy Wolf and Dominique Beaini},
  journal={Advances in Neural Information Processing Systems},
  volume={35},
  year={2022}
}
```
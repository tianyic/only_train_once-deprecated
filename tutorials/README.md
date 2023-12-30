# Tutorials

We will routinely update tutorials to cover varying use cases in 2024. Please expect slow update in Januaray due to recent heavy workload. 

Here are the **empirical principles** that we would like to highlight if employing OTO onto new applications outside our tutorials.

## Sanity Check

We highly recommend to proceed a sanity check to test the compliance of OTO onto target DNN. The sanity check will randomly pick up a set of minimally removal structures as redundant 

```python
oto.random_set_zero_groups()
```
and produce compact subnetwork, as presented in [sanity_check](https://github.com/tianyic/only_train_once/blob/main/sanity_check/test_resnet18.py). If sanity check does not pass, please mark illed node groups as unprunable via

```python
oto.mark_unprunable_by_node_ids()
```
For example, in [YOLOv5](https://github.com/tianyic/only_train_once/blob/main/sanity_check/test_yolov5.py), we mark the node groups corresponding to detection heads as unprunable. 

## Optimizer setup (Important)

OTO is designed to **seamlessly** integrate into the existing training pipeline for the full models. This existing pipeline is typically reliable for achieving high performance with full models.

To minimize the effort in [**hyperparameters**](https://github.com/tianyic/only_train_once/blob/cbb3d3dccf95c383e9cddcbaf8592cf3db13817b/only_train_once/__init__.py#L47) tuning while ensuring optimal performance, we recommend setting the hyperparameters in OTO's optimizers identical to those in your baseline optimizers. This approach generally yields satisfactory results in DNN compression across a wide range of applications, from computer vision to natural language processing, and from academic benchmarks to real-world AI products. However, be aware that some applications might require extended training steps for convergence due to the reduced learning capacity of sparse models.

It is important to note that different optimizer setups can lead to significantly varied performance outcomes. Additionally, there is potential that alternative hyperparameter configurations, differing from our baseline recommendation, could enhance performance. We suggest users with the interest and resources to experiment with different hyperparameter settings and explore these possibilities.


## Old tutorials 

Tutorials over old library can be found at [here](https://github.com/tianyic/only_train_once/tree/otov2_legacy_backup/tutorials). It covers ResNet50 CIFAR10, ResNet50 ImageNet and VGG16BN CIFAR10. These tutorials will be refreshed upon the new library next year. 
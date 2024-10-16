.. _getting-started:

Getting Started
===============

This section provides a quick guide to help you get started with BackdoorMBTI, including downloading data, running backdoor attacks, and executing defense experiments.

Download Data
-------------

Download the necessary data if it cannot be automatically downloaded. Some data download scripts are provided in the `scripts` folder.

Backdoor Attack
---------------

Here is an example to quickly start an attack experiment and reproduce the BadNets backdoor attack results. We use ResNet-18 as the default model and a poison ratio of 0.1.

For users installing from PyPI, you can run the following commands directly in the terminal:

.. code-block:: bash

   atk_train --data_type image --dataset cifar10 --attack_name badnet --model resnet18 --pratio 0.1 --num_workers 4 --epochs 100
   atk_train --data_type audio --dataset speechcommands --attack_name blend --model audiocnn --pratio 0.1 --num_workers 4 --epochs 100 --add_noise true
   atk_train --data_type text --dataset sst2 --attack_name addsent --model bert --pratio 0.1 --num_workers 4 --epochs 100 --mislabel true

For users installing from source code, use the following command structure:

.. code-block:: bash

   cd scripts
   python atk_train.py --data_type image --dataset cifar10 --attack_name badnet --model resnet18 --pratio 0.1 --num_workers 4 --epochs 100
   python atk_train.py --data_type audio --dataset speechcommands --attack_name blend --model audiocnn --pratio 0.1 --num_workers 4 --epochs 100 --add_noise true
   python atk_train.py --data_type text --dataset sst2 --attack_name addsent --model bert --pratio 0.1 --num_workers 4 --epochs 100 --mislabel true

To introduce noise or label mislabeling, you can add the `--add_noise true` or `--mislabel true` arguments. After the experiment, metrics such as ACC (Accuracy), ASR (Attack Success Rate), and RA (Robustness Accuracy) will be collected in the attack phase.

For more detailed command options, run:

.. code-block:: bash

   atk_train -h
   python atk_train.py -h

Backdoor Defense
----------------

For defense experiments, it depends on the backdoor model generated in the attack phase, so make sure to complete the corresponding attack experiment before running defense.

For users installing from PyPI, use the following commands:

.. code-block:: bash

   def_train --data_type image --dataset cifar10 --attack_name badnet --pratio 0.1 --defense_name finetune --num_workers 4 --epochs 10
   def_train --data_type audio --dataset speechcommands --attack_name blend --model audiocnn --pratio 0.1 --defense_name fineprune --num_workers 4 --epochs 1 --add_noise true
   def_train --data_type text --dataset sst2 --attack_name addsent --model bert --pratio 0.1 --defense_name strip --num_workers 4 --epochs 1 --mislabel true

For users installing from source code, use the following command structure:

.. code-block:: bash

   cd scripts
   python def_train.py --data_type image --dataset cifar10 --attack_name badnet --pratio 0.1 --defense_name finetune --num_workers 4 --epochs 10
   python def_train.py --data_type audio --dataset speechcommands --attack_name blend --model audiocnn --pratio 0.1 --defense_name fineprune --num_workers 4 --epochs 1 --add_noise true
   python def_train.py --data_type text --dataset sst2 --attack_name addsent --model bert --pratio 0.1 --defense_name strip --num_workers 4 --epochs 1 --mislabel true

For more details on defense commands, run:

.. code-block:: bash

   def_train -h
   python def_train.py -h

In the defense phase, detection accuracy will be collected if the defense is a detection method, and the sanitized dataset will be used to retrain the model. After retraining, ACC, ASR, and RA metrics will be collected for further evaluation.

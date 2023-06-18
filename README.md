# Bloackchain Enabled Federated learning

## Introduction
A Proof-of-Stake (PoS) blockchain-based Federated Learning framework with a validation scheme robust against the distorted local model updates. This repo hosts an simulated implementation for VBFL written in Python.



## Instructions to Run
#### <ins>Suggested</ins> Environments Setup
```
python 3.7.6
pytorch 1.4.0
```
(1) Clone the repo
```
$ git clone https://github.com/aayushdewangan11/Bloackchain_Enabled_Federated-learning.git
```
(2) Create a new conda environment with python 3.7.6
```
$ conda create -n VBFL python=3.7.6
$ conda activate VBFL
```
(3) Head to https://pytorch.org/ for instructions to install PyTorch
```
$ # If using CUDA, first check its version
$ nvidia-smi
$ # Install the correct CUDA version for PyTorch. 
$ # The code was tested on CUDA 10.1 and PyTorch 1.4.0
$ conda install pytorch=1.4.0 torchvision torchaudio cudatoolkit=10.1 -c pytorch
```
(4) Install pycryptodome 3.9.9 and matplotlib
```
$ conda install pycryptodome=3.9.9
$ conda install matplotlib
```
#### Run VBFL Simulation

Sample running command 
```
$ python main.py -nd 20 -max_ncomm 100 -ha 12,5,3 -aio 1 -pow 0 -ko 6 -nm 3 -vh 0.08 -cs 0 -B 10 -mn mnist_cnn -iid 0 -lr 0.01 -dtx 1
```

VBFL arguments

(1) <b>-nd 20</b>: 20 devices.

(2) <b>-max_ncomm 100</b>: maximum 100 communication rounds.

(3) <b>-ha 12,5,3</b>: role assignment hard-assigned to 12 workers, 5 validators and 3 miners for each communication round. A <b>*</b> in <b>-ha</b> means the corresponding number of roles are not limited. e.g., <b>-ha \*,5,\*</b> means at least 5 validators would be assigned in each communication round, and the rest of the devices are dynamically and randomly assigned to any role. <b>-ha \*,\*,\*</b> means the role-assigning in each communication round is completely dynamic and random.

(4) <b>-aio 1</b>: <i>aio</i> means "all in one network", namely, every device in the emulation has every other device in its peer list. This is to simulate that VBFL runs on a permissioned blockchain. If using <b>-aio 0</b>, the emulation will let a device (registrant) randomly register with another device (register) and copy the register's peer list.

(5) <b>-pow 0</b>: the argument of <b>-pow</b> specifies the proof-of-work difficulty. When using 0, VBFL runs with VBFL-PoS consensus to select the winning miner.

(6) <b>-ko 6</b>: this argument means a device is blacklisted after it is identified as malicious after 6 consecutive rounds as a worker.

(7) <b>-nm 3</b>: exactly 3 devices will be malicious nodes.

(8) <b>-vh 0.08</b>: validator-threshold is set to 0.08 for all communication rounds. This value may be adaptively learned by validators in a future version.

(9) <b>-cs 0</b>: as the emulation does not include mechanisms to disturb digital signature of the transactions, this argument turns off signature checking to speed up the execution.

Federated Learning arguments (inherited from https://github.com/WHDY/FedAvg)

(10) <b>-B 10</b>: batch size set to 10.

(11) <b>-mn mnist_cnn</b>: use mnist_cnn model. Another choice is mnist_2nn, or you may put your own network inside of <i>Models.py</i> and specify it.

(12) <b>-iid 0</b>: shard the training data set in Non-IID way.

(13) <b>-lr 0.01</b>: learning rate set to 0.01.

Other arguments

(14) <b>-dtx 1</b>: see <b>Known Issue</b>.

Please see <i>main.py</i> for other argument options.


Please raise other issues and concerns you found. Thank you!

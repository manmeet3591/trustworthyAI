# Testing

sudo docker pull continuumio/anaconda3

sudo run -it continuumio/anaconda3

conda create -n py36 python=3.6

source activate py36

cd home

git clone https://github.com/manmeet3591/trustworthyAI

cd trustworthyAI/Causal_Structure_Learning/Causal_Discovery_RL

wget https://cran.r-project.org/src/contrib/Archive/CAM/CAM_1.0.tar.gz

pip install -r requirements.txt

apt-get install r-base

python setup_CAM.py

cd src

git clone https://github.com/zhushy/causal-datasets

mv causal-datasets/Causal_Discovery_RL/synthetic_datasets.zip .

unzip synthetic_datasets.zip

python main.py  --max_length 12 \
                --data_size 5000 \
                --score_type BIC \
                --reg_type LR \
                --read_data  \
                --transpose \
                --data_path synthetic_datasets/exp1_12nodes/gauss_diff_noise/1/ \ # contains data.npy which is required
                --lambda_flag_default \
                --nb_epoch 20000 \
                --input_dimension 64 \
                --lambda_iter_num 1000

# To push the container to docker hub

In a new terminal

sudo docker ps -a # Note down the container_id of the running container 

sudo docker commit eb4634e3d10f crl_working # make a new image out of the container

sudo docker login # login to docker hub to push the image

sudo docker tag crl_working:latest manmeet3591/causal_reinforcement_learning:firstimagepush

sudo docker push manmeet3591/causal_reinforcement_learning:firstimagepush

https://hub.docker.com/repository/docker/manmeet3591/causal_reinforcement_learning

# To start the jupyter notebook in the container

not required for causal reinforcement learning

jupyter notebook --ip=0.0.0.0 --allow-root &

sudo docker inspect container_id # In another terminal on root

https://(ip_address_of_container):port

# Trustworthy AI

This repository aims to include trustworthy AI related projects from Huawei Noah's Ark Lab.  
Current projects include:

- gCastle (or pyCastle, pCastle)

  The real datasets (id:10, 21, 22) used in [PCIC Causal Discovery Competition 2021 ](https://competition.huaweicloud.com/information/1000041487/introduction) have been released on the github: [temporary link](https://github.com/gcastle-hub/dataset).

- Causal Structure Learning

- Causal Disentangled Representation Learning


### gCastle

- This is a causal structure learning toolchain containing various functionality related to causal learning and evaluation. A tech report describing the toolbox is available [here](https://arxiv.org/abs/2111.15155).
- The package offers a number of causal discovery algorithms, most of which are gradient-based, hence the name: **g**radient-based **Ca**usal **st**ructure **le**arning pipeline.

### Causal Structure Learning

- **Causal_Discovery_RL**: code, datasets, and training logs of the experimental results for the paper
 ['Causal discovery with reinforcement learning'](https://openreview.net/forum?id=S1g2skStPB), ICLR, 2020. (oral)
- **GAE_Causal_Structure_Learning**: an implementation for ['A graph autoencoder approach to causal structure learning'](https://arxiv.org/abs/1911.07420), NeurIPS Causal Machine Learning Workshop, 2019.
- **Datasets**: 
    - Synthetic datasets: codes for generating synthetic datasets used in the paper.
    - Real datasets: a very challenging real dataset where the objective is to find causal structures based on 
    time series data. The true graph is obtained from expert knowledge. We welcome everyone to try this dataset and 
    report the result!
- We will also release the codes for other gradient-based causal structure learning methods.

### Causal Disentangled Representation Learning

- **CausalVAE**: code and datasets of the experimental results for the paper
 ['CausalVAE: Disentangled Representation Learning via Neural Structural Causal Models'](https://arxiv.org/pdf/2004.08697.pdf), CVPR, 2021. (accepted)
- **Datasets**: code for generating synthetic datasets used in the paper.

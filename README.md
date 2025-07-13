# svdefense

## Abstract

Federated learning (FL) enables collaborative model training without sharing raw data but remains vulnerable to gradient inversion attacks (GIAs), where adversaries can reconstruct private data from shared gradients. Existing defenses either incur impractical computational overhead for embedded platforms or fail to balance privacy protection and model utility. Moreover, many defenses can be easily bypassed by adaptive adversaries who have obtained the defense details. To address these limitations, we propose SVDefense, a novel defense framework against GIAs that leverages the truncated Singular Value Decomposition (SVD) to obfuscate gradient updates. SVDefense introduces three key innovations, the Self-Adaptive Energy Threshold that adapts the privacy protection for clients with different vulnerability to GIAs caused by their varying degrees of class imbalance, the Channel-Wise Weighted Approximation that selectively preserves essential gradient information for model training while enhancing privacy protection, and the Layer-Wise Weighted Aggregation for effective aggregation of client updates under class imbalance. Our extensive evaluation shows that SVDefense outperforms existing defenses across multiple applications, including image classification, human activity recognition, and keyword spotting, by offering robust privacy protection with minimal impact on model accuracy. Furthermore, SVDefense is practical for deployment on various resource-constrained embedded platforms. We will make our code publicly available upon paper acceptance.

## Code

We provide the implementation of our defense against IG attack. Our code is developed based on [Soteria](https://github.com/jeremy313/Soteria) and [PRECODE](https://github.com/dAI-SY-Group/PRECODE).

## Setup
You can directly navigate to the folder `scripts` and run
```
/bin/bash setup.sh
```
## Quick start

### Experiment E1: Defense performance under IG attack
For IG attack, you can directly get into the scripts and run 
```
/bin/bash defense_IG.sh
```
Here you can change the `defense`, `model`, and `dataset`. 
Then you can navigate to the folder `IG_attack` and get the metric results using cal_matric.py
```
python cal_matric.py
```

### Experiment E2: perturbation-based defense performance under IG attack
Taking the PRECODE as an example, you can directly navigate to the folder `scripts` and run 
```
/bin/bash defense_PRECODE.sh
```
Then you can navigate to the folder `PRECODE` and get the metric results using cal_matric.py
```
python cal_matric.py
```

### Experiment E3: Defense performance under ROG attack
Taking the PRECODE as an example, you can directly navigate to the scripts and run 
```
/bin/bash defense_PRECODE.sh
```
Then you can navigate to the folder `PRECODE` and get the metric results using cal_matric.py
```
python cal_matric.py
```

### Experiment E4: Classification performance on cifar10 dataset
For federated learning, we utilize the [flower framework](https://github.com/adap/flower).
You can change the parameters of `pyproject.toml` in the `svd-defense` folder. If your device can only support CPU, change the parameter `server-device` and `server-device` to 'cpu', otherwise to 'cuda'. The default is 'cpu'.
To directly get the sample defense performance, you can navigate to the folder `scripts` and run 
```
/bin/bash fl.sh
```
The accuracy across epochs can be found in svd-defense/{defense}_acc.txt. Then 
```
python draw.py
```
can output one line of results of the corresponding defense in Fig.7.

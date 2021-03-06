## Speech Separation with uPIT

Speech separation with utterance-level PIT(Permutation Invariant Training)

### Requirements

see [requirements.txt](requirements.txt)

### Usage

1. Generate dataset using [create-speaker-mixtures.zip](http://www.merl.com/demos/deep-clustering/create-speaker-mixtures.zip)

2. Prepare cmvn, .scp and configure experiments in .yaml files

3. Training:
    ```shell
    ./run_pit.py --config $conf --num-epoches 50 > $checkpoint/train.log 2>&1 &
    ```

4. Inference:
    ```
    ./separate.py --dump-dir cache $mdl_dir/train.yaml $mdl_dir/epoch.40.pkl egs.scp
    ```

### Experiments

| Configure | Mask | Epoch |  FM   |  FF  |  MM  | FF/MM | AVG  |
| :-------: | :--: | :---: | :---: | :--: | :--: | :---: | :--: |
| [config-1](conf/1.config.yaml) |  AM-ReLU    |  63   | 10.38 |  6.64 |  7.31 | 6.98  | 8.78  |
| [config-2](conf/2.config.yaml) |  AM-sigmoid |  50   | 9.95  |  5.99 |  6.72 | 6.35  | 8.26  |
|             -                  |  AM-oracle  |   -   | 12.49 | 12.73 | 11.58 | 11.88 | 12.19 |
|             -                  |  IRM-oracle |   -   | 12.86 | 13.14 | 11.96 | 12.27 | 12.57 |
|             -                  |  PSM-oracle |   -   | 15.79 | 16.03 | 14.90 | 15.20 | 15.50 |


### Reference

* Kolbæk M, Yu D, Tan Z H, et al. Multitalker speech separation with utterance-level permutation invariant training of deep recurrent neural networks[J]. IEEE/ACM Transactions on Audio, Speech and Language Processing (TASLP), 2017, 25(10): 1901-1913.
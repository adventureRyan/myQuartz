```python
config_path: args/config.yaml
gpus: [0]
no_progress_bar: False
is_random: True
resume: False
resume_latest: False
times: 2023_07_20_16.45.12
generate_data: False
dataset: sysu-xsub
dataset_args: {'ntu': {'eval_batch_size': 24, 'inputs': 'J', 'ntu120_path': '/home/dataset/ntu-rgbd-120', 'ntu60_path': '/home/dataset/ntu-rgbd-60', 'num_frame': 300, 'root_folder': '/home/dataset/jgl/datav2/dataset', 'train_batch_size': 24, 'transform': True}, 'sysu': {'eval_batch_size': 6, 'hangshu': 10, 'inputs': 'JVB', 'num_frame': 600, 'sysu_path': '/home/ryan/Documents/workspace/python7/epv99/datasets', 'train_batch_size': 6, 'transform': True}}
ignore_path: ./src/ignore.txt
visual_rate: 0.2
model_args: {}
backbone_name: 2005_EfficientGCN-B2
print_net: True
max_epoch: 90
is_sche_complex: False
backbone_model_args: {'act_type': 'swish', 'att_type': 'stja', 'bias': True, 'block_args': [[48, 1, 1], [36, 1, 1], [24, 1, 1], [64, 1, 1], [64, 1, 1], [128, 1, 1], [128, 2, 1], [256, 1, 1], [256, 2, 1], [512, 1, 1]], 'dilations': [1, 2], 'drop_prob': 0.0, 'edge': True, 'fusion_stage': 3, 'kernel_size': [5, 2], 'layer_type': 'Multi', 'reduct_ratio': 2, 'stem_channel': 128}
debug: False
lr_scheduler: step
model_name: jgl_net
optimizer: SGD
optimizer_args: {'Adam': {'betas': [0.9, 0.99], 'lr': 0.1, 'weight_decay': 0.0001}, 'AdamW': {'lr': 0.1, 'weight_decay': 0.0001}, 'SGD': {'lr': 0.1, 'momentum': 0.9, 'nesterov': True, 'weight_decay': 0.0001}}
pretrained_path: /home/ryan/Documents/workspace/python7/epv99/pre_train_param/checkpointt34.pth.tar
scheduler_args: {'cosine': {'max_epoch': 60, 'warm_up': 10}, 'multifactor': 'max_epoch:60', 'step': {'max_epoch': 40, 'step_lr': [15, 30], 'warm_up': 5}}
```

### 1. huggingface连接失败
File "/home/hry/anaconda3/envs/map_reg/lib/python3.7/site-packages/huggingface_hub/file_download.py", line 1292, in hf_hub_download "Connection error, and we cannot find the requested files in"
解决方法：export HF_ENDPOINT="https://hf-mirror.com"
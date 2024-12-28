1. find existing ssh key.pub, copy it to lambda lab
2. launch instance using this key.pub
3. Cmd + Shift + P, type "Remote-SSH: Open SSH Configuration File"
4. Add the following to the file:
```
Host lambda-lab
    HostName your-instance-ip
    User ubuntu
    IdentityFile ~/.ssh/lamda.pem
```
5. Connect to the host using "lambda-lab", open folder to the project folder
6. Set up ssh key in lambda gpu instance
    a. ssh-keygen -t ed25519 -C "your-email@example.com"
    b. cat ~/.ssh/id_ed25519.pub
    c. paste the key to the github ssh key settings
    d. ssh -T git@github.com # test ssh connection
7. git clone the repo
8. install conda 
```
sudo apt update
sudo apt install python3-pip
pip3 install conda
```
9. conda create -n ic-light python=3.10
10. conda activate ic-light
11. pip install torch torchvision --index-url https://download.pytorch.org/whl/cu121
12. pip install -r requirements.txt
13. python gradio_demo.py

# Deployment
Problem 1. Fix import error "cannot import name 'cached_download'"
Fix 1. pip install huggingface-hub==0.25.0
Reference: https://github.com/lllyasviel/IC-Light/issues/114

Problem 2. AssertionError: Torch not compiled with CUDA enabled

Problem 3. git@github.com: Permission denied (publickey).
Fix 3. nano /home/ubuntu/.ssh/config
```
Host github.com
    HostName github.com
    User git
    IdentityFile /home/ubuntu/lily-arizona/.ssh/id_ed25519
```

Problem 4. ImportError: cannot import name 'EncoderDecoderCache' from 'transformers'
```
pip install peft==0.13.0
```

Problem 5. Inference error when running gradio_demo.py


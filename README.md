<div align="center">
  <a href="https://ollama.com">
    <img alt="ollama" height="200px" src="https://github.com/ollama/ollama/assets/3325447/0d0b44e2-8f4a-4e99-9b52-a5c1c741c8f7">
  </a>
</div>

# Ollama
K80 support | Ubuntu 24.04 | 03/2025

Officially unsupported, but lots of us are hobbyists; this is a Hitchhikers guide to running Ollama on commodity ‘unsupported’ 
nvidia cards in the Kepler series: 

On fresh Ubuntu latest 24.04 LTS
sudo apt-get update
sudo apt-get install -y nvidia-driver-470
sudo reboot
nvidia-smi
wget https://developer.download.nvidia.com/compute/cuda/11.4.4/local_installers/cuda_11.4.4_470.82.01_linux.run
chmod +x cuda_11.4.4_470.82.01_linux.run
sudo sh cuda_11.4.4_470.82.01_linux.run --silent --toolkit --override
echo 'export PATH=/usr/local/cuda/bin${PATH:+:${PATH}}' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc
source ~/.bashrc
nvcc --version
cd ~
git clone https://github.com/Soledge/ollama37
mv ollama37 ollama
sudo reboot

cd ~/ollama
cmake -B build
cmake --build build
go run . serve &
go build .
ln -s ~/ollama/ollama /usr/local/bin/ollama

export MODEL= (phi4-mini, deepseek, etc)
ollama pull $MODEL
ollama run $MODEL

Enjoy.
# Web parsing service Crawl4AI

### http requests - port 5001

Setting up for user pnm12 from group pnm12

Create a folder for work
```
mkdir crawl4ai
cd crawl4ai
```

Create a virtual environment
```
python3 -m venv env
source env/bin/activate
pip list
```

Install components and run installation
```
pip install flask
pip install crawl4ai
crawl4ai-setup # Setup the browser
```

The following packages will be installed
```
aiofiles                  24.1.0
aiohappyeyeballs          2.6.1
aiohttp                   3.11.14
aiosignal                 1.3.2
aiosqlite                 0.21.0
annotated-types           0.7.0
anyio                     4.9.0
attrs                     25.3.0
beautifulsoup4            4.13.3
blinker                   1.9.0
certifi                   2025.1.31
cffi                      1.17.1
charset-normalizer        3.4.1
click                     8.1.8
colorama                  0.4.6
Crawl4AI                  0.5.0.post4
cryptography              44.0.2
cssselect                 1.3.0
distro                    1.9.0
fake-http-header          0.3.5
fake-useragent            2.1.0
faust-cchardet            2.1.19
filelock                  3.18.0
Flask                     3.1.0
frozenlist                1.5.0
fsspec                    2025.3.0
greenlet                  3.1.1
h11                       0.14.0
httpcore                  1.0.7
httpx                     0.28.1
huggingface-hub           0.29.3
humanize                  4.12.1
idna                      3.10
importlib_metadata        8.6.1
itsdangerous              2.2.0
Jinja2                    3.1.6
jiter                     0.9.0
joblib                    1.4.2
jsonschema                4.23.0
jsonschema-specifications 2024.10.1
litellm                   1.63.11
lxml                      5.3.1
markdown-it-py            3.0.0
markdownify               1.1.0
MarkupSafe                3.0.2
mdurl                     0.1.2
mpmath                    1.3.0
multidict                 6.2.0
networkx                  3.4.2
nltk                      3.9.1
numpy                     2.2.4
nvidia-cublas-cu12        12.4.5.8
nvidia-cuda-cupti-cu12    12.4.127
nvidia-cuda-nvrtc-cu12    12.4.127
nvidia-cuda-runtime-cu12  12.4.127
nvidia-cudnn-cu12         9.1.0.70
nvidia-cufft-cu12         11.2.1.3
nvidia-curand-cu12        10.3.5.147
nvidia-cusolver-cu12      11.6.1.9
nvidia-cusparse-cu12      12.3.1.170
nvidia-cusparselt-cu12    0.6.2
nvidia-nccl-cu12          2.21.5
nvidia-nvjitlink-cu12     12.4.127
nvidia-nvtx-cu12          12.4.127
openai                    1.66.3
packaging                 24.2
pillow                    10.4.0
pip                       24.0
playwright                1.50.0
propcache                 0.3.0
psutil                    7.0.0
pycparser                 2.22
pydantic                  2.10.6
pydantic_core             2.27.2
pyee                      12.1.1
Pygments                  2.19.1
pyOpenSSL                 25.0.0
pyperclip                 1.9.0
python-dotenv             1.0.1
PyYAML                    6.0.2
rank-bm25                 0.2.2
referencing               0.36.2
regex                     2024.11.6
requests                  2.32.3
rich                      13.9.4
rpds-py                   0.23.1
safetensors               0.5.3
scikit-learn              1.6.1
scipy                     1.15.2
setuptools                76.0.0
six                       1.17.0
sniffio                   1.3.1
snowballstemmer           2.2.0
soupsieve                 2.6
sympy                     1.13.1
tf-playwright-stealth     1.1.2
threadpoolctl             3.6.0
tiktoken                  0.9.0
tokenizers                0.21.1
torch                     2.6.0
tqdm                      4.67.1
transformers              4.49.0
triton                    3.2.0
typing_extensions         4.12.2
urllib3                   2.3.0
Werkzeug                  3.1.3
xxhash                    3.5.0
yarl                      1.18.3
zipp                      3.21.0
```

Copy the app1.py application to the folder

Add the service to systemD (sudo nano /etc/systemd/system/ai-consultant.service)
```
[Unit]
Description=ai-consultant
After=network-online.target nss-user-lookup.target

[Service]
User=pnm12
Group=pnm12
WorkingDirectory=/home/pnm12/crawl4ai
Environment="PYTHONPATH=/home/pnm12/crawl4ai/env/lib/python3.12/site-packages"             # python3.12???
ExecStartPre=/usr/bin/sleep 10
ExecStart=/home/pnm12/crawl4ai/env/bin/python3.12 /home/pnm12/crawl4ai/app1.py               # python3.12???

RestartSec=10
Restart=always
StandardOutput=journal
StandardError=journal

[Install]
WantedBy=multi-user.target
```

Setting up systemD
```
sudo systemctl daemon-reload
sudo systemctl enable --now ai-consultant.service
systemctl status ai-consultant.service
```

Debugging
```
systemctl status ai-consultant.service
journalctl -xeu ai-consultant.service
systemctl is-enabled ai-consultant.service
```

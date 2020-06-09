# My Solution to atmaCup 5 (private 2nd, public 5th)
夢中でやっていました。運営のみなさま、楽しい時間を過ごさせていただき、ありがとうございました！

## Solution Summary
GBDTs (LightGBM, XGBoost, CatBoost)のmedian ensembleです。

- Conv1Dの中間層の出力特徴量
- 信号の微分特徴量
- 信号のFFT特徴量

が特に効いていました。

- undersampling + bagging
- seed average
- class weight設定

といった、不均衡データへの対策を特に意識してモデリングしていました。最後にpseudolabelによってスコアを底上げしました。

## Usage

- このrepositoryをcloneしてくる
- ```input, output```フォルダを```code```と同じdirectory上へ作る

```
.
├── code
├── output
└── input

```

- atmaCup 5のデータをinputフォルダへ
- ```run_all.sh```を実行（outputフォルダに、最終サブである```submission_med.csv```など結果が保存される）

## 実行環境
Anacondaに、

- lightGBM (lightgbm==2.3.0)
- XGBoost (xgboost==1.0.2)
- CatBoost (catboost==0.23)
- Tensorflow (tensorflow==2.1.0)
- tensorflow-addons (tensorflow-addons==0.9.1)
- UMAP (umap-learn==0.4.4) 

を追加して使っています。

### python & conda version

```
Python 3.7.6
conda 4.8.3
```

### Docker

Docker で実行する場合の手順です。ローカル環境には docker / docker-compose をインストールしてください。

```bash
cp project.env .env #  step1: .env に環境変数ファイルをコピー
nano .env #  step2: 必要があれば編集

docker-compose up -d --build  # step3: image を build してコンテナ立ち上げ
```

`.env` で以下の設定が行えます

- INPUT_DIR: 入力になるデータのディレクトリです。
- OUTPUT_DIR: 作成されたモデル、特徴量などが保存されるディレクトリです

スクリプトを実行する場合には docker container 内部で実行します

```bash
➜ docker exec -it katsu-atmacup-5-conda bash
(base) root@0f8f3ab4a6a1:/analysis# python -V
Python 3.7.6
(base) root@0f8f3ab4a6a1:/analysis# conda -V
conda 4.8.2
```

### modules

```
absl-py==0.9.0
alabaster==0.7.12
anaconda-client==1.7.2
anaconda-navigator==1.9.12
anaconda-project==0.8.3
argh==0.26.2
asn1crypto==1.3.0
astor==0.8.1
astroid==2.3.3
astropy==4.0
atomicwrites==1.3.0
attrs==19.3.0
autopep8==1.4.4
Babel==2.8.0
backcall==0.1.0
backports.functools-lru-cache==1.6.1
backports.shutil-get-terminal-size==1.0.0
backports.tempfile==1.0
backports.weakref==1.0.post1
beautifulsoup4==4.8.2
bitarray==1.2.1
bkcharts==0.2
bleach==3.1.0
bokeh==1.4.0
boto==2.49.0
Bottleneck==1.3.2
cachetools==4.1.0
catboost==0.23
certifi==2019.11.28
cffi==1.14.0
chardet==3.0.4
Click==7.0
cloudpickle==1.3.0
clyent==1.2.2
colorama==0.4.3
conda==4.8.3
conda-build==3.18.11
conda-package-handling==1.7.0
conda-verify==3.4.2
contextlib2==0.6.0.post1
cryptography==2.8
cycler==0.10.0
Cython==0.29.15
cytoolz==0.10.1
dask==2.11.0
decorator==4.4.1
defusedxml==0.6.0
diff-match-patch==20181111
distributed==2.11.0
docutils==0.16
entrypoints==0.3
et-xmlfile==1.0.1
fastcache==1.1.0
filelock==3.0.12
flake8==3.7.9
Flask==1.1.1
fsspec==0.6.2
future==0.18.2
gast==0.2.2
gevent==1.4.0
glob2==0.7
gmpy2==2.0.8
google-auth==1.16.1
google-auth-oauthlib==0.4.1
google-pasta==0.2.0
greenlet==0.4.15
grpcio==1.29.0
h5py==2.10.0
HeapDict==1.0.1
html5lib==1.0.1
hypothesis==5.5.4
idna==2.8
imageio==2.6.1
imagesize==1.2.0
importlib-metadata==1.5.0
intervaltree==3.0.2
ipykernel==5.1.4
ipython==7.12.0
ipython-genutils==0.2.0
ipywidgets==7.5.1
isort==4.3.21
itsdangerous==1.1.0
jdcal==1.4.1
jedi==0.14.1
jeepney==0.4.2
Jinja2==2.11.1
joblib==0.14.1
json5==0.9.1
jsonschema==3.2.0
jupyter==1.0.0
jupyter-client==5.3.4
jupyter-console==6.1.0
jupyter-core==4.6.1
jupyterlab==1.2.6
jupyterlab-server==1.0.6
Keras-Applications==1.0.8
Keras-Preprocessing==1.1.2
keyring==21.1.0
kiwisolver==1.1.0
lazy-object-proxy==1.4.3
libarchive-c==2.8
lief==0.9.0
lightgbm==2.3.0
llvmlite==0.31.0
locket==0.2.0
lxml==4.5.0
Markdown==3.2.2
MarkupSafe==1.1.1
matplotlib==3.1.3
mccabe==0.6.1
mistune==0.8.4
mkl-fft==1.0.15
mkl-random==1.1.0
mkl-service==2.3.0
mock==4.0.1
more-itertools==8.2.0
mpmath==1.1.0
msgpack==0.6.1
multipledispatch==0.6.0
navigator-updater==0.2.1
nbconvert==5.6.1
nbformat==5.0.4
networkx==2.4
nltk==3.4.5
nose==1.3.7
notebook==6.0.3
numba==0.48.0
numexpr==2.7.1
numpy==1.18.1
numpydoc==0.9.2
oauthlib==3.1.0
olefile==0.46
openpyxl==3.0.3
opt-einsum==3.2.1
packaging==20.1
pandas==1.0.1
pandocfilters==1.4.2
parso==0.5.2
partd==1.1.0
path==13.1.0
pathlib2==2.3.5
pathtools==0.1.2
patsy==0.5.1
pep8==1.7.1
pexpect==4.8.0
pickleshare==0.7.5
Pillow==7.0.0
pkginfo==1.5.0.1
pluggy==0.13.1
ply==3.11
prometheus-client==0.7.1
prompt-toolkit==3.0.3
protobuf==3.12.2
psutil==5.6.7
ptyprocess==0.6.0
py==1.8.1
pyasn1==0.4.8
pyasn1-modules==0.2.8
pycodestyle==2.5.0
pycosat==0.6.3
pycparser==2.19
pycrypto==2.6.1
pycurl==7.43.0.5
pydocstyle==4.0.1
pyflakes==2.1.1
Pygments==2.5.2
pylint==2.4.4
pyodbc===4.0.0-unsupported
pyOpenSSL==19.1.0
pyparsing==2.4.6
pyrsistent==0.15.7
PySocks==1.7.1
pytest==5.3.5
pytest-arraydiff==0.3
pytest-astropy==0.8.0
pytest-astropy-header==0.1.2
pytest-doctestplus==0.5.0
pytest-openfiles==0.4.0
pytest-remotedata==0.3.2
python-dateutil==2.8.1
python-jsonrpc-server==0.3.4
python-language-server==0.31.7
pytz==2019.3
PyWavelets==1.1.1
pyxdg==0.26
PyYAML==5.3
pyzmq==18.1.1
QDarkStyle==2.8
QtAwesome==0.6.1
qtconsole==4.6.0
QtPy==1.9.0
requests==2.22.0
requests-oauthlib==1.3.0
rope==0.16.0
rsa==4.0
Rtree==0.9.3
ruamel-yaml==0.15.87
scikit-image==0.16.2
scikit-learn==0.22.1
scipy==1.4.1
seaborn==0.10.0
SecretStorage==3.1.2
Send2Trash==1.5.0
simplegeneric==0.8.1
singledispatch==3.4.0.3
six==1.14.0
snowballstemmer==2.0.0
sortedcollections==1.1.2
sortedcontainers==2.1.0
soupsieve==1.9.5
Sphinx==2.4.0
sphinxcontrib-applehelp==1.0.1
sphinxcontrib-devhelp==1.0.1
sphinxcontrib-htmlhelp==1.0.2
sphinxcontrib-jsmath==1.0.1
sphinxcontrib-qthelp==1.0.2
sphinxcontrib-serializinghtml==1.1.3
sphinxcontrib-websupport==1.2.0
spyder==4.0.1
spyder-kernels==1.8.1
SQLAlchemy==1.3.13
statsmodels==0.11.0
sympy==1.5.1
tables==3.6.1
tblib==1.6.0
tensorboard==2.1.1
tensorflow==2.1.0
tensorflow-addons==0.9.1
tensorflow-estimator==2.1.0
termcolor==1.1.0
terminado==0.8.3
testpath==0.4.4
toolz==0.10.0
tornado==6.0.3
tqdm==4.42.1
traitlets==4.3.3
ujson==1.35
umap-learn==0.4.4
unicodecsv==0.14.1
urllib3==1.25.8
watchdog==0.10.2
wcwidth==0.1.8
webencodings==0.5.1
Werkzeug==1.0.0
widgetsnbextension==3.5.1
wrapt==1.11.2
wurlitzer==2.0.0
xlrd==1.2.0
XlsxWriter==1.2.7
xlwt==1.3.0
xmltodict==0.12.0
yapf==0.28.0
zict==1.0.0
zipp==2.2.0
```
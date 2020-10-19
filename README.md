## jupyter-enterprise-gateway 安裝過程
> 憑著記憶寫出安裝過程，如果有不完善的地方或在安裝過程遇到錯誤還麻煩請提出

> 另外小弟目前是Spark新手，參數有設置不好的地方還請多多指教 :)

> E-mail：starlight395@gmail.com

> 目的：讓jupyter可以使用delpoy mode=cluster

### 安裝虛擬環境

*  這裡沒有要求一定要用anaconda/miniconda或virtualenv套件，使用虛擬環境原因除了可以設定自己的使用環境不干擾其他使用環境，之後可以打包成zip檔上傳至YARN讓其他的executor去使用相關的package，我是使用miniconda安裝虛擬環境，python=3.5
```  
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86.sh
chmod +x ./Miniconda3-latest-Linux-x86_64.sh
./Miniconda3-latest-Linux-x86_64.sh
source ~/.bashrc
conda create --name mySparkEnv python=3.5
```
    
### 安裝相關套件

*  這裡請注意要使用pip安裝相關package，使用conda會安裝到舊版，基本上只要這幾個即可，但我還是會附上目前安裝的list供參考：
```
pip install jupyter
pip install jupyter_enterprise_gateway
pip install jupyter-kernel-gateway
```

*  pip list
```
Package                           Version
--------------------------------- ------------
apache-log-parser                 1.7.0
apachelogs                        0.6.0
argon2-cffi                       20.1.0
attrs                             20.2.0
backcall                          0.2.0
bcrypt                            3.1.7
bleach                            3.2.1
cachetools                        4.1.1
certifi                           2018.8.24
cffi                              1.14.3
chardet                           3.0.4
click                             7.1.2
cloudpickle                       1.6.0
confluent-kafka                   1.5.0
cryptography                      3.1.1
cycler                            0.10.0
dask                              2.6.0
decorator                         4.4.2
defusedxml                        0.6.0
distributed                       2.6.0
docker                            4.3.1
docopt                            0.6.2
entrypoints                       0.3
featuretools                      0.13.4
findspark                         1.4.2
future                            0.18.2
google-auth                       1.22.1
hdfs                              2.5.8
HeapDict                          1.0.1
idna                              2.10
importlib-metadata                2.0.0
ipykernel                         5.3.4
ipython                           7.9.0
ipython-genutils                  0.2.0
jedi                              0.17.2
Jinja2                            2.11.2
joblib                            0.14.1
json5                             0.9.5
jsonschema                        3.2.0
jupyter                           1.0.0
jupyter-client                    6.1.7
jupyter-contrib-core              0.3.3
jupyter-contrib-nbextensions      0.5.1
jupyter-core                      4.6.3
jupyter-enterprise-gateway        2.3.0
jupyter-highlight-selected-word   0.2.0
jupyter-kernel-gateway            2.4.3
jupyter-latex-envs                1.4.6
jupyter-nbextensions-configurator 0.4.1
jupyterlab                        2.2.8
jupyterlab-server                 1.2.0
kiwisolver                        1.1.0
kmodes                            0.10.2
kubernetes                        12.0.0
lesscpy                           0.14.0
lightgbm                          3.0.0
lxml                              4.5.2
MarkupSafe                        1.1.1
matplotlib                        3.0.3
mistune                           0.8.4
msgpack                           0.6.2
nbconvert                         5.6.1
nbformat                          5.0.8
notebook                          6.1.4
numpy                             1.18.5
oauthlib                          3.1.0
packaging                         20.4
pandas                            0.25.3
pandocfilters                     1.4.2
paramiko                          2.7.2
parso                             0.7.1
pexpect                           4.8.0
pickleshare                       0.7.5
pip                               10.0.1
ply                               3.11
prometheus-client                 0.8.0
prompt-toolkit                    2.0.10
psutil                            5.7.2
ptyprocess                        0.6.0
py4j                              0.10.9
pyasn1                            0.4.6
pyasn1-modules                    0.2.8
pycparser                         2.20
pycryptodomex                     3.9.8
pydicti                           1.1.3
PyEmail                           0.0.1
Pygments                          2.7.1
PyNaCl                            1.4.0
pyparsing                         2.4.7
pypinyin                          0.39.0
pyrsistent                        0.17.3
pyspark                           3.0.0
python-dateutil                   2.8.1
pytz                              2020.1
PyYAML                            5.3.1
pyzmq                             19.0.2
requests                          2.24.0
requests-oauthlib                 1.3.0
rsa                               4.6
scikit-learn                      0.22.2.post1
scipy                             1.4.1
seaborn                           0.9.1
Send2Trash                        1.5.0
setuptools                        40.3.0
six                               1.15.0
sortedcontainers                  2.2.2
tblib                             1.7.0
terminado                         0.8.3
testpath                          0.4.4
toolz                             0.11.1
tornado                           6.0.4
tqdm                              4.49.0
traitlets                         4.3.3
ua-parser                         0.10.0
urllib3                           1.25.9
user-agents                       2.2.0
wcwidth                           0.2.5
webencodings                      0.5.1
websocket-client                  0.57.0
wheel                             0.35.1
yapf                              0.30.0
yarn-api-client                   1.0.2
zict                              2.0.0
zipp                              1.2.0
``` 

### 安裝YARN cluster mode 
*  [YARN cluster mode](https://jupyter-enterprise-gateway.readthedocs.io/en/latest/kernel-yarn-cluster-mode.html)
```
wget https://github.com/jupyter/enterprise_gateway/releases/download/v2.3.0/jupyter_enterprise_gateway_kernelspecs-2.3.0.tar.gz
mdkir /home/{username}/minconda3/env/{yourEnvName}/share/jupyter/kernel/spark_python_yarn_cluster
KERNELS_FOLDER=/home/{username}/minconda3/env/{yourEnvName}/share/jupyter/kernel/spark_python_yarn_cluster
tar -zxvf jupyter_enterprise_gateway_kernelspecs-2.3.0.tar.gz --strip 1 --directory $KERNELS_FOLDER/spark_python_yarn_cluster/ spark_python_yarn_cluster/
```

### vim spark_python_yarn_cluster kernel.json file

*  PATH：/home/{username}/minconda3/env/{yourEnvName}/share/jupyter/kernel/spark_python_yarn_cluster/kernel.json file
*  附上我的file作為參考
*  是否能改動appname? 有試過似乎是不行，從EG的程式看他是用appName抓application ID，改動會抓不到導致無法啟動
```
{
  "language": "python",
  "display_name": "Spark - Python (YARN Cluster Mode)",
  "metadata": {
	"process_proxy": {
	  "class_name": "enterprise_gateway.services.processproxies.yarn.YarnClusterProcessProxy"
	}
  },
  "env": {
	"SPARK_HOME": "/home/ericjiang/miniconda3/envs/cluster/spark-2.4.3-bin-hadoop2.7",
	"SPARK_CONF_DIR": "/home/ericjiang/miniconda3/envs/cluster/spark-2.4.3-bin-hadoop2.7/conf",
	"HADOOP_HOME": "/home/ericjiang/miniconda3/envs/cluster/hadoop-2.7.3",
	"HADOOP_CONF_DIR": "/home/ericjiang/miniconda3/envs/cluster/hadoop-2.7.3/etc/hadoop/",	
	"PROG_HOME": "/home/ericjiang/miniconda3/envs/cluster/share/jupyter/kernels/spark_python_yarn_cluster",
	"PYSPARK_PYTHON": "/usr/bin/python3",
	"PYTHONPATH": "/home/ericjiang/miniconda3/envs/cluster/lib/python3.5/site-packages:/home/ericjiang/miniconda3/envs/cluster/spark-2.4.3-bin-hadoop2.7/python:/home/ericjiang/miniconda3/envs/cluster/spark-2.4.3-bin-hadoop2.7/python/lib/py4j-0.10.7-src.zip",
	"SPARK_OPTS": "--master yarn --deploy-mode cluster --name ${KERNEL_ID:-ERROR__NO__KERNEL_ID} --py-files /home/ericjiang/dependencies.zip --conf spark.sql.auto.repartition=ture --conf spark.executor.heartbeatInterval=60 --conf spark.yarn.queue=spark --conf spark.executor.instances=5 --conf spark.driver-memory=8g --conf spark.driver.cores=4 --conf spark.executor.memory=8g --conf spark.executor.cores=4 --conf spark.default.parallelism=600 --conf spark.sql.shuffle.partitions=400 --conf spark.yarn.submit.waitAppCompletion=false --conf spark.yarn.dist.archives=/home/ericjiang/miniconda3/envs/cluster.zip#cluster --conf spark.yarn.appMasterEnv.PYSPARK_PYTHON=cluster/bin/python3.5 --conf spark.yarn.executorEnv.PYSPARK_PYTHON=cluster/bin/python3.5 --conf spark.yarn.appMasterEnv.PYTHONUSERBASE=cluster --conf spark.yarn.appMasterEnv.PYTHONPATH=cluster/lib/python3.5/site-packages:cluster/spark-2.4.3-bin-hadoop2.7/python:cluster/spark-2.4.3-bin-hadoop2.7/python/lib/py4j-0.10.7-src.zip --conf spark.yarn.appMasterEnv.PATH=cluster/bin:$PATH ${KERNEL_EXTRA_SPARK_OPTS}",
	"LAUNCH_OPTS": ""
  },
  "argv": [
	"/home/ericjiang/miniconda3/envs/cluster/share/jupyter/kernels/spark_python_yarn_cluster/bin/run.sh",
	"--RemoteProcessProxy.kernel-id",
	"{kernel_id}",
	"--RemoteProcessProxy.response-address",
	"{response_address}",
	"--RemoteProcessProxy.port-range",
	"{port_range}",
	"--RemoteProcessProxy.spark-context-initialization-mode",
	"lazy"
  ]
}
```

### vim jupyter_enterprise_gateway_config.py
*  輸入
`jupyter enterprisegateway --generate-config`
會產生`jupyter_enterprise_gateway_config.py`，在其中增加`c.EnterpriseGatewayApp.yarn_endpoint = 'http://172.24.0.12:8088/cluster'`

### 設定環境參數
*  可在`spark-env.sh`或`~/.bashrc`設置SPARK_HOME、HADOOP_HOME、SPARK_CONF_DIR、HADOOP_CONF_DIR路徑

### RUN

*  在不同的視窗啟動jupyter enterprise gateway & jupyter notebook
```
jupyter enterprisegateway --ip=172.24.0.216 --port_retries=0 --debug
jupyter notebook  --gateway-url=http://172.24.0.216:8888
```
接著啟動核心即可！




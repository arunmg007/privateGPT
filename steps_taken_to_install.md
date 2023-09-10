# Steps Taken to Install





## Steps

### Install Python 3.11

```bash
❯ sudo add-apt-repository ppa:deadsnakes/ppa
❯ sudo apt-get install python3.11 python3.11-venv 
❯ sudo apt-get build-essential libssl-dev libffi-dev python3.11-dev
```

*Note:* 
- Adding Python repo enables `apt-get` to download latest python 3.11 packages. 
- `build-essential` `libssl-dev` `libffi-dev` `python3.11-dev` these packages helps during the pip build requirements.



### Activating Python Virtual Env

```bash
❯ python3.11 -m venv privategpt
❯ cd privategpt
❯ source bin/activate
❯ python3.11 -m pip install pip
    Requirement already satisfied: pip in ./lib/python3.11/site-packages (23.2.1)
```


### Download GitHub repo

```bash
❯ git clone https://github.com/arunmg007/privateGPT.git 
❯ cd privateGPT
```

### Build Python pip requirements

```bash
❯ python3.11 -m pip install -r requirements.txt
```

### Download Language Module

```bash
❯ mkdir models
❯ cd models
❯ wget https://gpt4all.io/models/ggml-gpt4all-j-v1.3-groovy.bin
❯ cd ..
```

### Rename the env file

```bash
❯ cp example.env example.env.bak
❯ mv example.env .env
```

### Sqlite3 Upgrade to >= 3.35.x

```bash
❯ cd ..
❯ wget -c https://www.sqlite.org/2023/sqlite-autoconf-3430000.tar.gz
❯ mkdir sqlite3 && cd sqlite3
❯ tar xvfz ../sqlite-autoconf-3430000.tar.gz
❯ cd sqlite-autoconf-3430000/
❯ ./configure
❯ make
❯ sudo make install
```

*Note:* Check if Python3.11 reflects this version. If it doesn't follow this

```bash
❯ python3.11 -c "import sqlite3; print(sqlite3.sqlite_version)"
❯ ldd `find /usr/lib/python3.11/ -name '_sqlite3*'` | grep sqlite
	        libsqlite3.so.0 => /lib/x86_64-linux-gnu/libsqlite3.so.0 (0x00007f8a4812a000)
❯ sudo cp /lib/x86_64-linux-gnu/libsqlite3.so.0 libsqlite3.so.0.bakup.old.version
❯ sudo cp .libs/libsqlite3.so.0 /lib/x86_64-linux-gnu/
❯ python3.11 -c "import sqlite3; print(sqlite3.sqlite_version)"
```

### All Good to Ingest 

```bash
❯ python3.11 ingest.py
Downloading (…)e9125/.gitattributes: 100%|████████████████████████████████████████████████████████████████████████████| 1.18k/1.18k [00:00
Downloading (…)_Pooling/config.json: 100%|████████████████████████████████████████████████████████████████████████████████| 190/190 [00:00
Downloading (…)7e55de9125/README.md: 100%|████████████████████████████████████████████████████████████████████████████| 10.6k/10.6k [00:00
Downloading (…)55de9125/config.json: 100%|████████████████████████████████████████████████████████████████████████████████| 612/612 [00:00
Downloading (…)ce_transformers.json: 100%|█████████████████████████████████████████████████████████████████████████████████| 116/116 [00:00
Downloading (…)125/data_config.json: 100%|█████████████████████████████████████████████████████████████████████████████| 39.3k/39.3k [00:00
Downloading pytorch_model.bin: 100%|██████████████████████████████████████████████████████████████████████████████████| 90.9M/90.9M [00:04
Downloading (…)nce_bert_config.json: 100%|███████████████████████████████████████████████████████████████████████████████| 53.0/53.0 [00:00
Downloading (…)cial_tokens_map.json: 100%|█████████████████████████████████████████████████████████████████████████████████| 112/112 [00:00
Downloading (…)e9125/tokenizer.json: 100%|███████████████████████████████████████████████████████████████████████████████| 466k/466k [00:00
Downloading (…)okenizer_config.json: 100%|█████████████████████████████████████████████████████████████████████████████████| 350/350 [00:00
Downloading (…)9125/train_script.py: 100%|████████████████████████████████████████████████████████████████████████████| 13.2k/13.2k [00:00
Downloading (…)7e55de9125/vocab.txt: 100%|██████████████████████████████████████████████████████████████████████████████| 232k/232k [00:00
Downloading (…)5de9125/modules.json: 100%|████████████████████████████████████████████████████████████████████████████████| 349/349 [00:00
Creating new vectorstore
Loading documents from source_documents
Loading new documents: 100%|██████████████████████| 1/1 [00:00
Loaded 1 new documents from source_documents
Split into 91 chunks of text (max. 500 tokens each)                 
Creating embeddings. May take some minutes...              
Ingestion complete! You can now run privateGPT.py to query your documents
```

### Start you privateGPT

```bash
❯ python3.11 privateGPT.py
Found model file at  models/ggml-gpt4all-j-v1.3-groovy.bin
gptj_model_load: loading model from 'models/ggml-gpt4all-j-v1.3-groovy.bin' - please wait ...
gptj_model_load: n_vocab = 50400
gptj_model_load: n_ctx   = 2048
gptj_model_load: n_embd  = 4096
gptj_model_load: n_head  = 16
gptj_model_load: n_layer = 28
gptj_model_load: n_rot   = 64
gptj_model_load: f16     = 2
gptj_model_load: ggml ctx size = 5401.45 MB
gptj_model_load: kv self size  =  896.00 MB
gptj_model_load: ................................... done
gptj_model_load: model size =  3609.38 MB / num tensors = 285
Enter a query:
```

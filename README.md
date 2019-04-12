# test_repository
pipenvを使ってjupyter notebookで作業できるようにするためのレポジトリです。

#  手順
1. `pip install pipenv`
2. 作業ディレクトリに移動`cd working_dir` 
    - pipenvではディレクトリでは`pipenv　install`で生成されるPipfileがあるディレクトリごとに環境を分けられます。
2. `pipenv install --python 3.6`
3. `pipenv install jupyter jupytext`  
    -  `pipenv install environment-kernels`もやっておくと安全。
4. `pipenv run jupyter notebook --generate-config`でconfigファイルを生成
5. `vim ~/.jupyter/jupyter_notebook_config.py`でconfigファイルを以下のようにいじる  
    ```
    c = get_config()

    c.NotebookApp.ip = 'localhost'

    c.NotebookApp.token = "好きなトークンを設定"

    #ブラウザは立ち上げない
    c.NotebookApp.open_browser = False

    # 特定のポートに指定(デフォルトは8888)
    c.NotebookApp.port = 8888
    ```
6. あとは`pipenv run jupyter notebook`ないしは`pipenv shell`で環境内に入ってあとに`jupyter notebook`を走らせて、ブラウザ上で`http://localhost:8888`にアクセスすれば使えるはず。

7. ライブラリのインストールは`pipenv install hogehoge`で出来る。
    - とりあえずここら辺を入れておけばOK。  
    `pipenv install numpy pandas scipy scikit-learn matplotlib japanize-matplotlib seaborn tqdm`
    - 一度作った環境はPipfileで移動することができる。どこかで作成したPipfileをディレクトリに置いて`pipenv install`を走らせれば、環境が再現できる。


# 参考
- https://qiita.com/anvinon/items/5d9c128ef8b65b866dfe
- https://qiita.com/SUZUKI_Masaya/items/76b927b9812d77d33e57

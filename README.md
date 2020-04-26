# pipenv_jupyter
研究室サーバー上でjupyter notebookを立ち上げ、ローカルPCのブラウザから作業できるようにするためのレポジトリ

#  使い方
1. pipenvが入っていなければ`pip3 install pipenv`で取得
    - deathstarおよびstarkillerには入っている
    - starkillerで実行する場合は下記の[starkillerで使用する際の前準備](#-starkillerで使用する際の前準備)を先に実行して下さい。

2. `git clone https://github.com/GENZITSU/pipenv_jupyter.git`

3. `cd pipenv_jupyter`

4. `pipenv install`で仮想環境を作成

4. `pipenv run jupyter notebook --generate-config`でconfigファイルを生成
5. `vim ~/.jupyter/jupyter_notebook_config.py`でconfigファイルを以下のように変更
    ```
    c = get_config()

    c.NotebookApp.ip = 'localhost'

    c.NotebookApp.token = "好きなトークンを設定"

    #ブラウザは立ち上げない
    c.NotebookApp.open_browser = False

    # 特定のポートに指定(デフォルトは8888だが、他の人と競合するので別の番号に変えること)
    c.NotebookApp.port = 8888
    ```
6. `pipenv run jupyter notebook`(または`pipenv shell`で環境内に入ってあとに`jupyter notebook`を走らせて)ローカルPCのブラウザ上で`http://localhost:8888`にアクセス
    - アクセスが拒否される時はローカルPCの`.ssh/config`内のdeathstarのところに`LocalForward 8888 127.0.0.1:8888`を追加してみて下さい。

# 備考
1. もし上記手順で動かなかった場合は、以下のライブラリを追加でダウンロードしてみて下さい。
    - `pipenv install jupyter jupytext environment-kernels`
2. ライブラリの追加インストールは`pipenv install hogehoge`で出来ます。また、すでに入っているライブラリは`Pipfile`の中の[packages]で確認できます。
    - pipenvを用いた仮想環境作成では`Pipfile`が存在するディレクトリごとに環境を分けられるので、プロジェクト毎にディレクトリ分けて`Pipfile`を作成しておくのがお勧め。


# starkillerで使用する際の前準備
pipenvが入っているpyenvを使用するように変更する
- pyenvのインストール
    - `git clone https://github.com/yyuu/pyenv.git ~/.pyenv`
    - `pyenv install 3.6.9`
    - `pyenv rehash`
    - `pyenv global 3.6.9`
- ホームディレクトリに以下の`.bash_profile`を作成
    ```
    export PYENV_ROOT=$HOME/.pyenv
    export PATH=$HOME/.local/lib/python3.6/site-packages:$HOME/.local/bin:$PYENV_ROOT/bin:$PATH
    export PYENV_VERSION=3.6.9
    eval "$(pyenv init -)"
    ```
- `source ~/.bash_profile`
# 参考
- https://qiita.com/anvinon/items/5d9c128ef8b65b866dfe
- https://qiita.com/SUZUKI_Masaya/items/76b927b9812d77d33e57
- https://da-smlab.slack.com/archives/C04GQE1C5/p1587716978065100?thread_ts=1586439777.046500&cid=C04GQE1C5
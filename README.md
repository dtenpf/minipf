# Install

- [For Windows]Windows10以降はDocker for windows、Windows7以前の場合はDocker Toolboxを入れて下さい。全てのcheckboxにcheckを入れてinstallしてください。(64bitのみ)

  - https://www.docker.com/products/docker-toolbox
  - https://www.docker.com/docker-windows

- [For Linux]パッケージ管理を使っていれてください。下記はubuntuの例です。
~~~
sudo apt-get install docker.io
~~~

# For Proxy
- Proxy経由でのアクセスが必要な場合、HOST環境/Docker Boot部/Docker内の三箇所で設定が必要です。
   - http://qiita.com/tora470/items/cd9335f5ce638e11bb97

# Directories

- base_env
  - 管理者用
  - ビルドに必要なパッケージ群のDockerfile
- public_env
  - 一般開発者向け
  - 環境構築方法はREADME.mdを見てください。

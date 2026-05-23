# Environment Setup

# Podman セットアップ手順

この授業では、コンテナ実行環境として Podman を使います。授業前に、各自の PC に Podman をインストールしておいてください。

## Windows の場合

PowerShell を開き、次のコマンドを実行してください。

```
winget install RedHat.Podman-Desktop
```

インストールが終わったら、Podman Desktop を起動してください。初回起動時にセットアップ画面が表示された場合は、画面の指示に従って進めてください。

その後、PowerShell で次のコマンドを実行して確認します。

```
podman run --rm docker.io/library/hello-world
```

メッセージが表示されれば完了です。

## macOS の場合

ターミナルを開き、Homebrew が入っているか確認してください。

```
brew --version
```

Homebrew が入っていない場合は、次のコマンドでインストールしてください。

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Homebrew が使える状態になったら、次のコマンドで Podman をインストールします。

```
brew install podman
```

続いて、Podman を起動できるようにします。

```
podman machine init
podman machine start
```

最後に、次のコマンドで確認します。

```
podman run --rm docker.io/library/hello-world
```

メッセージが表示されれば完了です。


# Pintos 開発環境のセットアップ

この授業では、Pintos のビルドと実行に Podman を使います。Pintos では 32-bit x86 用のコンパイラや QEMU などが必要ですが、それらは授業用のコンテナイメージに入っています。

## 1. Podman を起動しておく

Windows の場合は、Podman Desktop を起動してください。

macOS の場合は、ターミナルで次を実行してください。

```
podman machine start
````

すでに起動している場合は、そのままで構いません。

## 2. 授業用イメージを取得する

次のコマンドを実行してください。

```text
podman pull docker.io/rui314/pintos:2026-course
```

初回はイメージのダウンロードに時間がかかります。

## 3. Pintos のソースコードを取得する

作業したいディレクトリで、次のコマンドを実行してください。

```
git clone https://github.com/ut-syspro-2026/pintos
```

これにより、手元の PC に `pintos` というディレクトリが作成されます。

## 4. Pintos ディレクトリをコンテナにマウントして起動する

`pintos` ディレクトリの一つ上のディレクトリで、次のコマンドを実行してください。

macOS の場合:

```
podman run -it --rm --name pintos -v "$(pwd)/pintos:/home/PKUOS/pintos" docker.io/rui314/pintos:2026-course bash
```

Windows PowerShell の場合:

```
podman run -it --rm --name pintos -v "${PWD}\pintos:/home/PKUOS/pintos" docker.io/rui314/pintos:2026-course bash
```

このコマンドを実行すると、コンテナ内のシェルに入ります。

コンテナ内の `/home/PKUOS/pintos` は、手元の PC 上の `pintos` ディレクトリと共有されています。手元の PC でファイルを編集すると、コンテナ内からも同じ変更が見えます。

## 5. 同じコンテナで別のシェルを開く

Pintos のデバッグ中など、同じコンテナ内で2つ目のシェルを開きたいことがあります。例えば、一方のシェルで Pintos を起動し、もう一方のシェルで `gdb` を実行したい場合です。

まず、手元の PC の別のターミナルまたは PowerShell を開き、起動中のコンテナを確認します。

```
podman ps
```

次のように、`pintos` という名前のコンテナが表示されます。

```text
CONTAINER ID  IMAGE                                COMMAND  CREATED        STATUS        PORTS  NAMES
123456789abc  docker.io/rui314/pintos:2026-course  bash     2 minutes ago  Up 2 minutes         pintos
```

このコンテナに対して、次のコマンドを実行すると、同じコンテナ内で新しいシェルを開けます。

```
podman exec -it pintos bash
```

これで、最初に開いたシェルと同じコンテナの中に、2つ目のシェルが開きます。どちらのシェルからも `/home/PKUOS/pintos` に同じファイルが見えます。

## 6. Pintos をビルドして起動する

コンテナ内で、次のコマンドを順に実行してください。

```text
cd /home/PKUOS/pintos/src/threads
make
cd build
pintos --
```

次のような出力が表示されれば成功です。

```text
Pintos hda1
Loading............
Kernel command line:
Pintos booting with 3,968 kB RAM...
Boot complete.
```

Pintos や QEMU を終了するには、`Ctrl+a` を押してから `x` を押してください。うまくいかない場合は `Ctrl+c` でも終了できます。

## 7. コンテナを終了する

コンテナ内の作業を終えるには、次のコマンドを実行してください。

```
exit
```

または `Ctrl+d` を押してください。

### What's the magic?

Now Let's conclude what you have done.

* First, You used docker to run a Ubuntu container that functions as a full-edged Linux OS inside your host OS.
* Then you used Qemu to simulate a 32-bit x86 computer inside your container.
* Finally, you boot a tiny toy OS -- Pintos on the computer which Qemu simulates.

Wow, _**virtualization is amazing**_, right?

Throughout this semester, **you can modify your Pintos source code in your host machine with your favorite IDE but compile/run/debug/test your Pintos in the container thanks to the mounting technique**. You can leave the container running when you are modifying Pintos source code in you host computer, because your modification will be visible in the container immediately.

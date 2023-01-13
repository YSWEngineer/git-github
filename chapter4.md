# Chapter 4 GitHubのリポジトリをパソコンに取得しよう

今までの章では個人作業がメインでしたが、ここからは複数人での共同作業について手を動かしながら学んでいきます。

Gitのみならず、GitHubの使い方についても触れていくので、気持ちを切り替えて臨みましょう。

<details><summary>Lesson 23 [Git Hubの登録] GitHubを使う準備をしましょう</summary>

今までの章では個人作業がメインでしたが、ここからは複数人での共同作業について手を動かしながら学んでいきます。Gitのみならず、GitHubの使い方についても触れていくので、気持ちを切り替えて臨みましょう。

- Lesson 23 [Git Hubの登録] GitHubを使う準備をしましょう
    
    これ以降、最終章まで、Gitと並んで本書が大きなテーマとしているGitHubというWebサービスを扱います。このLessonではその準備として、GitHubがどんなものかを理解してください。その後、実際に使っていくため、アカウントの作成を行いましょう。
    
    - GitHubとは何かを知ろう
        
        GitHub( [https://github.com](https://github.com) )は、多くの開発者に親しまれるWebサービスの名称です。Gitのリポジトリを作成してソースコードをホスティングすることができ、インターネットに接続可能な環境であればどこにいても開発作業を行えます。また、複数人での共同作業がしやすいような機能を備えていることも大きな特徴です。こうした特徴は、これ以降のChapterで十分に体感できると思いますので、楽しみにしていてくださいね。リポジトリは「プライベート」という設定(アクセスを許可した特定のユーザーのみが使用できる状態)にしない限り、誰にでも閲覧できる状態(パブリック)でGitHub上で公開されます。個人が趣味で作ったものから世界的な大企業が公開しているものまで、さまざまなリポジトリにアクセスすることができるので、ぜひいろいろと見てみてください。尚、有料プランでないと一部機能に制限がかかりますが、ほとんどの機能は無料で十分使うことができます。
        
        ※GitHubを使えば最小限の手間でリモートリポジトリを用意できます。
        
    - アカウントを作成し、GitHubユーザーになろう
        
        本書では、これ以降皆さんにも手を動かしていただきながらGitHubの活用方法を学習していきます。そのための第一歩として、GitHubのアカウントを作成しましょう。
        
        1. アカウント作成を開始する
            1. GitHub( [https://github.com](https://github.com) )にアクセスし、アカウントの作成を始めます。
                        
        2. アカウントに必要な情報を設定する
            1. 使用したいユーザー名、メールアドレス、パスワードを入力します。これらの情報は、今後GitHubへログインする際に必要となるので、紛失しないようにしましょう。
            - **Point** アカウント登録の注意点
                
                ユーザー名は好きなものを設定できますが、既にGitHubを使っている他のユーザーと同じものを使うことはできません。もし他のユーザーと重複した場合は入力欄の下に「Username XXX is not available.」というメッセージが表示されるので、別の値を入力しましょう。メールアドレスは、Chapter 2でGitの設定を行なった際に指定したものと同じにしてください。また、パスワードは短すぎたり簡単に予測されたりしないような、安全なものを設定しましょう。
                
        3. メールアドレスを確認する
            1. 入力したメールアドレスに、アカウント確認用のパスコードが送られます。パスコードを入力して認証を完了させましょう。
        4. GitHubの用途などの情報を入力する
            1. 皆さん自身のことについていくつか質問されます。このステップは必須ではありません。飛ばしたい場合はページ下部の[skip personalization]とクリックすると、入力を行わずにアカウントの作成を続行します。
        5. プランを選択し、アカウント作成を完了する
            1. 無料か有料か、プランを決めます。有料にしたい明確な理由がない限り、無料プランを選択しておきましょう。後で必要になってから有料プランに変更することもできます。
            
            ※アカウント作成直後はログインした状態となっています。ログアウトした場合は、GitHubのページ右上に表示されている[Sign in]をクリックし、ユーザー名とパスワードを入力して再ログインしましょう。</details>


<details><summary>Lesson 24 [Git Hubの利用準備] GitHubに公開鍵を設定しましょう</summary>

GitHubに対して操作を行う際、認証が必要になることがあります。このLessonでは、SSHというプロトコルを用いて認証するための設定を行います。慣れない操作もあるかもしれませんが、間違えないよう注意しましょう。

- Gitを使ってGitHubと認証する方法は2つある
    
    手元のパソコンとGitHubとで通信してデータをやり取りするには、認証という手続きが必要となります。現在、GitHubで使用できる認証方式は2つあり、1つは、HTTPSというプロトコルとパーソナルアクセストークン(P.128)を用いたユーザー認証です。もう1つはSSHというプロトコルと公開鍵を用いたサーバー認証です。本書ではこちらを採用します。いずれの方法も最初にコマンドラインやブラウザ上での設定が必要です。SSHを使う場合、最初の設定以降はコマンドライン上で認証のためにユーザー名やパーソナルアクセストークンなどを入力する必要がなく、GitHubに接続する際の手順が軽減できます。
    
    - 通信プロトコルと認証
        
        
        | 通信プロトコル | 認証方法 |
        | --- | --- |
        | SSH | 公開鍵 |
        | HTTPS | ユーザー名とパスワード |
    - 公開鍵による認証方式
        1. ペアの秘密鍵と公開鍵を作成
        2. 公開鍵をGitHubに登録
        3. 鍵を用いて暗号化通信を行う
        
        ※「SSH」や「公開鍵」の仕組みが分からなくても使うことはできますが、仕組みも理解できた方が望ましいので、時間のある時に調べてみてくださいね。
        
- SSH Keyを作成する
    1. SSH Keyを作成する ※事前にGitHubにログインしておくこと。
        1. 以下のコマンドを実行して、鍵(SSH Key)を作成します。”ichiyasa-g-2@example.com”の部分は自分のメールアドレスに置き換えてください。
        
        ```bash
        $ ssh-keygen -t ed25519 -C "emailaddress"
        
        ichiyasa % ssh-keygen -t ed25519 -C "emailaddress"
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/Users/yoshiwo/.ssh/id_ed25519):
        ```
        
    2. 鍵の保存場所を確認する
        1. 「Enter file in which to save tha key」と表示されたら、returnキーを押してください。この時に表示される絶対パスは、生成した鍵の保存先です。
        
        ```bash
        ichiyasa % ssh-keygen -t ed25519 -C "emailaddress"
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/Users/yoshiwo/.ssh/id_ed25519): #ここでreturnキーを押す
        
        ichiyasa % ssh-keygen -t ed25519 -C "emailaddress"
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/Users/yoshiwo/.ssh/id_ed25519): 
        Enter passphrase (empty for no passphrase):
        ```
        
    3. パスフレーズを入力する
        1. 続いて「Enter passphrase」表示されるので、パスフレーズ(パスワードのことだと思ってください。SSH Keyの管理に必要です)を入力します。GitHubのパスワードとは別の、今生成するSSH Key専用のパスフレーズを設定してください。尚、確認用に2度入力が必要です。
        
        ```bash
        ichiyasa % ssh-keygen -t ed25519 -C "emailaddress"
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/Users/yoshiwo/.ssh/id_ed25519): 
        Enter passphrase (empty for no passphrase): # ここでパスフレーズを2回入力する
        
        ichiyasa % ssh-keygen -t ed25519 -C "yosiwo.may15@gmail.com"
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/Users/yoshiwo/.ssh/id_ed25519): 
        Enter passphrase (empty for no passphrase): 
        Enter same passphrase again:　# 1回目入力後の表示、パスフレーズは入力しても画面に表示されない
        
        ichiyasa % ssh-keygen -t ed25519 -C "yosiwo.may15@gmail.com"
        Generating public/private ed25519 key pair.
        Enter file in which to save the key (/Users/yoshiwo/.ssh/id_ed25519): 
        Enter passphrase (empty for no passphrase): 
        Enter same passphrase again: # 2回目入力後の表示が以下の文字列になる
        Your identification has been saved in /Users/yoshiwo/.ssh/id_ed25519. # あなたのIDは/Users/yoshiwo/.ssh/id_ed25519に保存されています。
        Your public key has been saved in /Users/yoshiwo/.ssh/id_ed25519.pub. # 公開鍵は /Users/yoshiwo/.ssh/id_ed25519.pub に保存されています。
        The key fingerprint is: # 鍵のフィンガープリントは次のとおりです:
        SHA256:AXOJQ+NPNV7t/PGHWihrKX8DE2IhdpSLERAuegDQVOo yosiwo.may15@gmail.com
        The key's randomart image is:
        +--[ED25519 256]--+
        |+o..++*+ooo ..   |
        |. .o .*==o o  .  |
        |. o ...*oo.  o   |
        | + .  .o+..   o. |
        |. E    .S. . . oo|
        | .        + . o +|
        |           * o  .|
        |        . + +    |
        |         +.. .   |
        +----[SHA256]-----+
        ```
        
- SSH KeyをGitHubに登録しよう
    1. 公開鍵をクリップボードにコピーする
        1. 生成した公開鍵をGitHubの設定画面に登録するために、次のコマンドを実行してクリップボード(command + C と同じアクションを行う)にコピーします。WindowsとmacOSでコマンドが異なります。
        - macOSの場合
            
            ```bash
            $ pbcopy < /Users/ichiyasa/.ssh/id_ed25519.pub
            
            ichiyasa % pbcopy < /Users/yoshiwo/.ssh/id_ed25519.pub # 入力してreturnキーを押す
            # Usersの後ろはyoshiwo
            ```
            
    2. GitHubの設定画面を表示する
        1. GitHubのSettingsを開きます。左側のメニューより[SSH and GPG Keys]を選択した後、[New SSH Key]をクリックします。
            1. アイコンをクリック
            2. [Settings]を選択
            3. 左側の列にある[SSH and GPG keys]を選択
            4. SSH keysの行にある、[New SSH key]をクリック
    3. 公開鍵を貼り付ける
        1. [Title]を入力し、[Key]のフィールドに公開鍵をペーストします。[Title]の内容は自由ですが、あとで見た時にどのパソコンで発行したキーなのかわかる情報を入力しておくのがオススメです。入力が完了したら、[Add SSH key]をクリックしましょう。
            1. [Title]にタイトルを入力
            2. 公開鍵をペースト $ pbcopy < /Users/ichiyasa/.ssh/id_ed25519.pubでコピーした内容をそのままペーストすればよい。※コピー後はペーストするまで他のものをコピーしないこと。
            3. [Add SSH key]をクリック
- 正しく設定できたことを確認しよう
    1. 確認用のコマンドを入力する
        1. 鍵の設定がうまくいったことを確認するため、次のコマンドを実行してください。「Are you sure you want to continue connecting (yes/no)?」と問われたら「yes」と入力します。
        
        ```bash
        $ ssh -T git@github.com
        
        ichiyasa % ssh -T git@github.com
        The authenticity of host 'github.com (20.27.177.113)' can't be established.
        ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
        Are you sure you want to continue connecting (yes/no/[fingerprint])? yes # 「yes」と入力してreturnを押す
        ```
        
    2. パスフレーズを入力する
        1. 続いて先程設定したパスフレーズを入力してください。「Hi ユーザー名! You’ve successfully authenticated」と表示されたら設定は成功です。
        
        ```bash
        ichiyasa % ssh -T git@github.com
        The authenticity of host 'github.com (20.27.177.113)' can't be established.
        ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
        Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
        Warning: Permanently added 'github.com,20.27.177.113' (ECDSA) to the list of known hosts.
        Enter passphrase for key '/Users/yoshiwo/.ssh/id_ed25519': # ここでパスフレーズを入力してreturnを押す
        
        Enter passphrase for key '/Users/yoshiwo/.ssh/id_ed25519': 
        Hi YSWEngineer! You've successfully authenticated, but GitHub does not provide shell access.
        # 設定は成功した
        ```
        
        ※「Permission denied」と表示されたら失敗です。手順をやり直してください。また、これ以降ターミナルでの操作中にパスフレーズを聞かれたら、この値を入力しましょう。GitHubのパスワードと混同しやすいですが、ターミナルでパスワードを入力する機会はありません。必ずパスフレーズを使うと覚えておきましょう。
        
- **ワンポイント** Settingsメニューでさまざまな設定ができる
    
    今回は公開鍵の設定を紹介しましたが、Settingsメニューでできることは他にもあります。例えば、プロフィールの設定をして自分がどんな人物なのか伝えたり、メールで通知を受ける内容をカスタマイズしたり、いろいろと自分好みの設定が可能です。また、2段階認証を有効化するといった、安全にサービスを使うための機能も備わっています。
### 用語

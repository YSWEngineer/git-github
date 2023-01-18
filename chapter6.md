# Chapter 6 複数ブランチを同時に使ってファイルを更新しよう

ブランチ利用の応用編です。トピックブランチを2つ作成し、並行作業をしてみましょう。

作業行程は複雑になりますが、「なぜ今このコマンドを実行するのか」と常に考えながら、順を追って理解してください。

<details><summary>Lesson 36 [シナリオの解説] 複数ブランチを使うためのシナリオを理解しましょう</summary>
    
このChapterはすでにみなさんが知っている機能のみを使って進めていくため、すぐ実践に入ります。先ずはこのLessonでこれから実施する作業の内容を説明しますので、Chapter 5で学んだ操作も思い出しながらシナリオを把握してください。
    
- 1つ目のブランチを用いスピーカー情報を更新する
        
  イベントで登壇するうスピーカーが決まったため、イチヤサさんは専用のブランチを作成してイベントページにスピーカーのプロフィール文とプロフィール画像を追加します。尚、サンプルとして登場するスピーカーは「いろふさん」と「うらがみさん」です。

  しかし、いろふさんのプロフィール画像がまだ手に入っていないものとします。そこで、いろふさんの画像追加はTODOコメント(P.191参照)を残すのみで後回しとし、スピーカー情報の更新を中断します。

- 2つ目のブランチでセッション情報を更新する
        
  スピーカー情報の更新は途中のままにし、セッション情報を更新します。但し、作業の目的や内容が異なるため、使用するのはスピーカー情報用と別のブランチです。セッションの情報の更新は作業を完了させ、masterブランチへのマージまで行います。

- 1つ目のブランチに戻り、スピーカー情報の更新を終える
        
  セッション情報の更新中に、いろふさんのプロフィール画像が手に入ったとします。先ずは2つ目のブランチで加えた変更を1つ目のブランチにも反映させましょう。その後、1つ目のブランチで画像の追加とTODOコメントの削除を行い、コミットとマージを実行します。</details>


<details><summary>Lesson 37 [複数ブランチの使用1] 専用のブランチでスピーカーの情報を更新しましょう</summary>

イベントページに、スピーカーのプロフィール文とプロフィール画像を追加します。すでに作業手順は頭に入っているでしょうか。このLessonではこれまでと少し違う操作を紹介するので、自分に合った方法を見つけてください。
- スピーカー情報を途中まで更新する
    
    Lesson 36で説明したように、今回はspeakers-infoブランチを作成し、スピーカー情報を途中まで追加していきます。使うコマンドもほぼこれまでに説明したものばかりですが、オプションを利用してコマンド数を減らすやり方を説明します。
    
    ※オプションを使って少ないコマンドで目的を達成します。

    - チェックアウトと同時にブランチを作成するコマンド
        
        ```bash
        $ git checkout -b speakers-info
        # git checkout = git checkoutコマンド
        # -b = -bオプション
        # speakers-info = 作成し、切り替えたいブランチ名
        ```
        
    - 変更したファイルをまとめてステージングエリアに追加するコマンド
        
        ```bash
        $ git add -A
        # git add = git addコマンド
        # -A = -Aオプション
        ```
        
- ブランチを作成し、コミットしよう
    1. ブランチを作成し、チェックアウトする
        1. git branchコマンドでブランチを作成し、新しいブランチに切り替えるまでを1コマンドで行ってみましょう。git checkoutコマンドに-bオプションをつけて実行します。ブランチ名はspeakers-infoとします。
        
        ```bash
        $ git checkout -b speakers-info
        
        # git checkoutコマンドでspeakers-infoという名のブランチを作成し、同時にチェックアウトを行う
        % git checkout -b speakers-info
        Switched to a new branch 'speakers-info' # 新しいブランチ「speakers-info」ブランチに切り替わった
        ```
        
        ※打ち間違いなどにより誤ったブランチを作成してしまったら、もう一度masterブランチをチェックアウトした後、改めて正しいコマンドを実行してください。
        
    2. HTMLを更新する
        1. 今回は、HTML(プロフィール文)と画像(プロフィール画像)の更新が必要です。Chapter 3のコラムで紹介したように、Gitではテキストファイルのみでなく、画像のようなバイナリファイルも管理できることを思い出してください。まず、HTMLについては「スピーカー」の欄にプロフィール文を追記します。スピーカー2名分のサンプルを載せるので、みなさんも入力してみてください。
    3. TODOコメントを追加する
        1. 画像は、「images」フォルダーに追加する必要があります。しかし、いろふさんのプロフィール画像がまだ入手できていません。TODOコメントを残し、後から差し替えるものとして仮置きの画像を使っておきます。
        - **Point** あとでやりたい作業を書く「TODOコメント」
            
            プログラミングをしていると、あとでやりたい(やる必要がある)作業に備忘録としてソースコードコメントを付けることがしばしばあります。これを、TODOコメントと呼びます。今回のサンプルでは、いろふさんのプロフィール画像追加があとでやるべき作業として残るため、画像の追加箇所にTODOコメントを書いておきます。HTMLの場合は<!-- -->の間にTODOコメントを書きますが、他の言語を使用する場合はそれぞれの文法でTODOコメントを書いてください。
            
    4. 画像を用意する
        1. 画像を2枚用意します。内容は何でもいいので、みなさんのお好きな画像を使っても構いません。但し、画像ファイル名はHTMLで指定したとおり、それぞれspeaker1.png、speaker2.pngとしてください。サンプルプロジェクトへ画像を追加するには、Visual Studio Code左側のエクスぷローターに表示されている「images」フォルダーに画像をドラッグアンドドロップします。
        
        ※ファイル名さえあっていれば、画像は何でも構いません。
        
    5. ブラウザーでHTMLを確認する
        1. Gitに登録する前に、HTMLが正しく更新されたかをブラウザーで確認しておきましょう。

    6. 編集したファイルをコミットする
        1. ファイルの状態をチェックしたら、コミットしましょう。ここではgit addコマンドに-Aオプションを付け、新規追加・編集・削除したすべてのファイルを一度にステージングエリアへ追加します。そのあとは、これまでどおりコミットをすれば大丈夫です。
        
        ```bash
        $ git status # 現在の状態を確認する
        
        % git status
        On branch speakers-info
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   index.html
        
        Untracked files:
          (use "git add <file>..." to include in what will be committed)
        	images/speaker1.png
        	images/speaker2.png
        
        no changes added to commit (use "git add" and/or "git commit -a")
        ```

        ```bash
        $ git add -A # -Aは--allとも書ける
        ```
        
        ※-Aは--allとも書けます。文字数は多いですが、意味がわかりやすいですね。このように、オプションにはわかりやすい書き方と短い省略形が存在することがあります。これは、Git以外のコマンドにも言える特徴です。
        
        ```bash
        $ git status
        
        % git status
        On branch speakers-info
        Changes to be committed:
          (use "git restore --staged <file>..." to unstage)
        	new file:   images/speaker1.png
        	new file:   images/speaker2.png
        	modified:   index.html
        ```

        ```bash
        $ git commit -m "スピーカー情報を追記した"
        
        % git commit -m "スピーカー情報を追記した"
        [speakers-info f5e118d] スピーカー情報を追記した
         3 files changed, 8 insertions(+), 4 deletions(-)
         create mode 100644 images/speaker1.png
         create mode 100644 images/speaker2.png
        ```

    7. リモートリポジトリにプッシュする
        1. スピーカー情報の更新が未完なので、speakers-infoブランチはまだ役目を終えていませんが、プッシュしておきましょう。プルリクエストの作成やリリースなど、リモートリポジトリでの操作を行いたいときに限らず、プッシュはこまめに行うことをオススメします。
        
        ```bash
        $ git push origin speakers-info
        
        % git push origin speakers-info
        Enter passphrase for key '/Users/yoshiwo/.ssh/id_ed25519': 
        Enumerating objects: 9, done.
        Counting objects: 100% (9/9), done.
        Delta compression using up to 8 threads
        Compressing objects: 100% (6/6), done.
        Writing objects: 100% (6/6), 29.90 KiB | 7.47 MiB/s, done.
        Total 6 (delta 2), reused 0 (delta 0), pack-reused 0
        remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
        remote: 
        remote: Create a pull request for 'speakers-info' on GitHub by visiting:
        remote:      https://github.com/YSWEngineer/ichiyasaGitSample/pull/new/speakers-info
        remote: 
        To github.com:YSWEngineer/ichiyasaGitSample.git
         * [new branch]      speakers-info -> speakers-info
        ```

        ※こまめにプッシュしておけば、何らかの不具合でローカルリポジトリのデータが消えて作業内容が失われることを防いだり、他のパソコンでプルして作業したりすることができます。
### 用語
- **git checkoutコマンド**：操作対象となるブランチを指定するコマンド。このコマンドを実行すると、それ以降の操作対象が切り替わり、指定したブランチが使われるようになる。
- **TODOコメント**：あとでやりたい(やる必要がある)作業に備忘録としてソースコードコメントを付けること。
- **ステージングエリア**：コミットするファイルを登録する場所。
- **git status**：現在の状態を確認する。
- **-Aオプション**：-Aは--allとも書ける。
    - オプションにはわかりやすい書き方と短くした省略形が存在する。これはGit以外のコマンドにもいえる特徴。
- **リモートリポジトリ**：インターネット上に存在するリポジトリのこと。複数人で共有するものとして、サーバー上に配備するのが一般的。
- **プッシュ**：ローカルリポジトリからリモートリポジトリに反映すること。
- **ブランチ**：Gitで記録する履歴を枝分かれさせるための機能。複数の作業を並行して進めるときに使用する。
- **pull request(プルリクエスト)**：マージの依頼のこと。GitHubが提供している機能の一つ。作成したブランチの取り込みを依頼する際に用いる。
- **プル**：リモートリポジトリの内容をローカルリポジトリに取得し、ワークツリーに反映すること。
    - **git pull**：リモートリポジトリ内のブランチの内容が、ローカルリポジトリ内の同じ名前のブランチに反映されます。同時にワークツリーへの反映も行われます。</details>


<details><summary>Lesson 38 [複数ブランチの使用2] さらにブランチを作成し、セッションの情報を更新しましょう</summary>

いろふさんのプロフィール画像が手元にないままので、一旦中断してセッション情報の更新に移ります。ここからは、同時に複数のブランチを操作することを学びます。ブランチの使い分けを意識してみましょう。
- 新たなブランチをmasterブランチから作成する
    
    次にセッション情報(タイムテーブル)を更新しましょう。別の作業になるので、最初にセッション情報専用のsessions-infoブランチを作成します。現在使っているのは、先ほど作ったspeakers-infoブランチです。その状態でブランチを作成するコマンドを実行すると、基本的には現在使用中のブランチから新たなブランチが作られます。セッション情報の更新はスピーカー情報の更新とは全く別の作業なので、一度masterブランチに戻って、そこから別のブランチを作成しましょう。
    
    - masterブランチに切り替えずに新たなブランチを作成すると……

        ※ベースブランチをmasterにしないと、speakers-infoブランチで追加したコミットも含まれたブランチが作成されてしまいます。そのため、作業ごとに使い分けができません。
    
- ブランチを作成し、編集後にマージまで進めよう
    1. 新たなブランチをmasterブランチから作成する
        1. 一旦masterブランチに移動してから、sessions-infoという名前のブランチを作成します。
        
        ```bash
        $ git checkout master # masterブランチに移動する
        
        % git checkout master
        Switched to branch 'master'
        Your branch is up to date with 'origin/master'.
        ```
        
        ```bash
        $ git checkout -b sessions-info # sessions-infoブランチを作成して、チェックアウトする
        
        % git checkout -b sessions-info
        Switched to a new branch 'sessions-info'
        ```

    2. ファイルを編集し、マージまで進める
        1. index.htmlファイルを開き、テキストのように、セッション情報を追記します。
    3. ブラウザーでHTMLを確認する

    4. 変更をコミットする
        1. これまでと同じく、index.htmlをステージングエリアに追加し、コミットします。
        
        ```bash
        $ git status
        
        % git status
        On branch sessions-info
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   index.html
        
        no changes added to commit (use "git add" and/or "git commit -a")
        ```
        
        ```bash
        $ git add index.html
        
        % git add index.html
        ```
        
        ```bash
        $ git commit -m "セッション情報を記載した"
        
        % git commit -m "セッション情報を記載した"
        [sessions-info 858f97a] セッション情報を記載した
         1 file changed, 2 insertions(+), 2 deletions(-)
        ```

    5. リモートリポジトリにプッシュして、マージする
        1. あとは、Chapter5と同様にリモートリポジトリにプッシュし、プルリクエスト使ってマージを行ってください。ここではぷるリクエスト作成前に実行するコマンドのみ列挙し、詳細は割愛します。
        
        ```bash
        $ git push origin sessions-info
        
        % git push origin sessions-info # リモートリポジトリにプッシュする
        Enter passphrase for key '/Users/yoshiwo/.ssh/id_ed25519': # パスフレーズを要求されるので入力する
        Enumerating objects: 5, done.
        Counting objects: 100% (5/5), done.
        Delta compression using up to 8 threads
        Compressing objects: 100% (3/3), done.
        Writing objects: 100% (3/3), 428 bytes | 428.00 KiB/s, done.
        Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
        remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
        remote: 
        remote: Create a pull request for 'sessions-info' on GitHub by visiting:
        remote:      https://github.com/YSWEngineer/ichiyasaGitSample/pull/new/sessions-info
        remote: 
        To github.com:YSWEngineer/ichiyasaGitSample.git
         * [new branch]      sessions-info -> sessions-info
        ```

- **プルリクエストを作成→マージするまでの流れ：1~5はプルリクエスト作成の手順、6•7はマージを実行する手順、8•9はマージコミットの確認**
    1. プルリクエストを作成する
        1. ブランチをプッシュ(ローカルリポジトリからリモートリポジトリに反映すること)する。
        
        ```bash
        $ git push origin ブランチ名
        ```
        
    2. masterブランチへのプルリクエスト作成を開始する
        1. プッシュ後、GitHubのリポジトリを開くと新たに黄色いエリアが表示され、更新されたブランチがあることを確認できます。エリア右側の[Compare & pull request]をクリックする。
            1. 黄色いエリアがない場合は、**プルリクエストは専用画面から作成することもできる**ので、
                
                ①[Pull requests]タブをクリック
                
                ②[New pull request]をクリック
                
                ③base:とcompare:のブランチを選択
                
                ④[Create pull request]をクリック
                
    3. ベースブランチとトピックブランチを選択する
        1. 左側の[base repository:]を自分のアカウントのリポジトリを選択する。
        2. 自分のアカウントのリポジトリのページに遷移するので、
        3. 自分のアカウントのリポジトリのbase:masterとcompare:を選択する。
    4. プルリクエストに必要な情報を入力する
        1. コメント欄にどのような変更を加えたのか、わかりやすく書くこと。
    5. プルリクエストの内容を確定する
        1. [Create pull request]をクリックして、プルリクエストの作成が完了する。
    6. (プルリクエストを作成したので、マージを行う)3つのマージ方法から選択する
        1. [Merge pull request]の▼をクリック。
        2. [Create a merge commit]を選択。
    7. マージを実行する
        1. 3つのマージ方法を選択したら、[Merge pull request]をクリックする。
    8. マージコミットのコメントを入力する
        1. マージコミットのコメントを確認 ※デフォルト値のままで良い。
        2. [Confirm merge]をクリック。
        3. プルリクエストがマージされると、「Pull request successfully merged and closed」と表示される。
    9. ベースブランチのコミット履歴を確認する
        1. [Code]タブに移動する。
        2. [(コミット数) commits]をクリック。
        3. コミット履歴が表示されるので、マージコミットを確認する。
- Lesson 39 [複数ブランチの使用3] スピーカー情報更新用ブランチに戻り、作業を再開しましょう

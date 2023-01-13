# Chapter 3 ファイルをバージョン管理してみよう
準備がすべて終わったので、いよいよ本格的にGitの操作をしていきます。ローカルリポジトリを作って、実際にコミットの作成までやってみましょう。

<details><summary>Lesson 14 [Gitコマンドの概要] ローカルリポジトリでの操作を知りましょう</summary>

このChapter全体を通して、ローカルリポジトリに対する操作を学んでいきます。覚えなければいけないことは多いですが、これを覚えれば自分専用のローカルリポジトリでバージョン管理をするために必要なGitの知識を身に付けられます。

- ローカルリポジトリでの操作を知ろう
    
    Gitを実際に使い始める前に、このChapterで何を学ぶのかを整理しておきましょう。
    
    たくさんあるように感じますが、使用頻度が高くて最低限覚える必要があるのはステージングエリアへの登録(git add)とコミットの作成(git commit)を行うコマンドです。その他に、現在の状態を確認するコマンド(git status)もよく使います。少しずつ使えるコマンドを増やしていきましょう。
    
- このChapterで使用するコマンド
    1. リポジトリの作成
        1. git init…………ローカルリポジトリを作成する
    2. コミットの作成
        1. git add…………ステージングエリアに変更を登録する
        2. git commit……コミットを作成する
        3. git rm……………Git管理下のファイルやディレクトリを削除する
    3. 状態の復元
        1. git checkout…ワークツリーの変更を取り消す
        2. git reset………ステージングエリアに追加した変更をワークツリーへ戻す
    4. 状態の確認
        1. git status……ローカルリポジトリの状態を確認する
        2. git diff…………各エリアの差分を確認する
        3. git log…………コミットの履歴を確認する
- ローカルリポジトリを作成する
    
    git initコマンドを実行すると、そのディレクトリにローカルリポジトリが作られます。
    
    この作業だけでGitでバージョン管理をするための準備は完了し、ディレクトリに配置したファイルはuntracked(追跡されていないファイルを表す。まだ一度もコミットされておらず、Gitの管理下にない)という状態になります。ファイルはすべてワークツリーに配置されてしまうので、Gitで管理したくないファイルは.gitignoreファイルを作成して、ファイルを指定します。
    
- コミットするためのコマンド
    
    ワークツリーに配置されたファイルは、git addコマンドでステージングエリアに登録し、git commitコマンドでコミットします。
    
    それぞれのエリアの状況がわからなくなったときは、git statusコマンドやgit diffコマンド、git logコマンドなどで状態を確認できます。
### 用語
- **git add**：ステージングエリアへの登録を行う。
- **ステージングエリア**：コミットするファイルを登録する場所。
- **git commit**：コミットの作成。
- **git status**：現在の状態を確認する。
- **git init**：ローカルリポジトリを作成する。
- **.gitignore**：Gitで管理したくないファイルを.gitignoreファイルを作成してファイルを指定する。
- **git diff**：各エリアの差分を確認する。
- **git log**：コミットの履歴を確認する。</details>


<details><summary>Lesson 15 [ローカルリポジトリの作成] ローカルリポジトリを作りましょう</summary>

このLessonでは、ローカルリポジトリを実際に作っていきましょう。先ずディレクトリを作ってMarkdown形式のファイルを配置します。そして、そのディレクトリにローカルリポジトリを作成します。作成後はその状態を確認しましょう。

- ローカルリポジトリを作成するには
    
    本書ではMarkdownファイル(P.79参照)に学習した内容をメモして、そのファイルをバージョン管理しながらGitを学んでいきます。先ずはホームディレクトリに「ichiyasa」ディレクトリを作成し、そこに「Git_MEMO.md」というMarkdownファイルを保存します。「idhiyasa」ディレクトリにローカルリポジトリを作成したら、いったんその状態を確認してみましょう。
    
- Gitで管理するファイルを用意する
    1. 「ichiyasa」ディレクトリを作成する
        1. Git Bash(macOSではターミナル)を起動して、ホームディレクトリに「ichiyasa」ディレクトリを作ります。Chapter 2で解説したディレクトリ移動のcdコマンドと、ディレクトリ作成のmkdirコマンドを使いましょう。
        
        ```bash
        % cd ~ # ホームディレクトリに移動
        % mkdir ichiyasa # 「ichiyasa」ディレクトリを作成
        ```
        
    2. 「Git_MEMO.md」ファイルを作成する
        1. Visual Studio Codeを起動し、テキストファイルを作成し、「ichiyasa」ディレクトリに保存しましょう。その際、Markdownファイルは文字コードを「UTF-8」にしてください。「UTF-8」以外だとMarkdown用のビューワーなどで表示したときに文字化けする場合があります。Visual Studio Codeを使用していればデフォルトの文字コードは「UTF-8」になりますが、別のエディターを使用している場合は、文字コードに「UTF-8」を設定するように注意してください。
            1. Visual Studio Codeを開く
            2. ファイルタグから、新しいテキストファイルを選択
            3. 本書の内容を入力して、command + S を押す
            4. Finderが開くので、「ichiyasa」フォルダーを選択、ファイル名を「Git_MEMO.md」とする
            5. 保存をクリック
- 「ichiyasa」ディレクトリにローカルリポジトリを作ろう
    
    ローカルリポジトリには.gitというディレクトリが自動生成されています。ls -aコマンドで、ディレクトリの存在を確認してみましょう。
    
    1. ローカルリポジトリを作成する
        1. 先程作成した「ichiyasa」ディレクトリに移動して、ローカルリポジトリを作成します。git initコマンドを実行してみましょう。標準設定ではこのコマンドによってmasterという名のブランチが作られます(ブランチについてはChapter 5参照)。
        
        ```bash
        % cd ichiyasa # 「ichiyasa」ディレクトリに移動
        ichiyasa % git init # 「ichiyasa」ディレクトリにローカルリポジトリを作成
        Initialized empty Git repository in /Users/yoshiwo/ichiyasa/.git/ # Usersディレクトリの中のyoshiwoディレクトリの中のichiyasaディレクトリの中に.gitという初期化された空のGitリポジトリ(ローカルリポジトリ)
        ```
        
    2. ディレクトリ内を確認する
        1. lsコマンドでディレクトリの中にあるものを表示してみましょう。-aオプションで非表示ディレクトリも表示します。
        
        ```bash
        % ls -a # カレントディレクトリ以外のディレクトリやファイルを表示
        .		..		.git		Git_MEMO.md # (左から)起点カレントディレクトリ→Users→.gitディレクトリ→Git_MEMO.mdファイル
        ```
        
        - **Point** ローカルリポジトリの内容
            
            git initコマンドを実行すると、先程作成した「Git_MEMO.md」ファイルと別に、「.git」というディレクトリが自動作成されます。「.git」ディレクトリにはGitの情報が保管されているので削除してはいけません。
            
- ローカルリポジトリの状態を確認しよう
    
    ディレクトリに置いたファイルはワークツリーに配置されていることになります。その状態を確認してみましょう。ローカルリポジトリの状態を確認するには、git statusコマンドを実行します。
    
    ```bash
    % git status # ローカルリポジトリの状態を確認
    On branch main
    
    No commits yet
    
    Untracked files: # 登録されていないファイルは「Untracked files」という扱いになる
      (use "git add <file>..." to include in what will be committed)
    	Git_MEMO.md
    
    nothing added to commit but untracked files present (use "git add" to track)
    ```
    
    - **Point** git statusコマンドの実行結果の見方
        
        git statusコマンドの結果を見てみましょう。現時点では「Git_MEMO.md」ファイルを作成しただけなので、Gitの管理下にはファイルが登録されていません。**登録されていないファイルは「Untracked files」という扱いになる**ので、「Untracked files:Git_MEMO.md」と表示されています。
        
- git statusの結果の例
    
    ```bash
    On branch master # ブランチについての情報
    
    No commits yet # 一度もコミットしていない場合に表示される
    
    Untracked files: # untracked(追跡されていない)なファイルを表す
      (中略)
           Git_MEMO.md
    ```
    
    ```bash
    On branch master # ブランチについての情報
    
    No commits yet # 一度もコミットしていない場合に表示される
    
    Changes to be commited: # staged(ステージングエリアに追加済み)のファイルを表す
      (中略)
           new file:    Git_MEMO.md
    ```
    
    ```bash
    On branch master # ブランチについての情報
    Changes not staged for commit:
      (中略)
           modified:    Git_MEMO.md # modified(変更済み)のファイルを表す
    ```
    
    ```bash
    On branch master # ブランチについての情報
    nothing to commit, working tree clean # すべてコミットされ、その後に変更したファイルがないunmodified(変更されていない)状態を表す
    ```
    
- **ワンポイント** Markdownで構造を持つ文章を書こう
    
    Markdownは「見出し」や「段落」「箇条書き」などの構造を持つ文章を書くためのファイル形式です。オープンソースのソフトウェアの多くは、説明のためにREADME.mdなどのMarkdownファイルを添付しています。HTMLよりもシンプルな記述ルールになっており、手軽に構造を持つ文章を書けます。
    
    Markdownで記載した文章はそのままでもテキストエディターで読めますが、変換ツールを使用してMaikdownをHTMLやPDFにしたり、Markdown用のビューワーを使用したりすれば、より読みやすくなります。Visual Studio CodeにもMarkdownのビューワー機能がついており、command + K + V で表示できます。
### 用語
- **Markdown**：「見出し」や「段落」「箇条書き」などの構造を持つ文章を書くためのファイル形式のこと。
- **lsコマンド**：ディレクトリの中を確認する。lsコマンドの後ろにパラメーターとしてディレクトリパスを付けるとカレントディレクトリ以外のディレクトリの中を確認できる。
- **ls -a**：lsコマンドの後ろに-aオプションを付けるとファイルやディレクトリも表示される。
- **ワークツリー**：変更するファイルを保持する場所。「ワーキングツリー」「作業ディレクトリ」とも呼ぶ。
- **git statusコマンド**：ローカルリポジトリの状態を確認。</details>


<details><summary>Lesson 16 [ステージングエリアへの登録] ステージングエリアに登録しましょう</summary>

いよいよ、バージョン管理を実践していくLessonに入りました。最初のステップとして、先程作成した「Git_MEMO.md」をステージングエリアに登録します。パスの指定次第では、複数のファイルを同時に登録することもできます。

- ファイルをステージングエリアに登録しよう
    
    「Git_MEMO.md」ファイルをステージングエリアに登録してみましょう。ステージングエリアとは、コミットするファイルを登録する場所のことでしたね。ステージングエリアへファイルを登録するには、git addコマンドを使います。
    
    コマンドの後にファイルやディレクトリのパスを書くと、指定したファイルや指定したディレクトリ配下のファイルをステージングエリアに登録できます。
    
    - ステージングエリアに登録するコマンド
        
        ```bash
        $ git add Git_MEMO.md # git add=git addコマンド、Git_MEMO.md=ファイルパスまたはディレクトリパス
        ```
        
- ファイルやディレクトリの便利な指定方法を知ろう
    
    ファイルの数が多い場合に1つずつファイルを指定したり、カレントディレクトリに登録したいファイルがない場合にわざわざ移動したりするのは大変ですよね。そのようなときのために、相対パスの使い方に慣れておきましょう。git addコマンドにファイルパスを指定した場合はそのファイルだけが登録されますが、ディレクトリパスを指定した場合はディレクトリは以下のファイル全てを登録できます。このルールを覚えておけば、ファイル指定は簡単になります。
    
    - git addコマンドの利用例
        1. カレントディレクトリ配下の全てのファイルを追加
            
            ```bash
            $ git add . 
            ```
            
        2. 「subDirectory」ディレクトリ配下の全てのファイルを追加
            
            ```bash
            $ git add subDirectory
            ```
            
        3. 「subDirectory」ディレクトリ配下のfile1.mdを追加
            
            ```bash
            $ git add subDirectory/file1.md
            ```
            
- ファイルをステージングエリアに登録する
    1. git addコマンドでステージングエリアに登録する
        1. git addコマンドを使って「Git_MEMO.md」ファイルをステージングエリアに登録しましょう。ここでは相対パスで指定します。絶対パスも利用できますが、相対パスの方が簡単です。
        
        ```bash
        $ git add Git_MEMO.md
        ```
        
        ※git addコマンドで指定した相対パスが間違っている場合は、「fatal; pathspec ’ファイル名’ did not match any files」と表示されます。
        
    2. ステージングエリアに登録されたことを確認する
        1. git statusコマンドでローカルリポジトリの状態を確認してみましょう。実行結果を見てみると、「Git_MEMO.md」の分類が「Untracked files:」から「Changes to be committed:」に変わっていますね。「Git_MEMO.md」の前に「new file:」と書かれており、「Git_MEMO.md」が新しいファイルとしてステージングエリアに登録されたことがわかります。
        
        ```bash
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git status # 現在の状態を確認する
        On branch main
        
        No commits yet
        
        Changes to be committed:
          (use "git rm --cached <file>..." to unstage)
        	new file:   Git_MEMO.md
        ```

### 用語
- **ステージングエリア**：コミットするファイルを登録する場所。
- **git addコマンド**：ステージングエリアにファイルを登録する。
- **ディレクトリパス**：ディレクトリの位置を表したもの。
- **git add .**：カレントディレクトリ配下の全てのファイルを追加できて便利。
- **git status**：現在の状態を確認する。</details>


<details><summary>Lesson 17 [ファイルの差分確認] ファイルの差分を確認しましょう</summary>

ファイルの修正前と修正後の違いを「差分」といいます。差分を見て意図しない変更がないか確認することはとても重要です。このLessonでは、ワークツリーとステージングエリアや、ステージングエリアとGitディレクトリの差分を確認する方法を紹介します。

- ファイルの差分を確認する方法を知ろう
    
    ファイルの差分の確認方法も学びましょう。差分の確認にはgit diffコマンドを使用します。このコマンドによって様々な差分を確認できますが、今回は代表的な使い方を紹介します。まず、git diffコマンドに何もオプションをつけずに実行すると、ワークツリーとステージングエリアの差分を確認できます。そして--cachedオプションを付けるとステージングエリアとGitディレクトリの差分を確認できます。
    
- ファイルの差分を確認してみよう
    1. ファイルの差分を確認する準備をする
        1. では、実際に差分を確認する準備として、「Git_MEMO.md」ファイルを変更しましょう。この変更によって、ステージングエリアに登録した状態とワークツリーの状態が変わります。
    2. ワークツリーとステージングエリアの差分を確認する
        1. git diffコマンドを実行して、ワークツリーとステージングエリアの差分を確認してみましょう。追加した行は先頭に「+」が付いた緑色の文字で表示され、削除した行は先頭に「-」(マイナス)が付いた赤色の文字で表示されます。
        
        ```bash
        $ git diff # 各エリアの差分を確認する
        $ git diff --cached # ステージングエリアとGitディレクトリの差分を確認できる
        
        ichiyasa % git diff
        diff --git a/Git_MEMO.md b/Git_MEMO.md
        index 2a3fcae..66d3497 100644
        --- a/Git_MEMO.md
        +++ b/Git_MEMO.md
        @@ -1,2 +1,5 @@
         # Git学習メモ
        -## Gitコマンド
        \ No newline at end of file
        +## Gitコマンド
        +
        +- ローカルリポジトリを作る
        +      - git init
        \ No newline at end of file
        ```
        
        - **Point** 改行を追加すると行が変更されたとみなされる
            
            実行結果を見てみると、「Git_MEMO.md」ファイルの2行目の「## Gitコマンド」は、文章を変えていないのに行が削除されたことを意味する赤文字で表示されていますね。これは、2行目の文末に改行が追加されているので、「## Gitコマンド(改行なし)」という行が削除されて、「## Gitコマンド(改行あり)」という行が追加されたと見做されるためです。
            
    3. ステージングエリアとGitディレクトリの差分を確認する
        1. 続いて、git diffコマンドに--cachedオプションをつけて実行しましょう。コマンドを実行するとステージングエリアとGitディレクトリ(前回のコミット)の差分が表示されます。まだ一度もコミット実行していないので、ステージングエリアのファイルに書かれている行だけが表示されています。ワークツリーでの変更はステージングエリアに登録前なので、こちらの結果には表示されていませんね。
        
        ```bash
        $ git diff --cached # ステージングエリアとGitディレクトリの差分を確認できる
        
        ichiyasa % git diff --cached
        diff --git a/Git_MEMO.md b/Git_MEMO.md
        new file mode 100644
        index 0000000..2a3fcae
        --- /dev/null
        +++ b/Git_MEMO.md
        @@ -0,0 +1,2 @@
        +# Git学習メモ
        +## Gitコマンド
        \ No newline at end of file
        ```
        
- **ワンポイント** テキストファイルとバイナリファイル
    
ファイルは大きく分けて、文字のデータだけが格納されている「テキストファイル」と、それ以外の多くの情報を持つ「バイナリファイル」の2種類があります。テキストファイルは、Windowsの「メモ帳」やmacOSの「テキストエディット」、「Visual Studio Code」などで表示できるファイルが当てはまります。このLessonで編集しているMarkdownファイルはテキストファイルに当てはまります。バイナリファイルは、画像ファイルやMicrosoft Excelファイルのような、専用のアプリケーションで開く形式のファイルです。Gitではテキストファイルとバイナリファイルの両方をバージョン管理できます。しかし、Gitの機能を最大限に活用できるファイルはテキストファイルです。例えばバイナリファイルではgit diffコマンドでファイルの差分を確認できません。
### 用語
- **差分**：ファイルの修正前と修正後の違いを指す。
- **git diffコマンド**：各エリアの差分を確認する。
- **git diff --cached**：ステージングエリアとGitディレクトリの差分を確認できる。
- **git init**：ローカルリポジトリを作成する。
- **テキストファイル**：文字のデータだけが格納されているファイルのこと。例)Windowsの「メモ帳」、macOSの「テキストエディット」、「Visual Studio Code」などで表示できるファイル。
- **バイナリファイル**：文字のデータ以外の多くの情報を持つファイルのこと。例)画像ファイル、Microsoft Excelファイルのような専用のアプリケーションで開く形式のファイル。</details>


<details><summary>Lesson 18 [コミットする] ファイルをコミットしましょう</summary>

それではファイルをコミットしてみましょう。コミットには、「そのコミットがどういう内容なのか」を説明するコミットメッセージを書きます。このLessonでは、エディターを使ってコミットする方法と、より素早くコミットする方法の2つを紹介します。

- ローカルリポジトリにコミットしよう
    
    ステージングエリアに登録している「Git_MEMO.md」ファイルをコミットしましょう。コミットするには、git commitコマンドを利用します。
    
    コミットする際に、そのコミットでの変更内容を説明するコミットメッセージを書く必要があります。コマンドを実行すると、登録しておいたテキストエディター(本書ではVisual Studio Code)が開きます。コミットメッセージを書くとコミットが完了します。
    
    ※コミットメッセージを「日本語で書くか、英語で書くか」「1行で書くか、複数行で書くか」などは、チームの方針に合わせましょう。
    
- 「Git_MEMO.md」ファイルをコミットする
    
    まずは複数行のコミットメッセージを書いてコミットしてみましょう。コミットメッセージを書いてファイルを保存し、Visual Studio Codeを閉じると、コミットが完了します。
    
    1. ローカルリポジトリの状態を確認する
        
        ```bash
        $ git status # 現在の状況を確認する
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git status
        On branch main
        
        No commits yet # まだコミットしていない
        
        Changes to be committed: # Git_MEMO.mdがステージングエリアに登録されている
          (use "git rm --cached <file>..." to unstage)
        	new file:   Git_MEMO.md
        
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   Git_MEMO.md
        ```
        
    2. コミットを実行する
        
        ```bash
        $ git commit
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git commit
        hint: Waiting for your editor to close the file...
        ```
        
    3. Visual Studio Codeが開く
        
        ![スクリーンショット 2022-07-29 17.01.27.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/b4e15c9e-f3bb-4683-9f9c-251b76a0a44b/_2022-07-29_17.01.27.png)
        
        ※先頭が「#」の行はコメント行です。コミットメッセージには反映されません。
        
    4. コミットメッセージを書く
        
        ![スクリーンショット 2022-07-29 17.07.44.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/edb96ff0-6237-499e-8f3e-be06e11bf657/_2022-07-29_17.07.44.png)
        
        1. 1行目に要約(コミットタイトル)をかく
        2. 2行目は空白行
        3. 3行目以降に詳細を書く
        4. 書き終わったらファイルを保存してVisual Studio Codeを閉じる
    5. コミットが完了する
        1. Visual Studio Codeを閉じると、コミットが完了し、結果がコマンドラインに表示されます。
        
        ```bash
        # コミットメッセージのタイトルや、追加したファイルの情報が表示されます
        [main (root-commit) 2da8208] Gitの学習メモを作成
         1 file changed, 2 insertions(+)
         create mode 100644 Git_MEMO.md
        ```
        
    6. ローカルリポジトリの状態を確認する
        
        ```bash
        $ git status
        
        # ステージングエリアにあったGit_MEMO.mdは表示されなくなる
        # ワークツリーのGit_MEMO.mdはそのまま表示されています
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git status
        On branch main
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   Git_MEMO.md
        
        no changes added to commit (use "git add" and/or "git commit -a")
        ```
        
- **Point** オススメのコミットメッセージの形式
    
    コミットメッセージは1行で簡潔に書くことも、複数行を使って詳細を書くこともできます。
    
    複数行で書く場合は1行目に変更内容を要約した短い文章を書き、2行目を空白行にして3行目以降に詳細な説明を書く方法が、Gitの公式サイトに書かれているオススメの書き方です(参考：[https://git-scm.com/docs/git-commit#_discussion](https://git-scm.com/docs/git-commit#_discussion))。複数行で書いた場合は、1行目の内容がコミットタイトルして扱われます。
    
- コミットメッセージが1行の時に素早くコミットする
    
    コミットメッセージが1行の場合はVisual Studio Codeを開かずに素早くコミットできます。「Git_MEMO.md」を変更してステージングエリアに登録し、-mオプションを利用してコミットしてみましょう。
    
    1. 「Git_MEMO.md」ファイルを変更する
    2. ファイルをステージングエリアに登録する
        
        ```bash
        $ git add Git_MEMO.md
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git add Git_MEMO.md
        ```
        
    3. ステージングエリアの状態を確認する
        
        ```bash
        $ git status
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git status
        On branch main
        Changes to be committed:
          (use "git restore --staged <file>..." to unstage)
        	modified:   Git_MEMO.md
        # ステージングエリアに登録されている
        ```
        
    4. ファイルをコミットする
        1. git commitコマンドに-mオプションを付けると、コマンドラインから直接コミットメッセージを指定できます。コミットメッセージは「"」(ダブルクォーテーション)で囲みましょう。
        
        ```bash
        $ git commit -m "ローカルリポジトリの作成とステータスの確認コマンドを記載"
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git commit -m "ローカルリポジトリの作成とステータスの確認コマンドを記載"
        [main 9c379b8] ローカルリポジトリの作成とステータスの確認コマンドを記載
         1 file changed, 6 insertions(+), 1 deletion(-)
        # コミットされて結果が表示される
        ```
        
    5. ステータスを確認する
        1. 変更を全てコミットすると、ステータスを確認してもファイルは表示されなくなります。その代わりに「nothing to commit, working tree clean(コミットすべきものは何もない、ワークツリーはクリーンだ)」と表示されます。
        
        ```bash
        $ git status
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git status
        On branch main
        nothing to commit, working tree clean
        # コミットしていないファイルがないことを意味するメッセージが表示される
        ```
        
- **Point** コミットされるのはその時点でのファイルの状態
    
今回は「Git_MEMO.md」を2回コミットしましたが、そこに疑問を感じる人もいるかもしれませんね。コミットされるのは、git addコマンドでステージングエリアに登録した時点のファイルです。登録後にワークツリーで行った変更は含まれていません。新しい変更をステージングエリアに登録するためには、もう一度git addコマンドを実行する必要があります。
### 用語
- **git commitコマンド**：コミットを作成する(ファイルはステージングエリアからGitディレクトリに移動する(コミット(記録)される))。
- **コミットメッセージ**：コミットで加えた変更内容を説明するテキスト。
- **git commit -m**：コマンドラインから直接コミットメッセージを指定できる。この時、コミットメッセージは「"」ダブルクォーテーションで囲むこと。
- **ワークツリー**：Gitが保持している複数のコミットのうち、編集の開始地点となる場所。「ワーキングツリー」「作業ディレクトリ」とも呼ばれる。
- **ステージングエリア**：コミットするファイルを登録する場所。
- **Gitディレクトリ**：コミット(記録)を格納する場所。</details>


<details><summary>Lesson 19 [操作を取り消す] ローカルリポジトリでの操作を取り消しましょう</summary>


    

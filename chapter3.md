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
        
        ichiyasa % git add Git_MEMO.md
        ```
        
    3. ステージングエリアの状態を確認する
        
        ```bash
        $ git status
        
        ichiyasa % git status
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
        
        ichiyasa % git commit -m "ローカルリポジトリの作成とステータスの確認コマンドを記載"
        [main 9c379b8] ローカルリポジトリの作成とステータスの確認コマンドを記載
         1 file changed, 6 insertions(+), 1 deletion(-)
        # コミットされて結果が表示される
        ```
        
    5. ステータスを確認する
        1. 変更を全てコミットすると、ステータスを確認してもファイルは表示されなくなります。その代わりに「nothing to commit, working tree clean(コミットすべきものは何もない、ワークツリーはクリーンだ)」と表示されます。
        
        ```bash
        $ git status
        
        ichiyasa % git status
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

不要な変更をしていることに気がついて最後のコミットまで状態を戻したくなったり、誤ってステージングエリアに登録したものを取り消したくなったりすることがあります。このLessonでは、そのような変更を取り消す方法を2つ紹介します。

- 変更を取り消したくなるシチュエーションとは？
    
    ここまでにステージングエリアへの登録など、コミットするまでの一連の流れを説明してきました。しかし、ファイルを間違えて登録してしまった場合など、変更を取り消したくなることもあるかと思います。このLessonでは、ワークツリーへの変更を取り消す方法(git checkoutコマンド)と、ステージングエリアへの変更を取り消す方法(git resetコマンド)について紹介します。ワークツリーへの変更の取り消しでは、ファイルの状態が直前のコミット(または直前のステージングエリアへの登録)に戻ります。ステージングエリアへの変更の取り消しは、ファイルの状態はそのままでステージングエリアへの登録だけを取り消します。
    
    ※変更の取り消しといっても、エディターの「元に戻す」機能とは違います。
    
- git checkoutコマンドでワークツリーの変更を取り消す
    
    ファイルを色々と変更してしまったけれど、やっぱり直前にコミットした状態まで戻したくなった場合は、git checkoutコマンドを使ってワークツリーの変更を取り消せます。
    
    Chapter 5でも説明しますが、このコマンドはパラメーターにブランチ名を指定するとブランチを切り替えられます。今回のようにブランチ名ではなく「--」(ハイフン2つ)を指定すると、「直前のコミットの状態に戻す」という働きをします。
    
- **ワンポイント** git checkoutコマンドで取り消せないケース
    
    git checkoutコマンドで操作を取り消せない場合もあります。代表的なケースは、ファイルを新規作成したときやファイル名を変更したときです。ファイルを新規作成したときはファイルがそのまま残ってしまします。また、ファイル名を変更したときは、変更前のファイルと変更後のファイルの両方が残ってしまいます。どちらのケースも不要なファイルは自分で削除します。
    
- **ワンポイント** 新しく追加されたgit restoreとgit switchコマンド
    
    git checkoutコマンドはワークツリーの変更を取り消す以外にも、特定のコミットにワークツリーの状態を切り替えたり、ブランチの作成や切り替えができたりと、ひとつのコマンドで色々な操作ができます。多くの操作ができるのは便利ですがわかりづらくもあります(ブランチについてはChapter 5で紹介します)。
    
    そのため、よりわかりやすい役割分担のために導入されたのがgit restoreコマンドとgit switchコマンドです。git restoreコマンドを使うとワークツリーやステージングエリアの変更を取り消せます。そして、git switchコマンドを使うとブランチを切り替えられます。それぞれのコマンドでできることが少ないので、役割が明確でシンプルです。
    
    2つのコマンドはまだ正式版ではなく実験的にリリースされている状態であり、今度使い方が変更される可能性もあるので、本書では主にgit checkoutコマンドを使って解説します。しかし、git statusコマンドを実行した時に変更を取り消すヒントとして既にgit restoreコマンドが表示されていることから、今後は新しいコマンドの利用が推奨されていくと思います。そのため、どちらも試せるように、必要と思われる箇所では新しいコマンドを使う場合の方法も記載します。
    
- 「Git_MEMO.md」ファイルへの変更を取り消す
    1. 「Git_MEMO.md」ファイルを変更する
        
        ```bash
        # Git学習メモ
        ## Gitコマンド
        
        - ローカルリポジトリを作る
              - git init
        - ファイルの状態を確認
              - git status
        - ファイルを登録する # この2行を追記してファイルを上書き保存
              - git add
        ```
        
    2. ワークツリーの状態を確認する
        1. 一旦git statusコマンドを実行して、ワークツリーの状態を確認しておきましょう。
        
        ```bash
        $ git status
        
        ichiyasa % git status
        On branch main
        Changes not staged for commit: # ステージングエリアに登録されていない変更が表示される
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory) # ワークツリーディレクトリの変更を捨てるためにgit restore <file>を使用せよ
        	modified:   Git_MEMO.md
        
        no changes added to commit (use "git add" and/or "git commit -a")
        ```
        
        ※ステータスを確認した時、「use "git restore <faile>...” to discard changes in working directory」(ワークツリーの変更を捨てるには「git restore <file>」を使え)と表示されています。このように、Gitは操作のヒントを表示してくれることがあります。本書では次ページの方法で変更の取り消しを行いますが、どちらの方法でも構いません。
        
    3. ワークツリーの変更を取り消す
        
        ```bash
        $ git checkout -- Git_MEMO.md
        
        ichiyasa % git checkout -- Git_MEMO.md
        # git restore Git_MEMO.mdでも同じことができる
        ```
        
    4. ワークツリーの状態を確認する
        
        ```bash
        $ git status
        
        ichiyasa % git status
        On branch main
        nothing to commit, working tree clean # ワークツリーにはコミットしていないファイルがない、と表示
        ```
        
    5. ファイルを確認する
        
        ```bash
        # Git学習メモ
        ## Gitコマンド
        
        - ローカルリポジトリを作る
              - git init
        - ファイルの状態を確認
              - git status
        # ファイルは最後にコミットした状態へ戻っている(2行を付け加える前の状態)
        ```
        
        ※厳密にいうと、git checkoutコマンドは最後にコミットした状態ではなく、ステージングエリアの状態に戻すコマンドです。ステージングエリアにファイルの状態が登録されたままになっていると想定通りの動作になりませんそのような場合は、次で学ぶgit resetコマンドを使いましょう。
        
- ステージングエリアへの登録を取り消す
    
    間違ってファイルの状態をステージングエリアに登録してしまった時には、git resetコマンドを使って操作を取り消せます。先程学んだgit checkoutコマンドとは異なり、ワークツリー内のファイルの変更は取り消されません。下図のコマンドでは、git resetコマンドの後ろにHEADと指定していますね。
    
    HEADは、このローカルリポジトリで最後にコミットした状態を意味しています。ステージングエリアの状態を最後のコミットと同じ状態にリセットするという意味になります。
    
    - ステージングエリアへの登録を取り消すコマンド
        
        ```bash
        $ git reset HEAD Git_MEMO.md
        # git reset=git resetコマンド
        # HEADは最新のコミットを指す
        # Git_MEMO.md=ファイルパスまたはディレクトリパス
        ```
        
- **ワンポイント** git resetコマンドの働き
    
    git resetコマンドには、コミットをなかったことにする機能もあります。しかし、コミット自体に手を加えると様々な問題を引き起こすことがあるので、なるべく避けたほうがいいでしょう。
    
    コミットした内容を取り消したいときは、ファイルを以前の状態に修正して新しく「取り消すためのコミット」を追加しましょう。
    
- ステージングエリアへの登録を取り消す
    1. 「Git_MEMO.md」ファイルを変更する
        
        ```bash
        # Git学習メモ
        ## Gitコマンド
        
        - ローカルリポジトリを作る
              - git init
        - ファイルの状態を確認
              - git status
        - ファイルを登録する # この2行を追記してファイルを上書き保存
              - git add
        ```
        
    2. ファイルをステージングエリアに登録する
        
        ```bash
        $ git add Git_MEMO.md
        
        ichiyasa % git add Git_MEMO.md
        ```
        
    3. ローカルリポジトリの状態を確認する
        
        ```bash
        $ git status
        
        ichiyasa % git status
        On branch main
        Changes to be committed:
          (use "git restore --staged <file>..." to unstage)
        	modified:   Git_MEMO.md
        ```
        
        ステージングエリアに登録されたことを確認しましょう。メッセージを見ると「use "git restore --staged <file>..." to unstage」(アンステージにするには「git reset HEAD <file>...」を使え)と表示されています。
        
    4. ステージングエリアへの登録を取り消す
        
        ```bash
        $ git reset HEAD Git_MEMO.md
        
        ichiyasa % git reset HEAD Git_MEMO.md # git restore --staged Git_MEMO.mdでも同じことができます。
        Unstaged changes after reset: # リセットによってGit_MEMO.mdがunstagedされたと表示されています
        M	Git_MEMO.md
        ```
        
    5. ローカルリポジトリの状態を確認する
        
        ```bash
        $ git status
        
        ichiyasa % git status
        On branch main
        Changes not staged for commit: # Git_MEMO.mdはステージングエリアに登録されていないと表示される
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   Git_MEMO.md
        
        no changes added to commit (use "git add" and/or "git commit -a")
        ```
        
    6. 「Git_MEMO.md」ファイルを確認する
        
        ```bash
        # Git学習メモ
        ## Gitコマンド
        
        - ローカルリポジトリを作る
              - git init
        - ファイルの状態を確認
              - git status
        - ファイルを登録する # ファイルの内容は変更後の状態のままです
              - git add
        ```
        
        ※ファイルの内容も変更前に戻したい場合は、先程紹介したgit checkoutコマンドを使いましょう。
### 用語
- **git checkoutコマンド**：ワークツリーへの変更を取り消す。ブランチを作る。ブランチを切り替える。コミットした状態に切り替える。と、ひとつのコマンドで色々な操作ができる。一方で多いがためにわかりづらい側面もある。
    - **git checkout --**：直前のコミットの状態に戻す。
- **git reset**：ステージングエリアに追加した変更をワークツリーへ戻す(git add(ステージングエリアにファイルを登録する)を取り消す)。
- **git restoreコマンド**：ワークツリーやステージングエリアの変更を取り消すことができる。
- **git switchコマンド**：ブランチを切り替えられる。
- **ブランチ**：Gitで記録する履歴を枝分かれさせるための機能。複数の作業を並行して進める時に使用する。
- **git reset HAED**：ステージングエリアの状態を最後のコミットと同じ状態にリセットする。この時のHAEDは、ローカルリポジトリで最後にコミットした状態を意味する。</details>


<details><summary>Lesson 20 [ファイルを削除する] Gitの管理下にあるファイルを削除しましょう</summary>

Gitの管理下にあるファイルは、エクスプローラーなどで削除しただけでは不十分です。削除をステージングエリアに登録し、コミットしなければいけません。git rmコマンドを使うと、ファイルの削除とステージングエリアへの登録をコマンド1つで実行してくれます。

- Git管理下のファイルを削除しよう
    
    git rmコマンドはGitで管理しているファイルやディレクトリを削除するためのコマンドです。このコマンドを実行すると、ワークツリーからファイルやディレクトリを削除し、削除した状態をステージングエリアに登録します。その後でコミットすると削除作業が完了します。
    
    ※エクスプローラーやFinderでファイルやディレクトリを削除した場合は、git addコマンドを使って「ファイルを削除した状態」をステージングエリアに登録してください。git rmコマンドはそれらをまとめてやってくれるコマンドです。
    
- ディレクトリを削除するときは書き方が異なる
    
    ディレクトリを削除するにはgit rmコマンドに-rオプションを指定します。-rとはrecursive(再帰的)の略で、「指定したディレクトリの中にあるファイルやディレクトリに対して、削除の処理を繰り返し実行する」という意味を持ちます。-rオプションをつけないと中身があるディレクトリを削除できません。
    
    - ファイルやディレクトリを削除するコマンド
        
        ```bash
        $ git rm remove_me.txt
        # git rm = git rmコマンド
        # remove_me.txt = ファイルパス
        ```
        
        ```bash
        $ git rm -r subDirectory
        # -r = -rオプション
        # subDirectory = ディレクトリパス
        ```
        
        ※ディレクトリを削除するときは、-rオプションを忘れないようにしましょう。
        
- 不要なファイルをわざと追加して削除する
    
    git rmコマンドの使い方を学ぶために、次ページの手順では一旦不要なファイル(remove_me.txt)を作成します。それをコミットした後、git rmコマンドで削除してみましょう。
    
    - 次ページで行う作業
        1. 作成する
            1. ワークツリーにremove_me.txtファイルが作られる。
        2. 登録する
            1. ステージングエリアにremove_me.txtファイルが登録される。
        3. コミット
            1. Gitディレクトリにremove_me.txtファイルがコミット(記録)される。
        4. 削除する
            1. remove_me.txtファイルを削除してワークツリーに登録する。
            2. 削除したremove_me.txtファイルをステージングエリアに登録する。
        5. コミットする
            1. Gitディレクトリに削除したremove_me.txtファイルを登録する。
- 「remove_me.txt」ファイルを用意する
    1. 削除するファイルを作成する
        1. Visual Studio Codeを起動してファイルを新規作成し、「remove_me.txt」という名前で保存します。削除を試すためのものなので中身は入力しません。
            1. ファイルタグから「新しいテキストファイル」をクリック→ファイルタグから「名前を付けて保存…」をクリック
            2. Finderが開くので、ファイル名を「remove_me.txt」という名前に、保存する場所は「Git_MEMO.md」と同じディレクトリにすること。今回の場合は「ichiyasa」という名前のディレクトリ。
    2. ファイルをステージングエリアに登録する
        
        ```bash
        $ git add remove_me.txt
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git add remove_me.txt
        ```
        
    3. ファイルをコミットする
        
        ```bash
        $ git commit -m "削除対象のファイルを作成"
        # git commitコマンドに-mを付けると、コマンドラインから直接コミットメッセージを指定できる
        # このとき指定するメッセージは「"」ダブルクォーテーションで囲むこと
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git commit -m "削除対象のファイルを作成"
        [main eda8205] 削除対象のファイルを作成
         1 file changed, 0 insertions(+), 0 deletions(-)
         create mode 100644 remove_me.txt
        ```
        
    4. ディレクトリにあるファイルを確認する
        
        ```bash
        $ ls
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % ls
        Git_MEMO.md	remove_me.txt # 「remove_me.txt」ファイルが存在していることを確認
        ```
        
- 「remove_me.txt」ファイルを削除する
    1. ファイルを削除する
        
        ```bash
        $ git rm remove_me.txt
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git rm remove_me.txt
        rm 'remove_me.txt'
        ```
        
    2. ディレクトリにあるファイルを確認する
        
        ```bash
        $ ls
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % ls
        Git_MEMO.md # 「remove_me.txt」ファイルが削除されていることがわかる
        ```
        
        ※git rmコマンドでファイルを削除してもコミットされたわけではありません。コミットしないとバージョン管理されないので、git rmコマンドの実行後にコミットすることを忘れないようにしましょう。
        
    3. ファイルの状態を確認する
        
        ```bash
        $ git status
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git status
        On branch main
        Changes to be committed:
          (use "git restore --staged <file>..." to unstage)
        	deleted:    remove_me.txt # 「remove_me.txt」ファイルの状態がdeletedとしてステージングエリアに登録されている
        
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   Git_MEMO.md
        ```
        
    4. ファイルを削除したことをコミットする
        
        ```bash
        $ git commit -m "remove_me.txtファイルを削除する" # git commit -mでコマンドラインから直接コミットメッセージを指定できる
        
        yoshiwo@Yoshiwos-MacBook-Pro ichiyasa % git commit -m "remove_me.txtファイルを削除する"
        [main 642aeee] remove_me.txtファイルを削除する #削除したことがコミットされる
         1 file changed, 0 insertions(+), 0 deletions(-)
         delete mode 100644 remove_me.txt
        ```
        
- **ワンポイント** 改行コードの警告
    
    git addコマンドの実行結果に「warning: LF will be replaced by CRLF in ファイル名」という警告が表示されることがあります。
    
    これは、Gitのインストール次に指定した改行コードの設定が影響しており(P.37参照)、改行コードを「LF」で保存したファイルが、「CRLF」に変換されることがあると警告しています。ファイルの改行コードを変換したくない場合は、P.63で学んだgit configコマンドでcore.autocrifの設定をfalseにしましょう。
### 用語
- **git rmコマンド**：Gitで管理しているファイルやディレクトリを削除するためのコマンド。
- **git rm -r**：git rmに-rオプションを指定すると、「指定したディレクトリの中にあるファイルやディレクトリに対して、削除の処理を繰り返し実行する」という意味を持つ。-rはrecursive(再帰的(コンピューターで、ある作業中に、さらに同じ作業を呼び出して処理すること))の略。
- **git addコマンド**：ステージングエリアにファイルを登録する。
- **git commitコマンド**：コミットを作成する(ファイルはステージングエリアからGitディレクトリに移動する(コミット(記録)される))。
- **git commit -m**：コマンドラインから直接コミットメッセージを指定できる。この時、コミットメッセージは「"」ダブルクォーテーションで囲むこと。
- **lsコマンド**：カレントディレクトリ内のファイルとディレクトリが表示される。</details>


<details><summary>Lesson 21 [Gitで管理しないファイルを設定] Gitで管理しないファイルを設定しましょう</summary>

Gitで管理すべきではないファイルも存在します。そういうファイルはステージングエリアへ登録しないようにしましょう。このLessonでは、どのようなものを管理すべきでないのか紹介し、それらを無視するための設定方法について紹介します。

- Gitで管理すべきでないファイル
    
    Gitでバージョン管理すべきではないファイルというものが存在します。例えば、アプリケーションをビルドする際に自動作成されるパッケージファイルやログファイル、ファイルをコピーしてリネームしたバックアップなどの一時ファイルは、Gitで管理すべきではありません。ログファイルはアプリケーションを実行するたびに出力されるものですし、パッケージファイルはビルドすれば作成されるものなので、あえてバージョン管理をする必要はありません。また、バックアップファイルはGitでバージョン管理をしていれば不要になりますよね。他にも、パスワードのようなセキュリティに関する情報が書かれたファイルも、Gitに登録するべきか必ず検討しましょう。
    
    Gitに登録したファイルは、リモートリポジトリを共有しているメンバー全員に公開されてしまいます。「リモートリポジトリを共有しているメンバーに見られてもいい情報なのか」を必ず意識するようにしましょう。
    
    - Gitで管理すべきではないファイル
        - ログファイル
        - パッケージファイル
        - バックアップファイル
        
        など自動生成される一時ファイルは管理不要。
        
        - WindowsのThumbs.db
        - macOSの.DS_Store
        
        OSのファイル管理のためのものなので不要。
        
        - パスワードが書かれたファイル
        
        リモートリポジトリで共有すべきでない情報。
        
    
    ※不要なファイルがあると、リポジトリのサイズが大きくなったり、無駄なコミットやコンフリクトが発生したりと、いろいろな問題が起きます。
    
- Gitで管理しないファイルを設定しよう
    
    ステージングエリアへ登録する時に、毎回Gitで管理したくないファイルを意識するのは大変ですし、ミスが発生する可能性もあります。そういう時のためにGitで管理しないファイルを設定できます。設定は簡単で、.gitignoreファイルというテキストファイルをローカルリポジトリに配置して、そこに無視したいファイル名やディレクトリ名を書くだけです。.gitignoreファイルはローカルリポジトリ配下であればどこに置いてもいいですが、.gitignoreファイルが配置されたディレクトリ配下のパスにしか効果がありません。ローカルリポジトリ内のすべてのディレクトリに設定を反映するには「.git」ディレクトリと同じディレクトリに保存しましょう。
    
    設定してしまえば、git statusコマンドでファイルが表示されることもなく、git addコマンドでディレクトリを指定した時にも、そのファイルは無視されます。
    
    - .gitignoreの配置場所
        - 「ichiyasa」ディレクトリ(カレントディレクトリ)
            - 「.git」ディレクトリ
            - .gitignore
                - .gitignoreの内容→sample.txt
            - Git_MEMO.md
            - sample.txt→.gitignore内にあるのでGitに無視される
        
        ※.gitignoreファイルは、その名のとおり「Gitが無視(ignore)する」設定をします。
        
    - .gitignoreの書き方
        - ファイル名を直接指定する
        - ディレクトリ名を指定する(ディレクトリ全体が対象)
        - *(アスタリスク)を使えば、ファイルの拡張子で指定できる
- .gitignoreファイルを作ってみよう
    
    .gitignoreの効果を体感するために、Gitの管理から外したい「sample.txt」ファイルを作成し、.gitignoreファイルに指定して無視させてみましょう。
    
    1. 「sample.txt」ファイルを作成する
        1. Visual Studio Codeを起動して、「sample.txt」という名前で保存します。「sample.txt」の中身は何も書かなくて構いません。
            1. ファイルタグから「新しいテキストファイル」をクリック→ファイルタグから「名前を付けて保存…」をクリック
            2. Finderが開くので、ファイル名を「sample.txt」という名前に、保存する場所は「Git_MEMO.md」と同じディレクトリにすること。今回の場合は「ichiyasa」という名前のディレクトリ。
    2. .gitignoreファイルを作る前の状態を確認する
        
        ```bash
        $ git status
        
        ichiyasa % git status
        On branch main
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   Git_MEMO.md
        
        Untracked files:
          (use "git add <file>..." to include in what will be committed)
        	sample.txt # 「sample.txt」ファイルがUntracked filesに表示されている ファイルを作成しただけでGitの管理下にはファイルが登録されていない状態
        
        no changes added to commit (use "git add" and/or "git commit -a")
        ```
        
    3. .gitignoreファイルを作成する
        1. 次に.gitignoreファイルを作成し、「sample.txt」を指定しましょう。尚、Windowsで.gitignoreファイルのようなファイル名が「.」(ドット)で始まるファイルを作成する場合は、Visual Studio Codeからファイルを作成するようにしてください。それ以外の方法だと面倒な手間が発生することがあります。
            1. ファイルタグから「新しいテキストファイル」をクリック→ファイルタグから「名前を付けて保存…」をクリック
            2. Finderが開くので、ファイル名を「.gitignore」という名前に、保存する場所は「sample.txt」と同じディレクトリにすること。今回の場合は「ichiyasa」という名前のディレクトリ。
    4. .gitignoreファイルを作った後の状態を確認する
        1. .gitignoreに「sample.txt」を指定した前後でgit statusコマンドの実行結果が変わっています。「sample.txt」が表示されなくなり、ファイルはGitから無視されるようになりました。
        
        ```bash
        $ git status
        
        ichiyasa % git status
        On branch main
        Changes not staged for commit:
          (use "git add <file>..." to update what will be committed)
          (use "git restore <file>..." to discard changes in working directory)
        	modified:   Git_MEMO.md
        
        Untracked files:
          (use "git add <file>..." to include in what will be committed)
        	.gitignore # 「sample.txt」ファイルが表示されなくなり、.gitignoreファイルがUntracked filesに表示
        
        no changes added to commit (use "git add" and/or "git commit -a")
        ```
        
    5. .gitignoreファイルをステージングエリアに登録する
        
        ```bash
        $ git add .gitignore
        
        ichiyasa % git add .gitignore
        ```
        
    6. .gitignoreファイルをコミットする
        
        ```bash
        $ git commit -m ".gitignoreファイルを追加する"
        
        ichiyasa % git commit -m ".gitignoreファイルを追加する"
        [main 06b898e] .gitignoreファイルを追加する
         1 file changed, 1 insertion(+)
         create mode 100644 .gitignore # .gitignoreファイルがコミットされた
        ```
        
    
    ※macOSでは「.DS_Store」ファイル、Windowsでは「Thumbs.db」ファイルが、フォルダーに作成されることがあります。これらのファイルはGitで管理する必要がないので、.gitignoreファイルに設定しておきましょう。
    
- **ワンポイント** .gitignoreファイルのテンプレート
    
    さまざまなプログラミング言語やツールのための.gitignoreファイルのテンプレートをGitHub社がオープンソースで公開しています。
    
    .gitignoreファイルの書き方に迷ったら、こちらを参考にしてみましょう。( [https://github.com/github/gitignore](https://github.com/github/gitignore) )
### 用語
- **Gitで管理すべきではないファイル**：アプリケーションをビルドする際に自動作成されるパッケージファイルやログファイル、ファイルをコピーしてリネームしたバックアップなどの一時ファイル。
- **コンクリフト**：複数ブランチで(複数人で)同じファイルの同じ箇所を編集した後に起こる衝突。必要な内容を勝手に上書きしないための機能。
- **.gitignore**：Gitで管理したくないファイルやディレクトリを指定するためのファイル。先頭の「.」は隠しファイルであることを意味します。
- **untracked**：(追跡されていない)ファイルを表す。</details>


- Lesson 22 [コミット履歴の確認] コミットの履歴を確認しましょう

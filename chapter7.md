# Chapter 7 コンフリクトに対処しよう
並行作業をしていると発生しうる「コンフリクト」という現象の解決方法について学びます。

苦手意識を持たれることも多いテーマですが、ぜひ丁寧に読んで理解を深めてくださいいよいよラストスパート、がんばりましょう。

<details><summary>Lesson 40 [コンフリクトの理解] コンフリクトとは何かを理解しましょう</summary>

コンフリクトについて理解するところから始めましょう。コンフリクトは機能の名前ではなく、Gitを使っていると時々出くわす現象のことです。先ずは、どんなときに、なぜ発生するのか把握しておくことが大事です。
- コンフリクトの発生条件を知ろう
    
    コンフリクトは、マージやリベース、プルなど、ブランチを統合する際に発生しうるものです。わかりやすくするため、このLessonではマージを例にして説明していきます。これまでのChapterで確認してきたように、Gitはgit mergeコマンドさえ実行すれば、適切に内容を統合してくれます。しかし、マージする2つのブランチがそれぞれ同じファイルの同じ箇所に異なる変更を加えていた場合、Gitはマージの仕方を判断することができません。
    
    例えば、masterブランチで、あるファイルに「東京都」と書かれていたとします。そこからトピックブランチを作成し、「北海道」と書き換えてmasterブランチにマージしようとしたところ、masterブランチの内容が別の作業者により「沖縄県」に変更されていたらどうでしょう。Gitは、マージ後に残すべきなのが「北海道」なのか「沖縄県」なのか判断することができないのです。このとき発生するのが「コンクリフト」です。コンフリクトが起きたら、人間がマージ後の正しい姿を判断し、手動でマージを行う必要があります。
    
    ※コンフリクトのことを日本語で「競合」と呼ぶこともあります。

- コンフリクトを解消してブランチをマージする
    
    masterブランチの変更をセッション情報更新用ブランチに取り込もうとすると、コンフリクトが発生します。ヤマグチさんによる変更もイチヤサさんが行っていた変更も失わないようにファイルを書き換え、マージを完了させましょう。ここまでできたら、これまでと同じようにプルリクエストの作成、レビュー、マージを終えて作業完了です。
### 用語
コンフリクト：複数ブランチで(複数人で)同じファイルの同じ箇所を編集した後に起こる衝突。必要な内容を勝手に上書きしないための機能。</details>


<details><summary>Lesson 41 [コンフリクトの発生] コンフリクトを発生させてみましょう</summary>

実際にコンフリクトを発生させましょう。作業自体はこれまで行ってきたものとほぼ同じですが、マージの結果が少し変わるので注目してください。一部、登場人物のヤマグチさんになったつもりで作業していただくため、ややこしいですががんばりましょう。
- セッション情報を更新するためのプルリクエストを作成しよう
    1. ブランチの作成からプルリクエスト作成まで進める
        1. 今回は、change-session-titleというブランチを作成して作業します。前のChapterと同様に、git checkoutコマンドを実行しましょう。
        
        ```bash
        $ git checkout -b change-session-title # 「change-session-title」ブランチを作成し、切り替える
        
        % git checkout -b change-session-title
        Switched to a new branch 'change-sesssion-title'
        ```
        
        - Point ブランチ名の付け方はさまざま
            
            これまでのLessonでいくつかのブランチを作成してきましたが、update-venue、speakers-info、change-session-titleなどその都度命名の仕方が異なっていることに気付いたでしょうか。実はブランチ名の付け方もチームによってさまざまなのです。内容を表していれば名前は自由ということもあれば、案件名を必ず付ける、バグトラッキングシステムのチケットIDを使う、などルールを設けている場合もあり、多岐にわたります。
            
    
    ※Gitは様々な使い方ができるので、運用ルールを決めてチームで合意しておくことがとても大事ですね。ブランチ名の付け方もその一例です。
    
    1. セッションタイトルを書き替える
        1. index.htmlを開いてセッションタイトルを書き替えましょう。うらがみさんのセッションタイトルを、「現場で使える！実践Git」から「めざせ脱初心者！現場で使える実践Git」に変更します。
2. 変更をコミットしてプッシュする
    1. コミット、プッシュを行ったのち、プルリクエストを作成したところで手を止めてください。先程説明したシナリオを実現するため、マージは行いません。少し後で、コンフリクトが起きた状態にして、プルリクエストがどうなるのかを確認します(P.219参照)。
    
    ```bash
    $ git commit -am "うらがみさんのセッションタイトルを更新した" # コミットを作成し、同時にステージングエリアの追加と記録を保持した
    
    % git commit -am "うらがみさんのセッションタイトルを更新した"
    [change-sesssion-title 4de2619] うらがみさんのセッションタイトルを更新した
     1 file changed, 1 insertion(+), 1 deletion(-)
    ```
    
    ```bash
    $ git push origin change-session-title # プッシュコマンドを行う
    
    % git push origin change-session-title
    Enter passphrase for key '/Users/yoshiwo/.ssh/id_ed25519': 
    Enumerating objects: 5, done.
    Counting objects: 100% (5/5), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 396 bytes | 396.00 KiB/s, done.
    Total 3 (delta 2), reused 0 (delta 0), pack-reused 0
    remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
    remote: 
    remote: Create a pull request for 'change-session-title' on GitHub by visiting:
    remote:      https://github.com/YSWEngineer/ichiyasaGitSample/pull/new/change-session-title
    remote: 
    To github.com:YSWEngineer/ichiyasaGitSample.git
     * [new branch]      change-session-title -> change-session-title
    ```
    
    **※ブランチ名を間違えて登録したため解決方法を検索→[gitのローカルのブランチ名を変更したいとき]今開いているブランチをリネームする場合は、単純に新しいブランチ名を指定するだけです**。`git branch -m <新しいブランチ名>`
    
    ※[Create pull request]をクリックして、プルリクエストを作成した状態で放置してください。
- ヤマグチさんによる作業をmasterブランチに反映しよう
    
    さて、ここからはヤマグチさんの作業です。トピックブランチを作成してタイムテーブルのレイアウトを変更し、masterブランチにマージしたとの状態を作り出します。ここでは手順をシンプルにするために、ブラウザー上でGitHubのmasterブランチにあるファイルを直接編集してみましょう。これをもって、ヤマグチさんがトピックブランチを作成し、ファイル編集、コミット、プルリクエスト作成、そしてマージまでを済ませたものと思ってください。
1. GitHubでファイルの編集画面を開く
    1. ブラウザーで、GitHub上にあるリモートリポジトリの画面を開き、ファイル一覧からindex.htmlをクリックします。これでGitHubの画面上にindex.htmlの内容が表示されます。
        
2. index.htmlを編集する
    1. ファイルの右上にある鉛筆の[Edit this file]ボタンをクリックすると、ブラウザー上でファイル編集ができます。タイムテーブルに以下のような変更を加えてみましょう(テキスト参考)。
            
3. 変更をコミットする
    1. 編集が完了したら、下のほうにスクロールしていくと「Commit changes」というフォームが現れます。ここでコミットメッセージを入力し、[Commit changes]をクリックして内容を確定させます。これで、編集した内容を反映するmasterブランチへのコミットが作成されます。
            
    ※テキストと実際の画面と内容が異なっている。
- masterブランチの変更を取得する
    
    ヤマグチさん役はここまでです。さて、masterブランチに入った変更をchange-session-titleブランチに取り込みましょう。手順は、Chapter 6で学習したものと同じです。
    
    1. ローカルリポジトリのmasterブランチを最新化する
        1. 先ずはmasterブランチに切り替え、git pullコマンドで最新化を行いましょう。先程ヤマグチさんとしてGitHub上で編集した内容を取得することができます。
        
        ```bash
        $ git checkout master # masterブランチに切り替える
        
        % git checkout master
        Switched to branch 'master'
        Your branch is up to date with 'origin/master'.
        ```
        
        ```bash
        $ git pull origin master # 最新化して編集した内容を取得する
        
        % git pull origin master
        Enter passphrase for key '/Users/yoshiwo/.ssh/id_ed25519': 
        From github.com:YSWEngineer/ichiyasaGitSample
         * branch            master     -> FETCH_HEAD
        Already up to date.
        ```
        
    2. change-session-titleブランチにmasterブランチをマージする
        1. 続いて、再びchange-session-titleブランチへ戻り、masterブランチをマージします。ところが、これまでとは違い、「CONFLICT(content): Merge conflict in index.html」というメッセージが表示されます。これがコンクリフト発生の合図です。
        
        ```bash
        $ git checkout change-session-title # ブランチを「change-session-title」ブランチに切り替える
        
         git checkout change-session-title
        Switched to branch 'change-session-title'
        ```
        
        ```bash
        $ git merge master # masterブランチをマージする
        
        ```

### 用語
- **git checkout -b ブランチ名**：対象のブランチを新規作成し、切り替える。
- **git commitコマンド**：コミットを作成する(ファイルはステージングエリアからGitディレクトリに移動する(コミット(記録)される))。
    - **git commit -am**：**-aオプション**はステージングエリアの追加を行う。**-mオプション**はコミットメント(記録を保持すること)を指定する。-amと一度にまとめてオプションを行うことが可能。
- **git pushコマンド**：ローカルリポジトリからリモートリポジトリに反映すること。
- **git pullコマンド**：リモートリポジトリ内のブランチの内容が、ローカルリポジトリ内の同じ名前のブランチに反映されます。同時にワークツリーへの反映も行われます。</details>


<details><summary>Lesson 42 [コンフリクトの解消] コンフリクトが発生した際の対応を学びましょう</summary>

コンフリクトの状況を確認する方法と、どう対処したら良いかを説明します。これまでは自動で行えていたマージがうまくいかず少々不安にもなりますが、何が起こっているか把握できれば大丈夫です。慌てず、ファイルを正しい状態へと編集しましょう。
- コンフリクトの発生を確認しよう
    1. git statusコマンドで確認する
        1. git statusコマンドを実行すると、その結果でコンフリクトの発生を確認することができます。「both modified」すなわち、マージ先とマージ元の両ブランチで変更を加えたと書かれているファイルがコンフリクトしています。
        
        ```bash
        $ git status
        ```
        
        ![git statusコマンドで確認する.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d4a3a8c4-b902-4528-bf75-6d80a4f6253b/git_status%E3%82%B3%E3%83%9E%E3%83%B3%E3%83%88%E3%82%99%E3%81%A6%E3%82%99%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B.jpeg)
        
    - **ワンポイント** コンフリクト発生時のyouとthem
        
        コンフリクト発生時にファイルの状態を表すメッセージとして、both modified以外に「deleted by them」や「added by you」などと表示されることがあります。いきなり人を表す代名詞が出てきて戸惑うかもしれませんが、youはマージ元である現在使用中のブランチ、themはマージ先のブランチを指します。例えば、使用中のブランチで編集したファイルがマージ先のブランチで削除されていた場合、表示されるのはdeleted by themです。
        
    1. GitHub上で確認する
        1. GitHub上のプルリクエストの画面でもコンフリクトを確認することができます。change-session-titleブランチのプルリクエストを見ると、「This branch has conflicts that must be resolved」(このブランチには解消が必要なコンフリクトがある)と表示され、マージができなくなっているはずです。初めに解説した通り、コンフリクトがあるとGitは正しいマージの内容を判断できず、自動で完了させることができないためです。
        
        ![GitHub上で確認する.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9aad6e67-a351-4e69-b466-fd6b07684fea/GitHub%E4%B8%8A%E3%81%A6%E3%82%99%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B.jpeg)
        
- ファイルを正しい状態に編集し直そう
    1. コンフリクトの原因となっている箇所を特定する
        1. Visual Studio Codeでindex.htmlを開きましょう。タイムテーブルを見ると、連続する<<<と>>>、そして===で囲まれた部分が見つかると思います。それぞれ、<<<の行から>>>の行までがコンフリクトしている箇所、===の行がマージ先とマージ元の変更箇所の境目です。今回は、以下のようになっているはずです。
        
        ![コンフリクトの原因となっている箇所を特定する.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/1f439e9b-cab5-4160-a4df-b27991bee6ca/%E3%82%B3%E3%83%B3%E3%83%95%E3%83%AA%E3%82%AF%E3%83%88%E3%81%AE%E5%8E%9F%E5%9B%A0%E3%81%A8%E3%81%AA%E3%81%A3%E3%81%A6%E3%81%84%E3%82%8B%E7%AE%87%E6%89%80%E3%82%92%E7%89%B9%E5%AE%9A%E3%81%99%E3%82%8B.jpeg)
        
    2. ファイルを正しく修正しよう
        1. ヤマグチさんが変更したタイムテーブルの形式に合わせながらも、うらがみさんのセッションタイトルを更新した状態を目指してファイル修正をしましょう。コンフリクトの印である記号は、解消と同時に忘れずに削除してください。
        
        ![ファイルを正しく修正しよう.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/23eb809b-1800-4159-8574-3539ea67165f/%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%82%92%E6%AD%A3%E3%81%97%E3%81%8F%E4%BF%AE%E6%AD%A3%E3%81%97%E3%82%88%E3%81%86.jpeg)
        
- 修正したファイルを再度コミットしよう
    1. ステージングエリアに追加する
        1. 編集が完了したらステージングエリアに追加しましょう。その後git statusコマンドを実行すると、これまでと同様にファイルの編集が確認できます。また、「All conflicts fixed but you are still merging.(use "git commit" to conclude merge)」(コンフリクトは解消したが、マージは終わっていない。コミットを行ってマージを完了させよ)と表示されていますね。コンフリクトにより失敗したマージは、解消してコミットを行うまで、マージしている最中(マージが未完)のままとみなされます。
        
        ```bash
        $ git add -A
        ```
        
        ```bash
        $ git status
        ```
        
        ![ステージングエリアに追加する.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3334b677-b5f5-4b2c-9fdb-a7b831333245/%E3%82%B9%E3%83%86%E3%83%BC%E3%82%B7%E3%82%99%E3%83%B3%E3%82%AF%E3%82%99%E3%82%A8%E3%83%AA%E3%82%A2%E3%81%AB%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B.jpeg)
        
        ※コンフリクト発生中はなるべく他の作業をせず、先ず解消してマージしきることをオススメします。他の作業をすると、コンフリクト解消以外の内容がコミットに入ってしまい、後から作業の意味が分かりづらくなる恐れがあります。
        
    2. マージを完了する
        1. Gitが案内しているとおり、コミットを行うことでマージを完了させます。コマンドのパラメーターは必要ありません。Chapter 6で紹介したように(P.202参照)、コミットメッセージが入力された状態でエディターが立ち上がりますが、何も編集せずに閉じてしまえば大丈夫です。
        
        ```bash
        $ git commit
        ```
        
        ![マージを完了する.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/bf3a8ac7-13e6-4061-9223-2bd564572170/%E3%83%9E%E3%83%BC%E3%82%B7%E3%82%99%E3%82%92%E5%AE%8C%E4%BA%86%E3%81%99%E3%82%8B.jpeg)
        
    3. リモートリポジトリにプッシュする
        1. コンフリクトの解消が終わったら、これまでどおりプッシュを行いましょう。
        
        ```bash
        $ git push origin change-session-title
        ```
        
        ![リモートリポジトリにプッシュする.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/3b45cdf2-6f53-4548-a988-d72f55fa61af/%E3%83%AA%E3%83%A2%E3%83%BC%E3%83%88%E3%83%AA%E3%83%9B%E3%82%9A%E3%82%B7%E3%82%99%E3%83%88%E3%83%AA%E3%81%AB%E3%83%95%E3%82%9A%E3%83%83%E3%82%B7%E3%83%A5%E3%81%99%E3%82%8B.jpeg)
        
    4. プルリクエストを確認する
        1. プッシュした後でGitHubを表示して再度プルリクエストを確認すると、コンフリクト発生中とは異なり、自動でのマージができるようになっています。あとは、レビューをしてもらい、masterブランチへマージすれば作業完了です。
        
        ![プルリクエストを確認する.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a0523157-3929-4467-9c57-955aa3dc1337/%E3%83%95%E3%82%9A%E3%83%AB%E3%83%AA%E3%82%AF%E3%82%A8%E3%82%B9%E3%83%88%E3%82%92%E7%A2%BA%E8%AA%8D%E3%81%99%E3%82%8B.jpeg)
        
- **ワンポイント** コンフリクトを解消するために
    
    ファイルの種類や状況によって、コンフリクトが解消できたといえる状態は異なります。今回のように内容が正しいことを確認すればよいケースのみならず、コンパイルやアプリケーションの実行が正しく行えることや、テストに通ることを確認する必要がある場合も多々あります。しかし、ゴールはただ1つ、「ファイルが正しい状態となる」よう編集を行うことです。作業内容の意味を把握し、丁寧に対処するようにしましょう。1人で判断できない時は、コンフリクトの原因となった変更を加えたメンバーに意図を確認したり、チームで相談したり、コミュニケーションを取りながら作業をすることも大事なので覚えておきましょう！

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

+++
categories = [ "Software Engineering" ]
date = "2017-02-23T00:25:03-07:00"
draft = false
eyecatch = "hibernate_logo.png"
slug = "how-hibernate-ruined-my-career"
tags = [ "hibernate", "orm" ]
title = "Hibernateはどのようにして私のキャリアを破滅寸前にしたか"
+++

このエントリでは、Grzegorz Gajosによる記事、[How Hibernate Almost Ruined My Career](http://ggajos.com/how-hibernate-ruined-my-career/)を紹介する。
(Grzegorzから和訳と転載の許可は得た。)
以下はその全文の和訳だが、意訳超訳が混じっているので、もとのニュアンスを知りたければ元記事を読んでもいいし、読まなくてもいい。

<br>

{{< google-adsense >}}

----------------
想像してくれ。
君はJava開発者で、次のビッグプロジェクトを開始しようとしているところだ。
君は、そのプロジェクト全体に影響する根本的な決断をする必要がある。
君の柔軟なデータモデルをオブジェクト指向で抽象化するベストな方法を選択したい。生のSQLを扱いたくはないからね。
どんな種類のデータもサポートしたいし、理想では全種のデータベースをサポートしたい。

すぐに思いつくのは、単にHibernateを使うという解だ。そうだろ？
Javaディベロッパの90%は君に同意するだろう。
しかし、それって正しい決断になっているだろうか？

Hibernateが一般に受け入れられているスタンダードだからといって盲目的に採用してしまうと、どんな問題が発生するかを見てみよう。

モニカというJava開発者がいるとしよう。
モニカは最近出世してアーキテクトの役職に就き、会社の新製品のための技術スタックを選定する責任者になった。
彼女は、Javaの世界にはデータベースとのやり取りを扱うたった一つの適切なツールがあることを知っている。Hibernateだ。
Hibernateは良く知られ支持されているJPAのスタンダードではあるが、プロジェクト開始前に多少のチェックをするのが定跡だ。
幸いにも、同僚のベンが適任者を知っている。

# 4年前、Hibernateは銀の弾丸かのように見えた
* ベン: やあモニカ。ジョンを紹介させてくれ。彼はHibernateの達人だ。君の助けになるはずだ。
* モニカ: ジョン、時間を取ってくれてありがとう。
  今、私たちが次なる目玉製品を開発しようとしてるのは知ってる？
  次のFacebookやGoogleになるつもりなの。
  忙しくなるわ。巨大なものになる。
  本当にすてき！
  みんなとても興奮してる！
  私はアーキテクトの役に就いたから、とりあえず採用する技術スタックを選定しなければいけないの。
  ひとつだけまだ欠けてるのが永続化なんだけど…
* ジョン: Hibernate！
* モニカ: そう！そのとおり！
  わたしもそう考えていたの！
  それならわたしたちにぴったりで上手く行きそうでしょう。
  マーケットと豊富な実績に裏付けられた、真の業務問題のための真の業務ソリューション。
  とてもたくさんのポジティブな経験談を聞いたことがあるわ。
  けど、一つ問題があって、チームメンバのひとりがそれに絶対反対してるの。
  アプリケーションとデータベースの間に別のレイヤを加えるのを気にして。
  彼はすごく頭がいいから、これが良い決断だと納得させるには本当にしっかりした根拠が必要なの。
  助けてくれる？
* ジョン: もちろん、よろこんで！
  Hibernateは、実際、すばらしいツールです。
  銀行といった、大きな真の業務ソリューションで広く使われています。
  それを使って失敗するということはありえません。
  永続化ときたらHibernate。
  Javaで書いているならそれが完全に正しい選択ですし、さらには他の言語への移植もあります。
  どれだけ多くの職務記述書がそれを要求しているか！
* モニカ: 全く同感！
  同じことを感じていたわ。
  前のプロジェクトで、ほとんどのところで生のJDBCからSQLを使っていたんだけど、ばかげてた！
  そうでしょ！
  けど、実は、ほんとに優秀なSQL屋がチームにいて、Hibernateが生成したSQLを見て神経質になってるの。
  きたなくて読みにくいって。
  これって将来問題になりそう？
* ジョン: 気を付けてください。DBA屋ってのは違ったものの見方をします。
  彼らはプロジェクトにおける自分の立場をHibernateに奪われるのではないかと危惧しています。
  さらに、データベースには組み込みのクエリ最適化機構があるので、クエリの実際の見た目がどんなかは気にする必要はありません。
  データベースが最適化してくれます。
  それが高速開発ってものです。
  SQLにはまねできません。
* モニカ: ほんとに？
  もうSQLを触らなくていいの？
  すごい！
  この前DBAがクエリの最適化に数週間かけていたわ。
  数週間！
  あぁ、こんなこと言うのは恥ずかしいんだけど、わたしたちが何を使っていたか分かる？
  …ストアドプロシージャ(笑)
  もうくちゃくちゃだった。
  そのプロジェクト、まだそれ使ってるって信じられる？
  そこの人たちほんとに気の毒だわ。
  未だにあんな退屈なコードを何度も何度も書かないといけないなんて。
  あれってJavaというかもうSQLプロジェクトじゃない？
* ジョン: それはまさにオブジェクト指向とリレーショナルのアプローチの違いです。
  いわゆるオブジェクト指向インピーダンスミスマッチですね。
  Hibernateはその溝を埋めてくれます。
  開発者はビジネスロジックの構築に専念できます。
  ステークホルダもマネージメント全体も幸せになれます。
  最も重要となることをしましょう。ビジネスです！
  ボイラープレートの多くは消え去り、魔法のようで目には見えませんが、ロジックとデータとの間にしっかりとしたコネクションができるのです。
* モニカ: 相互協調。充実したシナジー。
  まるでデータベースが最初から言語の一部だったかのよう。
  信念の技術的飛躍の指導者になれてとても幸せ。
  ソフトウェアという旅路でワープスピードに乗ったみたい。
* ジョン: そう！その調子！
* モニカ: わーい！すごーい！
  わくわくしてきた！たーのしー！
  ありがとうジョン。
  準備万端！

# 3年前、柔軟性のないソリューションとともに大きくなる苦悩
* モニカ: ねえジョン、去年話したプロジェクト覚えてる？
* ジョン: もちろん。調子はどうですか？
* モニカ: もうすぐリリースするわ。
  全て順調。だけどいくつか疑問がわいてきたの。
* ジョン: いいですよ。聞いてください。
* モニカ: ええと、もうデータベーススキーマを一から生成することはできないんだけど、データロスのないスキーマ変更をサポートするにはどうするのが一番いい？
* ジョン: えぇ、まず、Hibernateはプロダクション環境での移行ツールとして使われることを想定していません。
  FlywayDBやLiquibaseといったものを使うべきです。
  結構簡単ですよ。移行スクリプトを書いて、それでエンティティモデルを更新しつつ、Hibernateのマッピングも直して、
  実際のデータベース構造と同期するようにしてください。
* モニカ: ふーん、分かった。前のプロジェクトでは単に生のSQLで移行してた。
* ジョン: それでもいいと思います。エンティティモデルとスキーマが同期してさえいれば、好きなやり方でやってください。
* モニカ: そうね。
  もう一つ、わたしたちいつも遅延フェッチと即時フェッチの問題と戦ってるの。
  ある時、全部を即時でやることに決めたんだけど、それって最適じゃないでしょ？
  それに、たまにセッションが残ってないせいかなにかで、フィールドにアクセスできないことがあるの。
  それって普通？
* ジョン: もっとHibernateについて学ぶ必要があります。
  データベースとのマッピングは単純ではありません。
  複数のやりかたがあるのが普通です。
  その中から自分に合ったものを選ぶのです。
  遅延フェッチはオブジェクトを必要なときにロードできるようにしますが、アクティブなセッションの中で実行しないといけません。
* モニカ: わたしたちはまだ最終的なデプロイでどのデータベースエンジンを使うべきか迷ってるの。
  Hibernateってポータブルだと思ってたけど、MS SQLの魔法を使うためにちょっとネイティブクエリを使ってて、実際にはプロダクション環境ではMySQLで行きたいんだけど。
* ジョン: HibernateはdetachedなCriteriaクエリかHQLを使っている限りは柔軟です。
  ネイティブクエリを使ったらそのデータベースにソリューションが固定されちゃいますよ。
* モニカ: それならMS SQL専用にしないとダメみたいね。
  最後の質問。チームメンバからHQLには「limit」キーワードがないと聞いたわ。
  冗談かと思ったけど、わたしも見つけられなかった。
  バカな質問で申し訳ないんだけど…
* ジョン: 確かに。HQLには「limit」はありません。
  クエリオブジェクトでコントロールすることはできます。
  データベースベンダ依存のものなので。
* モニカ: 他の要素は全部HQLにあるのに変ね。
  まあ気にしないで。
  時間取ってくれてありがとう！

# 2年前、わたしたちは今再びSQLでソリューションをハックしている
* モニカ: ジョン、最初わたしたちSQLを触らないつもりだったけど、今はその必要があると感じてる。
  要件が大きくなってきていて、それを避ける手立てはないみたいなの。
  間違ったことをしているかもしれないけど、またSQLを毎日のように使い始めたわ。
* ジョン: いえ、それは間違っていません。
  最初期にはデータベースを気に掛ける必要はありませんでしたが、プロジェクトが進んだ今では、SQLを使ってパフォーマンスの最適化に取り組むのはいいことです。
* モニカ: ときどきエラーを調査するのに数日かかるの。
  なぜ期待通りに動かないのか、なぜ思いがけない結果が出力されるのかが全く分からないから、Hibernateが生成したSQLを解析しないといけないみたい。
  Hibernateのバグトラッカーに載ってる有名な問題に当たったこともある。
  それだけじゃない。エンティティモデルの同期を保ったまま適切な移行処理を書くのは難しいの。
  Hibernateの内部をよく調査して、どう動くのかを予測する必要があって、時間を取られてしまう。
* ジョン: 学習曲線というのは常にあります。
  たくさんの記述はいりませんが、どう動くかは知っておく必要があります。
* モニカ: 大きなデータセットを扱うのも厄介。
  最近データベースに大量のインポートをしたんだけど、あまりにも遅かった。
  あとで、速くするにはセッションをクリアする必要があったって分かったんだけど、それでもまだ全然遅い。
  だから生のSQLで書き直すことにしたの。
  笑ったわ。生のSQLを書くのが実際最速の方法だったから。
  だから最後の選択肢としてそうすることに決めたの。
* ジョン: インポートはオブジェクト指向な処理ではないです。
  Hibernateはオブジェクト指向設計に焦点を当てています。
  ネイティブクエリという選択肢を忘れてはいけません。
* モニカ: Hibernateのキャッシュがどう動くか知りたいんだけど、教えてくれる？
  ちょっと分からないの。
  一次キャッシュとか二次キャッシュとかあるけど、どういうものなの？
* ジョン: もちろんです。
  それはいわゆる永続データのトランザクションレベルキャッシュです。
  クラスタやJVMレベルで、クラス毎やコレクション毎のキャッシュを設定できます。
  クラスタキャッシュを組み込むことさえできます。
  しかし、キャッシュは他のアプリケーションが永続化領域に加えた変更については関知しないことを覚えておいてください。
  期限切れのキャッシュデータを定期的に消すように設定することはできますが。
* モニカ: ごめん。気分が悪くなってきた。
  もう少し説明してくれる？
* ジョン: はい。
  `save`とか`update`とか`saveOrUpdate`にオブジェクトを渡したり、`load`、`get`、`list`、`iterate`、`scroll`でオブジェクトを取得するときは常に、そのオブジェクトはセッションの内部キャッシュに追加されます。
  一次キャッシュからオブジェクトやそのコレクションを削除することもできます。
* モニカ: あぁ…
* ジョン: さらに、キャッシュモードを制御することもできます。
  `normal`モードでは読み込みと書き込みで二次キャッシュを使います。
  `get`モードでは二次から読みますがライトバックはできません。
  `put`は`get`と同じですが二次から読むことはできません。
  `refresh`モードもあります。
  これは二次に書き込みますが、そこからは読み込まず、`use minimal puts`プロパティを無視し、データベースからの全ての読み込み時に二次キャッシュを強制リフレッシュします。
* モニカ: いいわ。わかった。
  ちょっと考えさせて。
  もう遅いわ。行かなきゃ。
  説明ありがとう！
* ジョン: どういたしまして！

# 2週間前、Hibernateをあきらめる
* モニカ: ジョン、わたしソフトウェア開発の新時代に入ろうとしてるんだと思ってた。
  一光年の飛躍をしてるんだと思ってた。
  けど、4年たった今も、わたしたちは同じ問題に対応してるみたい。単に違う方向から。
  私はHibernateのアーキテクチャ、設定、ロギング、ネーミング戦略、Tuplizer、エンティティ名リゾルバ、拡張IDジェネレータ、IDジェネレータ最適化、ユニオンサブクラス、XDocletマークアップ、インデックス付きコレクションの双方向関連、3項関連、idbag、暗黙的ポリモーフィズムと他の継承マッピングの組み合わせ、二つの異なるデータストア間でのオブジェクトレプリケーション、detachedオブジェクトと自動バージョニング、コネクション開放モード、ステートレスセッションインターフェース、コレクション永続化の分類法、キャッシュレベル、遅延/即時フェッチ、他にもいろんなことを学ばなければならなかった。
  わたしの知ってる全てがあっても、ひどい失敗になっていたと思う。
  ソフトウェアの出来損ないだわ！
  究極の失敗！
  大参事！
  アルマゲドン！
* ジョン: 待ってください！なにがあったんですか？
* モニカ: わたしたち行き詰ったの。
  わたしたちのアプリケーションの性能はばかばかしいほど遅い！
  レポートを取得するのに二日も待たないといけない！
  二日でやっと顧客にダッシュボードを生成して見せられるの。
  つまり毎日計算処理を開始させなければならない上に、ダッシュボードの情報はどんどん遅れてしまう。
  うちのDBAエキスパートがクエリ最適化に2か月取り組んでるけど、データベース構造がめちゃくちゃで。
  それを手伝ってる開発者もいるけど、困ったことに、DBAはSQLで考えているから、開発者はそれをdetached CriteriaかHQLに翻訳しようと何日も費やしてしまうの。
  今となっては性能がかなり重要だから、できるだけネイティブSQLを使おうとしてるわ。
  なんにせよ、データベーススキーマがはっきり間違っちゃってるから大したことはできない。
  オブジェクト指向な視点ではそれでいいと感じていたけど、リレーショナルな視点では最悪だったみたい。
  どうしてこうなっちゃったんだろう？
  開発者はエンティティ構造を変えるのはかなりの労力になると言うから、それをする余裕はないし。
  前のプロジェクトは乱雑ではあったけど、そんな窮地には陥らなかった。
  既存のデータを処理する完全に別のアプリケーションを書くこともできた。
  今は、生成されたテーブルを変えるのは危険だわ。
  エンティティモデルが完全に正しく動くことを保証するのは本当に難しいもの。
  けどこれさえも最悪な点ってわけではないわ！
  性能改善するには、データベース問題だけでなく、データベースとアプリケーションの間のレイヤ全体の問題も解決しないといけない。
  それが圧倒的！
  この新しく加わった人たちはね、コンサルタントなの。
  彼らはデータを抽出して、なにか別のストレージに入れて、外側から計算を実行しようとしてる。
  どれも時間かかりすぎ！
* ジョン: なんと言っていいか分かりません。
* モニカ: いいのよジョン、あなたを責めはしないわ。
  わたしはHibernateを選択して全ての問題を解決しようとしたけど、今ではそれが銀の弾丸ではないと分かる。
  もうダメージは負ったし、それをなかったことにはできない。
  実は、あなたにお願いしたいことがあるの。
  わたしはこの4年間のキャリアをHibernateのあれこれとの戦いに費やしてしまったわ。
  もう今の会社でわたしに未来はないみたい。
  助けてくれない？

# 今日、学んだ教訓は？
* ジョン: やあピーター、モニカを紹介するよ。
* ピーター: やあモニカ！
  わたしたちは新しい次なる目玉を開発しようとしてるんだけどね。
  巨大なものになりそうだよ！
  Uberみたいになりたいんだ！
  永続化について何か知って…
* モニカ: Hibernateはダメ！

# まとめ
モニカはHibernateのエキスパートだ。
しかし、この例ではHibernateは間違った選択だった。
彼女のソリューションが以前より大きな問題に変化したと気付いたときには、プロジェクト全体を脅かす最大の脅威になってしまっていた。

データはアプリケーションの目的の中心で、好むと好まざるにかかわらず、アーキテクチャ全体に影響する。
このストーリーから学んだとおり、アプリケーションがデータベースを使うからとか、[ソーシャルプルーフ](http://d.hatena.ne.jp/keyword/%A5%BD%A1%BC%A5%B7%A5%E3%A5%EB%A5%D7%A5%EB%A1%BC%A5%D5)があるからというだけの理由でHibernateを選択してはいけない。
柔軟性をもつソリューションを選ぶべきだ。
堅牢なJDBCラッパには[JdbcTemplate](http://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/jdbc/core/JdbcTemplate.html)や[Fluent JDBC Wrapper](http://jdbc.jcabi.com/)といった多くの選択肢がある。
あるいは他にも、[jOOQ](http://www.jooq.org/)といった強力なソリューションがある。

----------------

以上がGrzegorzの記事。

ジョンにそそのかされて、Hibernateへの期待が高まるあまり一時けもの並の知能になったモニカが、4年の間に現実を知り絶望していくさまが生々しく怖い話だ。
オブジェクト指向の都合だけでデータベーススキーマを決めてしまった辺りが一番の失敗だったんだろうか。
SQL中心に考えつつHibernateでORマッピングやスキーマを構築することも、HibernateとSQL両方熟知してればできるんだろうか。

なんにせよ、Hibernateが忌み嫌われるようになった理由がよくわかる面白い記事だった。

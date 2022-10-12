モナレッジで書いた自分の記事をバックアップする2【python】

　SQLite3に保存する。問題あり。実行するたび自分の全記事のアクセス数が増加し、DBは全記事が更新されてしまう。

<!-- more -->

# ブツ

* [リポジトリ][]

[リポジトリ]:https://github.com/ytyaru/Python.Monaledge.Article.Backup.20221011111027

# 実行

```sh
ADDRESS='モナレッジに登録した自分のモナコイン用アドレス'
NAME='Python.Monaledge.Article.Backup.20221011111027'
git clone https://github.com/ytyaru/$NAME
cd $NAME/src
./run.py $ADDRESS
```

# 結果

　`monaledge.db`というSQLite3ファイルに保存される。

　使い方は前回参照。

* [][]

[]:

## 前回との差異

* [][]

[]:

* 変更判定を更新日時からタイトルに変えた
* 一部外部キー制約をなくした

### 変更判定を更新日時からタイトルに変えた

　前回考えた妥協案にした。

before
```python
def is_changed(self, id, updated): return not self._db.exists_article(id) or self._db.get_article_updated(id) < updated
```

after
```python
def is_changed(self, id, title): return not self._db.exists_article(id) or self._db.get_article_title(id) != title
```

### 一部外部キー制約をなくした

```sql
PRAGMA foreign_keys=true;
create table if not exists comments(
    id integer not null primary key,
    article_id integer not null,
    created integer not null,
    updated integer not null,
    user_id integer not null,
    content text not null
    --foreign key (article_id) references articles(id),
    --foreign key (user_id) references users(id)
);
```

　コメントアウトしてある外部キー制約をやめた。理由は一度にコミットしようとすると外部キー制約違反「FOREIGN KEY constraint failed」になるから。

　私としては`artciles`とそれにぶら下がるコメント`comments`を一括でコミットしたい。なぜならモナレッジAPI[artcile][]では本文とコメントが一緒に取得されるし、ファイルI/Oの頻度を減らして応答速度向上とディスク劣化を最小限に抑えたいから。

　本当は外部キー制約したい。コメントは記事という親にぶらさがるから、その関係をちゃんと制約として実装したかった。いい方法はないものか。

[article];

# 課題

　今回の実装だと、タイトルが更新されないかぎり他の項目は一切更新されない。コメントが付こうがモナがもらえようがアクセス数が増えようが一切更新されない。

* 何もしない（レコードが既存でタイトルが同じなら）
* UPSERT
	* 挿入（本文を含むすべて挿入）
	* 更新（本文を含むすべて更新）

　けど、前回は以下のようにする想定だった。

* レコードが存在しない
	* 挿入（本文を含むすべて挿入）
* レコードが存在する
	* タイトルが同じ
		* 更新（本文、タイトル、コメント以外の変更ある項目すべて更新）
	* タイトルが違う
		* 更新（本文を含むすべて更新）

　でもよく考えたらタイトルが同じときは本文だけでなくコメントも更新できない。なぜならコメントは本文と同じ[article][] APIで取得するから。[myArticles][]の中には入っていない。[myArticles][]の時点で本文、コメントそれぞれに更新があったか判定できる日時でもあれば[article][] API発行を必要最小限にできたのだが。

　そもそも目的は記事マークダウンのバックアップだった。せいぜい他にはタイトル、日時、カテゴリがあれば十分。それ以外の要素は最悪なくてもいい。本当はコメントも欲しいが、更新するには毎回[article][] APIを実行せねばならないので諦める。

　アクセス数やモナについては個別に変化があれば更新してもいい。それは[myArticles][]で取得できるので可能。

　こうなると更新処理は2種類に分かれる。UPSERT文では実装できない。

　すべてを更新するときは既存のUPSERTにあるUPDATE文を流用できる。けど、本文、タイトル、コメント以外の変更ある項目を更新する処理をどうするか。

項目|更新する|補足
----|--------|----
`created`|❌|変わらないはずなので更新不要
`updated`|？|アクセスがあっただけで更新されると思われる。記事、コメント、モナに変更がなくても。それははたして更新されたと判断すべきなのか？
`sent_mona`|⭕|
`access`|⭕|
`ogp_path`|⭕|
`category_id`|⭕|

　`updated`だけ更新すべきか迷う。条件付きで更新すればいいかもしれない。

* タイトルがDBと異なるときはすべて更新する（更新日時も含めて）
* タイトルが同じとき
	* `sent_mona`, `ogp_path`, `category_id`に変更があったとき
		* 更新日時も変更する

　本当はコメントが追加されたときも更新したいのだが、タイトルを変えないかぎり[article][] APIを発行しないためコメントに変化があったか判定できない。そこはもう諦めるしかない。それが嫌なら毎回全件更新するしかない。バックアップするたび全記事のアクセス数が増えてしまう。それを避けたくて今回タイトル変更された記事のみ対象にしたわけで。

　というか、本文またはコメントが更新されたかどうかは、それ以外（`sent_mona`,`access`,`ogp_path`,`category_id`）が更新されていないのに更新日時が変わったことでわかるのでは？

　もしそうなら[article][] APIを実行せずとも判断できる。

　次はそういう実装にしてみるか。


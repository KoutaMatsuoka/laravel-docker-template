# Laravel Lesson レビュー①

## Todo一覧機能

### Todoモデルのallメソッドで実行しているSQLは何か

  `select * from todos;`
  
### Todoモデルのallメソッドの返り値は何か

  `Illuminate\Database\Eloquent`内に記述のある`Collection`クラスのインスタンス

### 配列の代わりにCollectionクラスを使用するメリットは

  逐一インスタンス化して処理するため、大本のデータに手が加えられないまま残る点

### view関数の第1・第2引数の指定と何をしているか

  view関数は画面として表示したいHTMLを指定している
  第1引数には表示対象となるファイルを指定し、第2引数には渡したいデータを連装配列の形で代入する

### index.blade.phpの$todos・$todoに代入されているものは何か

  `$todos`にはControllerにて取得したCollectionインスタンスが、`$todo`には`foreach`で取り出したCollectionインスタンスに格納されているTodoインスタンスがそれぞれ格納されている

## Todo作成機能

### Requestクラスのallメソッドは何をしているか

  フォームから送信された値を一括で取得している

### fillメソッドは何をしているか

  `$todo->{連想配列のkey} = {連想配列のvalue}`を実行し、連想配列で取得した値をTodoインスタンスの各プロパティに一括で代入している

### $fillableは何のために設定しているか

  一括代入の際に悪意のある攻撃の影響を受けぬよう`fill()`によってModelに代入可能なプロパティを制限するため

### saveメソッドで実行しているSQLは何か

  `INSERT INTO todos (id, content, created_at, updated_at) VALUES ();`

### redirect()->route()は何をしているか

  `route()`の引数で指定したルートにリダイレクト先を設定している

## その他

### テーブル構成をマイグレーションファイルで管理するメリット

  マイグレーションファイルを開発者各員で共有することで同一の状態から作業を開始できる点・SQLを介さずDB運用が可能となるため学習コストの低減に繋がる点

### マイグレーションファイルのup()、down()は何のコマンドを実行した時に呼び出されるのか

  `up()`は`php artisan migrate`、`down()`は`php artisan migrate:rollback`の実行によりそれぞれ呼び出される

### Seederクラスの役割は何か

  誰が実行しても同一の条件となるテストデータの定義
  今回は連装配列形式によるテストデータの設定及びその投入処理、そしてテストデータ実行以前のデータを削除する処理を纏めて設定している

### route関数の引数・返り値・使用するメリット

  定義した名前付きルートの名称を`route()`の引数に渡すことで返り値としてURLを取得する。
  Bladeファイルの記述が短くなるために可読性の向上が期待できるほか、ルート名に変更がなければ修正箇所を削減することができるため保守性の向上にもつながる。

### @extends・@section・@yieldの関係性とbladeを分割するメリット

  @extends`にて継承する親ファイルを指定し、`@section`と`@endsection`で挟んだ範囲を親ファイルの`@yield`に代入することで一つのHTMLファイルとして表示ができる。  共通するHTMLの記述を一元管理し、それぞれに代入することでファイルごとの可読性や保守性を向上させることができる

### @csrfは何のための記述か

  CSRF攻撃対策のための記述、トークンを発行している

### {{ }}とは何の省略系か

  `<?php= ?>`

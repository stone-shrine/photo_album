# README
# アプリケーション名


<br>

# アプリケーション概要
このアプリケーションでできることを記載。

<br>

# URL
デプロイ済みのURLを記載。デプロイが済んでいない場合は、デプロイが完了次第記載すること。

<br>

# テスト用アカウント
ログイン機能等を実装した場合は、ログインに必要な情報を記載。またBasic認証等を設けている場合は、そのID/Passも記載すること。

<br>

# 利用方法
このアプリケーションの利用方法を記載。説明が長い場合は、箇条書きでリスト化すること。

<br>

# アプリケーションを作成した背景
このアプリケーションを通じて、どのような人の、どのような課題を解決しようとしているのかを記載。

<br>

# 洗い出した要件
要件定義をまとめたスプレッドシートのリンクを記載。

<br>

# 実装した機能についての画像やGIFおよびその説明
実装した機能について、それぞれどのような特徴があるのかを列挙する形で記載。画像はGyazoで、GIFはGyazoGIFで撮影すること。

<br>

# 実装予定の機能
洗い出した要件の中から、今後実装予定の機能がある場合は、その機能を記載。

<br>

# データベース設計
![ER_Figure](https://user-images.githubusercontent.com/122013996/220292200-44595782-7476-4d29-beb3-0ebeeb7066f4.png)

<br>

# 画面遷移図
![画面遷移図](https://user-images.githubusercontent.com/122013996/220062938-d2e53d80-fa80-4d60-9a9b-fb26672232f6.png)

<br>

# 開発環境
使用した言語・サービスを記載。

<br>

# ローカルでの動作方法
git cloneしてから、ローカルで動作をさせるまでに必要なコマンドを記載。

<br>

# 工夫したポイント




<br><br><br><br>

# テーブル設計
## Usersテーブル
| Column             | Type   | Options     |
| ------------------ | ------ | ----------- |
| name               | string | null: false |
| email              | string | null: false |
| encrypted_password | string | null: false |

### Association
has_many :comments  
has_many :photos  
has_many :friends  
has_many :albums, through: :user_albums

<br><br>

## Commentsテーブル
| Column  | Type       | Options                        |
| ------- | ---------- | ------------------------------ |
| user    | references | null: false, foreign_key: true |
| photo   | references | null: false, foreign_key: true |
| content | text       | null: false                    |

### Association
belongs_to :user  
belongs_to :photo

<br><br>

## Friendsテーブル
| Column    | Type       | Options                                                      |
| --------- | ---------- | ------------------------------------------------------------ |
| user_id   | references | null: false, foreign_key: true, unique: true                 |
| friend_id | references | null: false, foreign_key: { to_table: :users }, unique: true |

### Association
belongs_to :user

<br><br>

## Photosテーブル
| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |

### Association
belongs_to :user  
has_many :comments  
has_many :albums, through: :photo_albums

<br><br>

## Albumsテーブル
| Column | Type   | Options     |
| ------ | ------ | ----------- |
| name   | string | null: false |

### Association
has_many :users, through: :user_albums  
has_many :photos, through: :photo_albums

<br><br>

## Tagsテーブル
| Column | Type   | Options     |
| ------ | ------ | ----------- |
| tag    | string | null: false |

### Association
has_many :photos, through: :photo_tags

<br><br>

## User_Albumsテーブル
| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| user   | references | null: false, foreign_key: true |
| album  | references | null: false, foreign_key: true |

### Association
belongs_to :user  
belongs_to :album

<br><br>

## Photo_Albumsテーブル
| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| photo  | references | null: false, foreign_key: true |
| album  | references | null: false, foreign_key: true |

### Association
belongs_to :photo  
belongs_to :album

<br><br>

## Photo_Tagsテーブル
| Column | Type       | Options                        |
| ------ | ---------- | ------------------------------ |
| photo  | references | null: false, foreign_key: true |
| tag    | references | null: false, foreign_key: true |

### Association
belongs_to :photo  
belongs_to :tag

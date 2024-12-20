# README

### Users テーブル

| Column          | Type         | Options                        |
|-----------------|--------------|--------------------------------|
| id | INTEGER | primary key, auto_increment |
| username        | STRING  | NOT NULL               |
| email           | STRING | UNIQUE, NOT NULL               |
| encrypted_password  | STRING | NOT NULL                       |
| last_name       | STRING  | NOT NULL                       |
| first_name      | STRING  | NOT NULL                       |
| last_name_kana  | STRING  | NOT NULL                       |
| first_name_kana | STRING  | NOT NULL                       |
| birth_date      | date         | NOT NULL                       |


### Association
has_many :products
has_many :purchases

### Products テーブル

| Column            | Type         | Options                        |
|-------------------|--------------|--------------------------------|

| name              | STRING | NOT NULL                       |
| description       | text         | NOT NULL                       |
| price             | INTEGER(10,2)| NOT NULL                       |
| user         | references      | FOREIGN KEY, NOT NULL          |
| category_id          | INTEGER  | NOT NULL                       |
| condition_id         | INTEGER  | NOT NULL                       |
| shipping_fee_payer_id| INTEGER  | NOT NULL                       |
| prefecture_id   | INTEGER  | NOT NULL                       |
| shipping_day_id     | INTEGER  | NOT NULL                       |


### Association
belongs_to :user, foreign_key: :seller_id
has_one :purchase

### Purchases テーブル

| Column              | Type         | Options                        |
|---------------------|--------------|--------------------------------|
| user            | references      | FOREIGN KEY, NOT NULL          |
| product          | references      | FOREIGN KEY, NOT NULL  |

### Association
belongs_to :user
belongs_to :product
has_one :shipping_address


### ShippingAddresses テーブル

| Column         | Type         | Options                        |
|----------------|--------------|--------------------------------|

| purchase    | references      | FOREIGN KEY, NOT NULL          |
| postal_code    | STRING  | NOT NULL                       |
| prefecture_id     |  INTEGER | NOT NULL                       |
| city           | STRING | NOT NULL                       |
| address_line1  | STRING | NOT NULL                       |
| address_line2  |STRING |                                |
| phone_number   | STRING  | NOT NULL |

### Association
belongs_to :purchase

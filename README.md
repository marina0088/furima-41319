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
has_many :products, dependent: :destroy
has_many :purchases, dependent: :destroy

### Products テーブル

| Column            | Type         | Options                        |
|-------------------|--------------|--------------------------------|
| id                | INTEGER      | PRIMARY KEY, AUTO_INCREMENT    |
| name              | STRING | NOT NULL                       |
| description       | TEXT         | NOT NULL                       |
| price             | DECIMAL(10,2)| NOT NULL                       |
| stock             | INTEGER      | NOT NULL, DEFAULT 0             |
| seller_id         | INTEGER      | FOREIGN KEY, NOT NULL          |
| category          | STRING  | NOT NULL                       |
| condition         | STRING  | NOT NULL                       |
| shipping_fee_payer| STRING  | NOT NULL                       |
| prefecture_id   | STRING  | NOT NULL                       |
| shipping_days     | STRING  | NOT NULL                       |
| image_url         | STRING | NOT NULL                       |
# | created_at        | DATETIME     | DEFAULT CURRENT_TIMESTAMP      |
# | updated_at        | DATETIME     | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

### Association
belongs_to :user, foreign_key: :seller_id
has_one :purchase, dependent: :destroy

### Purchases テーブル

| Column              | Type         | Options                        |
|---------------------|--------------|--------------------------------|
| id                  | INTEGER      | PRIMARY KEY, AUTO_INCREMENT    |
| user_id             | INTEGER      | FOREIGN KEY, NOT NULL          |
| product_id          | INTEGER      | FOREIGN KEY, UNIQUE, NOT NULL  |
| purchase_date       | DATETIME     | DEFAULT CURRENT_TIMESTAMP      |
| shipping_address_id | INTEGER      | FOREIGN KEY, NOT NULL          |

### Association
belongs_to :user
belongs_to :product
has_one :shipping_address, dependent: :destroy


### ShippingAddresses テーブル

| Column         | Type         | Options                        |
|----------------|--------------|--------------------------------|
| id             | INTEGER      | PRIMARY KEY, AUTO_INCREMENT    |
| purchase_id    | INTEGER      | FOREIGN KEY, NOT NULL          |
| postal_code    | STRING  | NOT NULL                       |
| prefecture_id     | STRING  | NOT NULL                       |
| city           | STRING | NOT NULL                       |
| address_line1  | STRING | NOT NULL                       |
| address_line2  |STRING |                                |
| recipient_name | STRING | NOT NULL                       |
| phone_number   | STRING  | NOT NULL |

### Association
belongs_to :purchase






This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

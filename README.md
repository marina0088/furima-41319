# README

### Users テーブル

| Column          | Type         | Options                        |
|-----------------|--------------|--------------------------------|
| id              | INTEGER      | PRIMARY KEY, AUTO_INCREMENT    |
| username        | VARCHAR(50)  | UNIQUE, NOT NULL               |
| email           | VARCHAR(100) | UNIQUE, NOT NULL               |
| password_digest  | VARCHAR(255) | NOT NULL                       |
| last_name       | VARCHAR(50)  | NOT NULL                       |
| first_name      | VARCHAR(50)  | NOT NULL                       |
| last_name_kana  | VARCHAR(50)  | NOT NULL                       |
| first_name_kana | VARCHAR(50)  | NOT NULL                       |
| birth_date      | DATE         | NOT NULL                       |
| created_at      | DATETIME     | DEFAULT CURRENT_TIMESTAMP      |
| updated_at      | DATETIME     | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

### Association
has_many :products, dependent: :destroy
has_many :purchases, dependent: :destroy

### Products テーブル

| Column            | Type         | Options                        |
|-------------------|--------------|--------------------------------|
| id                | INTEGER      | PRIMARY KEY, AUTO_INCREMENT    |
| name              | VARCHAR(100) | NOT NULL                       |
| description       | TEXT         | NOT NULL                       |
| price             | DECIMAL(10,2)| NOT NULL                       |
| stock             | INTEGER      | NOT NULL, DEFAULT 0             |
| seller_id         | INTEGER      | FOREIGN KEY, NOT NULL          |
| category          | VARCHAR(50)  | NOT NULL                       |
| condition         | VARCHAR(50)  | NOT NULL                       |
| shipping_fee_payer| VARCHAR(50)  | NOT NULL                       |
| shipping_origin   | VARCHAR(50)  | NOT NULL                       |
| shipping_days     | VARCHAR(50)  | NOT NULL                       |
| image_url         | VARCHAR(255) | NOT NULL                       |
| created_at        | DATETIME     | DEFAULT CURRENT_TIMESTAMP      |
| updated_at        | DATETIME     | DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP |

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
| postal_code    | VARCHAR(10)  | NOT NULL                       |
| prefecture     | VARCHAR(50)  | NOT NULL                       |
| city           | VARCHAR(100) | NOT NULL                       |
| address_line1  | VARCHAR(255) | NOT NULL                       |
| address_line2  | VARCHAR(255) |                                |
| recipient_name | VARCHAR(100) | NOT NULL                       |
| phone_number   | VARCHAR(20)  |                                |

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

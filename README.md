# airbnb-clone-project
# Team Roles
# Technology Stack
# Database Design
# Feature Breakdown
# API Security
# CI/CD Pipeline
# requirements.md
erDiagram
    User {
        UUID user_id PK
        VARCHAR first_name NOT NULL
        VARCHAR last_name NOT NULL
        VARCHAR email UNIQUE NOT NULL
        VARCHAR password_hash NOT NULL
        VARCHAR phone_number
        ENUM role NOT NULL
        TIMESTAMP created_at DEFAULT CURRENT_TIMESTAMP
    }

    Property {
        UUID property_id PK
        UUID host_id FK
        VARCHAR name NOT NULL
        TEXT description NOT NULL
        VARCHAR location NOT NULL
        DECIMAL pricepernight NOT NULL
        TIMESTAMP created_at DEFAULT CURRENT_TIMESTAMP
        TIMESTAMP updated_at ON UPDATE CURRENT_TIMESTAMP
    }

    Booking {
        UUID booking_id PK
        UUID property_id FK
        UUID user_id FK
        DATE start_date NOT NULL
        DATE end_date NOT NULL
        DECIMAL total_price NOT NULL
        ENUM status NOT NULL
        TIMESTAMP created_at DEFAULT CURRENT_TIMESTAMP
    }

    Payment {
        UUID payment_id PK
        UUID booking_id FK
        DECIMAL amount NOT NULL
        TIMESTAMP payment_date DEFAULT CURRENT_TIMESTAMP
        ENUM payment_method NOT NULL
    }

    Review {
        UUID review_id PK
        UUID property_id FK
        UUID user_id FK
        INTEGER rating NOT NULL
        TEXT comment NOT NULL
        TIMESTAMP created_at DEFAULT CURRENT_TIMESTAMP
    }

    Message {
        UUID message_id PK
        UUID sender_id FK
        UUID recipient_id FK
        TEXT message_body NOT NULL
        TIMESTAMP sent_at DEFAULT CURRENT_TIMESTAMP
    }

    User ||--o{ Property : hosts
    User ||--o{ Booking : books
    Property ||--o{ Booking : has
    Booking ||--o{ Payment : has
    Property ||--o{ Review : has
    User ||--o{ Review : writes
    User ||--o{ Message : sends
    User ||--o{ Message : receives

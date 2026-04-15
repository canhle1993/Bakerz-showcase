# Bakerz Bite Showcase

Public showcase repository for the **Bakerz Bite** project.

## At A Glance

**Bakerz Bite** is a Laravel-based bakery e-commerce web application that combines customer shopping flows, health-based product suggestions, reward experiences, and admin-side operations in one system.

- Project type: Team-based academic capstone / real product showcase
- My role: Full-stack contributor focused on client experience, feature implementation, admin modules, and deployment support
- Main stack: Laravel 11, PHP 8.2, Blade, Bootstrap, jQuery, MySQL / MariaDB
- Live demo: [http://103.153.72.209/](http://103.153.72.209/)
- Demo video: [YouTube walkthrough](https://www.youtube.com/watch?v=FIMq_x9z6Uc&t=4s)
- Recognition: [Featured by Aptech Vietnam](https://aptechvietnam.com.vn/san-pham-hoc-vien/website-ban-banh-va-ca-phe-truc-tuyen-tien-loi-bakerz-bite/)

## Quick Links

- [My Contributions](#my-contributions)
- [What Makes This Project Notable](#what-makes-this-project-notable)
- [Live Links](#live-links)
- [Screenshots](#screenshots)
- [System Flow](#system-flow)
- [Repository Structure](#repository-structure)
- [Private Source Code Note](#private-source-code-note)
- [Supporting Documents](#supporting-documents)

## Overview

Bakerz Bite is a bakery e-commerce web application built with Laravel. The project combines customer shopping flows, health-based product suggestions, order processing, reward-based experiences, and admin-side management tools in one system.

This public repository is designed for recruiters, interviewers, and reviewers who want to quickly understand the project without accessing the private production source code.

## My Contributions

- Designed and implemented major customer-facing pages, including the homepage and product presentation flows
- Built core shopping-related features such as category browsing, cart data handling, and order history
- Developed the health-based product suggestion experience based on BMI and selected health conditions
- Implemented promotional and engagement modules such as Deal of the Day, best-seller content, Workshop, Blog, Our Chef, Coming Soon, and Bakerz Bite Rewards
- Contributed to admin-side functionality, including Power BI reporting, healthy-type management, and product quantity management
- Supported feature integration, UI behavior fixes, CI/CD deployment flow, and overall project completion across both client and admin areas

## What Makes This Project Notable

- Health-based product suggestion flow using BMI and selected health conditions
- VNPay integration for online payment processing
- Power BI dashboard reporting for admin-side analytics
- CI/CD deployment pipeline using GitHub Actions and server automation
- Full end-to-end flow across both client-facing and admin-facing modules

## Live Links

- Live Demo: [http://103.153.72.209/](http://103.153.72.209/)
- Project Demo Video: [https://www.youtube.com/watch?v=FIMq_x9z6Uc&t=4s](https://www.youtube.com/watch?v=FIMq_x9z6Uc&t=4s)
- Featured Project Article: [https://aptechvietnam.com.vn/san-pham-hoc-vien/website-ban-banh-va-ca-phe-truc-tuyen-tien-loi-bakerz-bite/](https://aptechvietnam.com.vn/san-pham-hoc-vien/website-ban-banh-va-ca-phe-truc-tuyen-tien-loi-bakerz-bite/)

## Highlights

- Customer-facing bakery storefront with category-based browsing
- Product detail pages with image galleries and reviews
- Health-based meal suggestion flow using BMI and selected health conditions
- Deal of the Day and Coming Soon product areas
- Customer profile, order tracking, and reward-based workshop access
- Admin-side product, order, discount, and promotional management
- Power BI integration for dashboard reporting
- VNPay integration for payments
- CI/CD deployment to server using GitHub Actions

## Tech Stack

- Backend: Laravel 11, PHP 8.2
- Frontend: Blade, Bootstrap, jQuery
- Database: MySQL / MariaDB
- Reporting: Power BI Embed
- Payment: VNPay
- Maps: Embedded map on contact page
- Deployment: GitHub Actions, SSH-based server deployment

## Deployment Workflow

- The project uses GitHub Actions for deployment automation
- On push to the `master` branch, a workflow connects to the server via SSH and updates the deployed application
- The deployment flow includes pulling the latest code and clearing Laravel configuration and application cache

## Recognition

- Bakerz Bite was featured by Aptech Vietnam as one of the representative student projects for Semester 1
- Public article: [Website bán bánh và cà phê trực tuyến tiện lợi - Bakerz Bite](https://aptechvietnam.com.vn/san-pham-hoc-vien/website-ban-banh-va-ca-phe-truc-tuyen-tien-loi-bakerz-bite/)

## Screenshots

### Home Hero

![Home Hero](docs/screenshots/home-hero.png)

### Health-Based Suggestion Form

![Health Filter Form](docs/screenshots/health-filter-form.png)

### Health-Based Suggestion Results

![Health Filter Results](docs/screenshots/health-filter-results.png)

### Customer Profile And Orders

![Customer Profile](docs/screenshots/profile-orders.png)

### Admin Order Management

![Admin Order Management](docs/screenshots/admin-order-management.png)

### Power BI Dashboard

![Power BI Dashboard](docs/screenshots/powerbi-dashboard.png)

## System Flow

The full system flow is available in:

- [system-flow.html](system-flow.html)

GitHub can also render the Mermaid diagrams directly in this README.

### Authentication Flow

```mermaid
flowchart LR
    A([User Access]) --> B{"Already logged in?"}
    B -- "No" --> C["Login Page"]
    B -- "Yes" --> D{"role_id?"}
    C --> E["POST /login"]
    E --> F{"Authentication"}
    F -- "Failed" --> C
    F -- "Success" --> D
    D -- "role=1 Client" --> G([Storefront])
    D -- "role=2 Admin" --> H([Admin Dashboard])

    C2["Register Page"] --> R["POST /register"]
    R --> R1{"Validate\n@gmail.com only"}
    R1 -- "Error" --> C2
    R1 -- "OK" --> R2["Create user\nrole_id=1\nrank=Bronze"]
    R2 --> R3["Send verification\nemail"]
    R3 --> G
```

### Client Shopping Flow

```mermaid
flowchart TD
    HOME([Home Page /filter]) --> HF["Select health\nconditions / BMI"]
    HOME --> BS["Best Sellers"]
    HOME --> SP["Seasonal Products"]
    HOME --> CP["Coffee and Espresso"]
    HOME --> DEAL["Deal of the Day"]
    HOME --> CS["Coming Soon"]

    HF -->|"health tag AND logic"| PRODUCTS

    SEARCH(["Search /search"]) --> PRODUCTS
    CAT(["Category Filter /shop/category"]) --> PRODUCTS

    PRODUCTS["Product Listing"] --> QV["Quick View\nAJAX modal"]
    PRODUCTS --> PD["Product Detail\nproductsingle/{id}"]

    PD --> REVIEW["Submit Review\n1-5 stars"]
    PD --> WISH["Wishlist\nPOST /add-to-wishlist"]
    PD --> ADDCART["Add to Cart\nPOST /cart/new_add"]

    ADDCART --> CARTDB[("cart table")]
    ADDCART --> CARTSESSION[("Session cart")]
    CARTDB <-->|"getsession sync"| CARTSESSION

    CARTSESSION --> CARTPAGE["Cart Page\n/cart/show"]
    CARTPAGE --> UPDATEQTY["Update quantity"]
    CARTPAGE --> DELITEM["Remove item"]
    CARTPAGE --> CHECKOUT["Checkout\n/showcheckout"]

    CHECKOUT --> CHKINV{"Inventory\navailable?"}
    CHKINV -- "Out of stock" --> CARTPAGE
    CHKINV -- "OK" --> CREATEORDER["Create Order\nstatus=Pending"]
    CREATEORDER --> ORDERDETAILS["Create OrderDetails"]
    CREATEORDER --> INVENTORY["Decrease product\ninventory"]
    CREATEORDER --> NOTIF["Create Notification\ntype=order"]
    CREATEORDER --> VNP["Redirect to VNPay"]

    VNP --> VNPRETURN{"vnp_ResponseCode?"}
    VNPRETURN -- "00 Success" --> PAID["Order status = Paid"]
    VNPRETURN -- "Other" --> FAILED["Payment Failed"]
    PAID --> PROFILE
    FAILED --> PROFILE

    PROFILE([Profile /client/profile]) --> ORDERS["Orders by\nstatus tab"]
    ORDERS --> CANCELBTN["Cancel order"]
    ORDERS --> RECHECK["Repay order"]
```

### Order Lifecycle

```mermaid
stateDiagram-v2
    [*] --> Pending : Client checkout / VNPay redirect
    Pending --> Paid : VNPay callback success or admin confirm
    Paid --> Confirmed : Admin confirms order
    Confirmed --> Delivered : Admin marks delivered
    Delivered --> [*]

    Pending --> Cancel : Client or admin cancels
    Paid --> Cancel : Admin cancels
    Cancel --> [*]
```

### Rank And Rewards Flow

```mermaid
flowchart LR
    REG([Register account]) --> BR["Bronze\ndefault rank"]
    BR -->|"Earn points\nvia purchases"| GO["Gold"]
    GO -->|"Earn more\npoints"| DI["Diamond"]

    BR --> DISC_BR["Discount\nBronze level"]
    GO --> DISC_GO["Discount\nGold level"]
    DI --> DISC_DI["Discount\nDiamond level"]
    DI --> WORKSHOP["Workshop\nRegistration\nDiamond only"]

    WORKSHOP --> WSTATUS{"Admin review"}
    WSTATUS -- Approved --> WS_OK["Approved"]
    WSTATUS -- Cancelled --> WS_CANCEL["Cancelled"]
```

### Health-Based Product Filter

```mermaid
flowchart TD
    CLIENT([Client]) --> BMI["Enter height and weight\nBMI calculation"]
    BMI --> BMI_CALC["JS calculates BMI\nauto-select weight tag"]
    CLIENT --> MANUAL["Manually select\nhealth conditions"]
    BMI_CALC --> SELECT["health_id selection"]
    MANUAL --> SELECT

    SELECT --> QUERY["Query link_product_heathy\nAND logic\nCOUNT DISTINCT = selected tags"]
    QUERY --> RESULT["Matched Products"]

    ADMIN_H([Admin]) --> HEATHY_MGMT["Manage Healthy Types"]
    HEATHY_MGMT --> HEATHY_TABLE[("heathy_catalog table")]
    HEATHY_TABLE --> LINK[("link_product_heathy pivot")]
    PRODUCT_MGMT["Manage Products"] --> LINK
```

### Admin Management Overview

```mermaid
flowchart TD
    DASH([Admin Dashboard\nPower BI + Notifications]) --> PM["Product Management"]
    DASH --> OM["Order Management"]
    DASH --> UM["User Management"]
    DASH --> CM["Category Management"]
    DASH --> DM["Discount Management"]
    DASH --> BM["Banner Management"]
    DASH --> CHEF["Chef Management"]
    DASH --> BLOG["Blog Management"]
    DASH --> DEAL["Deal of the Day"]
    DASH --> SOON["Coming Soon"]
    DASH --> WS["Workshop Management"]
    DASH --> CONTACT["Contact Messages"]
    DASH --> SM["Social Media"]
    DASH --> REVIEW["Review Management"]

    PM --> STOCK["Stock Management"]
    STOCK --> INSTOCK["In Stock"]
    STOCK --> OUTSTOCK["Out of Stock"]
    STOCK --> CHECKSTOCK["Check Stock"]

    NOTIF_O["Order Notification"] -->|"sidebar bell"| DASH
    NOTIF_R["Review Notification"] -->|"sidebar bell"| DASH
```

### Database Relationships

```mermaid
erDiagram
    user {
        int user_id PK
        string name
        string email
        int role_id FK
        string rank
        int score
        int isdelete
    }
    product {
        int product_id PK
        string product_name
        int inventory
        decimal price
        string status
        int isdelete
    }
    order {
        int order_id PK
        int user_id FK
        decimal total
        decimal pay
        string status
        string delivery_address
    }
    orderdetails {
        int id PK
        int order_id FK
        int product_id FK
        int quantity
        decimal selling_price
        decimal discount
    }
    cart {
        int id PK
        int user_id FK
        int product_id FK
        int quantity
    }
    category {
        int category_id PK
        string category_name
        int isdelete
    }
    heathy_catalog {
        int heath_id PK
        string name
        int isdelete
    }
    discount {
        int discount_id PK
        string discount_name
        decimal discount
        int isdelete
    }
    notifications {
        int id PK
        int user_id FK
        int order_id FK
        int review_id FK
        string type
        int is_read
    }
    userreview {
        int ID PK
        int user_id FK
        int product_id FK
        int ratestar
        string comment
        int is_deleted
    }
    workshop {
        int id PK
        int user_id FK
        string product
        string status
        int isdelete
    }

    user ||--o{ order : places
    user ||--o{ cart : has
    user ||--o{ userreview : writes
    user ||--o{ workshop : registers
    order ||--o{ orderdetails : contains
    product ||--o{ orderdetails : in
    product ||--o{ cart : in
    product ||--o{ userreview : receives
    product }o--o{ category : linkcatalogproduct
    product }o--o{ heathy_catalog : link_product_heathy
    product }o--o{ discount : discountproduct
```

### CI/CD Deployment Flow

```mermaid
flowchart LR
    DEV([Developer]) -->|"git push master"| GH["GitHub\nmaster branch"]
    GH -->|"trigger"| GHA["GitHub Actions\ndeploy.yml"]
    GHA -->|"SSH connect"| SERVER["Production Server"]
    SERVER -->|"git pull"| CODE["Update codebase"]
    CODE -->|"php artisan"| CLEAR["config:clear\ncache:clear"]
    CLEAR --> LIVE([Live Site])
```

## Repository Structure

- `system-flow.html`: full interactive system flow documentation
- `docs/screenshots`: UI screenshots used in this showcase
- `docs/features`: feature summaries
- `docs/api`: public-facing route and API notes
- `docs/demo`: links for live demo or video demo
- `docs/deployment`: stack and deployment notes
- `portfolio`: project summary, responsibilities, and technical reflections

## What Is Public Here

- Product summary
- Feature overview
- System flow documentation
- Selected screenshots
- Portfolio and presentation materials

## What Is Not Included

- Full backend source code
- Full frontend source code
- Environment files or secrets
- Production configuration
- Internal implementation details that belong to the private repository

## Private Source Code Note

The full source code for Bakerz Bite is private.

This repository is intentionally used as a public showcase for architecture, features, UI evidence, and individual contribution summary.

If you are a recruiter, interviewer, or reviewer and would like a deeper walkthrough, I can provide:

- a live demo
- a guided screen-sharing session
- additional implementation details upon request

## Supporting Documents

- Feature summaries: [docs/features](docs/features)
- System flow: [system-flow.html](system-flow.html)
- Project portfolio notes: [portfolio](portfolio)
- Live demo details: [docs/demo/demo-link.md](docs/demo/demo-link.md)
- Video demo details: [docs/demo/video-link.md](docs/demo/video-link.md)

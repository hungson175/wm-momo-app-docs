# MoMo App - UI/UX Design Specification 

**Document Version:** 1.1
**Date:** June 26, 2025
**Target Platforms:** Android & iOS (Web-mobile app, Not native )

---

## 1.0 Overview & Core Concepts

MoMo is a digital wealth management and micro-investing application in Vietnam. It aims to make investing accessible, simple, and automated for a young, tech-savvy demographic, including first-time investors.

### 1.1 Target Audience
* Young professionals and millennials in Vietnam.
* Novice to intermediate investors looking for a low-barrier-to-entry platform.
* Users interested in building long-term wealth through savings and diversified investments.

### 1.2 Core Products
The app revolves around several key financial products:
* **Fund Certificates (Chứng chỉ quỹ):** The core offering, allowing users to invest in diversified portfolios managed by professional fund companies.
* **Stock Trading (Chứng khoán):** Direct buying and selling of individual stocks on the Vietnamese stock market.
* **Structured Savings (Tích lũy):** Goal-oriented savings products like HayBond with competitive interest rates.
* **IPO Access (Săn IPO):** A feature to discover and participate in Initial Public Offerings.
* **Child Accounts (Cho con):** A feature to save and invest for children.

### 1.3 Design Philosophy
* **Theme:** Bright, clean, and user-friendly light mode theme. This creates an approachable and clear financial overview, making financial data feel less intimidating.
* **Clarity:** Use of clear typography, generous white space, and a structured layout with defined cards to make complex financial data easy to digest.
* **Visualization:** Heavy reliance on charts (area charts, donut charts, line charts) to visually represent portfolio performance and allocation.
* **Gamification:** Use of symbolic "mascots" for investment profiles to make risk assessment more relatable and less intimidating.

---

## 2.0 Global UI Elements & Design System (MoMo Inspired)

These are recurring elements that define the app's visual identity, based on a light, pink-accented theme.

### 2.1 Color Palette
* **Primary Background:** White (`#FFFFFF`).
* **Card/Surface Background:** White (`#FFFFFF`), typically with a very subtle, light grey border (e.g., `#F0F0F0`) or a soft drop shadow to create separation. Some primary cards may feature a light gradient.
* **Primary Accent (Positive/CTA):** Vibrant Pink/Magenta (e.g., `#E5007A`). Used for primary action buttons (`Buy`, `Purchase`), active tab backgrounds, and key highlights.
* **Positive Indicator:** Bright Green (e.g., `#00C782`). Used exclusively for displaying profit figures and positive percentage changes (e.g., `+8.33%`).
* **Secondary Accent (Negative):** Bright Red (e.g., `#FF453A`). Used for loss figures and negative data changes.
* **Tertiary Accents:**
    * **Blue, Orange, Purple, Teal:** Used in charts for categorical data.
* **Primary Text:** Dark Gray/Near Black (e.g., `#222222`).
* **Secondary Text/Labels:** Medium Gray (e.g., `#8A8A8E`).

### 2.2 Typography
A clean, modern, sans-serif font (e.g., SF Pro, Roboto) should be used throughout the app.
* **Screen Title:** Medium-to-Bold weight, Dark Gray. (e.g., 20pt Bold).
* **Value/Hero Numbers:** Large, Regular/Light weight, Dark Gray. (e.g., 32pt).
* **Card Title:** Medium-to-Bold weight, Dark Gray. (e.g., 17pt Bold).
* **Body Text:** Regular, Dark Gray. (e.g., 16pt).
* **Labels/Subtitles:** Small, Regular, Medium Gray. (e.g., 14pt).
* **Button Text:** Medium weight. `White` for solid pink buttons; `Pink` for outline-style buttons.

### 2.3 Core Components
* **Bottom Navigation Bar:** A standard 5-tab bar. The active tab is indicated by a **Pink** icon and label. Inactive tabs are gray.
* **Cards:** The primary container for content. They feature rounded corners, a white background, and a subtle light grey border or shadow to lift them off the main white background.
* **Buttons:**
    * **Primary CTA (e.g., "Mua" / "Buy"):** Solid **Pink** background with **White** text.
    * **Secondary CTA (e.g., "Bán" / "Sell"):** Transparent background with a **Pink** border and **Pink** text.
* **Segmented Controls:** Used for switching views or filtering. The selected segment has a solid **Pink** background with **White** text. Unselected segments have a light grey background with dark text.
* **Charts:** Area charts are used for performance over time. Donut charts are used for asset allocation. Small line charts are used for quick trend visualization next to list items.

---

## 3.0 Screen-by-Screen Breakdown

### 3.1 Home Screen (`z6742151638455_...jpg`)
* **Objective:** Provide a high-level summary of the user's total investment performance and quick navigation to all major app features.
* **Components:**
    * **Header:** User avatar, user name, and account ID on the left. Notification, Search, and QR icons on the right.
    * **Main Asset Chart:** A large area chart showing portfolio growth. Below it is a segmented control for timeframes (1W, 1M, 3M, 6M, 1Y).
    * **Feature Grid:** A grid of circular icons for primary features: `Stocks`, `For Kids`, `Haybond Savings`, `Fund Certificates`, `IPO Hunting`. Note the tag on "Haybond" indicating an interest rate.
    * **Promotional Banner:** A horizontally scrollable carousel with pagination dots. Used for marketing new funds or features. Contains a clear CTA button ("Xem ngay" / "View Now").
    * **Bottom Navigation:** `Trang chủ` (Home) is active.

### 3.2 Assets - Allocation View (`z6742151704938_...jpg`)
* **Objective:** Display a detailed breakdown of the user's Net Asset Value (NAV) across all product categories.
* **Components:**
    * **Header:** Simple title: `Tài sản` (Assets).
    * **NAV Summary:** A hero section displaying the total NAV value with a show/hide toggle. A small line chart mirrors the one on the Home screen.
    * **Quick Actions:** A 4-icon grid for core money operations: `Nạp tiền` (Deposit), `Chuyển tiền/chứng khoán` (Transfer), `Rút tiền` (Withdraw), `Lịch sử tiền` (History).
    * **Allocation Panel:**
        * **Tabs:** "Phân bổ" (Allocation) and "Biểu đồ tăng trưởng" (Growth Chart). "Phân bổ" is active.
        * **Left List:** A list of asset classes (`Tiền`, `Chứng khoán`, `Chứng chỉ quỹ`, etc.) with their current values and P/L percentages.
        * **Right Chart:** A donut chart visually representing the allocation percentages shown in the list. Each segment's color corresponds to a dot next to the asset class.

### 3.3 Assets - Growth Chart View (`z6742151711379_...jpg`)
* **Objective:** Provide a larger, more detailed view of the user's portfolio performance over time.
* **Components:**
    * Identical to the **Assets - Allocation View** except for the main panel.
    * **Growth Chart Panel:**
        * The "Biểu đồ tăng trưởng" tab is active.
        * It contains a large area chart with a labeled Y-axis (in millions) and a dropdown for time-frame selection (1Y selected).

### 3.4 Market - Stocks View (`z6742151638454_...jpg`)
* **Objective:** Provide a real-time overview of the stock market, including major indices and top-moving stocks.
* **Components:**
    * **Header Tabs:** A sub-navigation bar for different market types. `Chứng khoán` (Stocks) is active.
    * **Search Bar:** Allows searching for specific stock tickers.
    * **Index Cards:** Side-by-side cards for key indices (VNINDEX, VN30) showing their current value and a small trend chart.
    * **Movers Panel:** A tabbed section for `Top biến động` (Top Movers), `Top dẫn dắt` (Top Leaders), etc. Includes time filters (From Session Start, 2H, 1H, 15M). The list is presented in two columns with ticker, price, change, and a mini line chart.
    * **Bottom Navigation:** `Thị trường` (Market) is active.

### 3.5 Market - Savings View (`z6742151640063_...jpg`)
* **Objective:** Display and compare savings interest rates from banks and MoMo's own products.
* **Components:**
    * **Header Tabs:** The `Tiết kiệm` (Savings) tab is active.
    * **Bank Rate Grid:** A 2x2 grid of cards showing recent interest rate changes for a specific term (e.g., 3 months) at various banks.
    * **Product Promotion Card:** A dedicated card to promote a MoMo savings product (HayBond), highlighting its competitive rate.
    * **Rate Table:** A simple table comparing the interest rates of the "HayBond" product across different terms (3M, 6M, 12M).

### 3.6 Trade - Regular Buy Order (`z6742151644148_...jpg`)
* **Objective:** Allow users to place a buy order for a stock in their regular (non-margin) account.
* **Components:** This is a high-density screen.
    * **Account Tabs:** Toggle between `TK Thường` (Regular Account) and `TK Margin`.
    * **Ticker Info:** Shows the selected stock, its exchange, current price, and daily change.
    * **Left Column (Order Book):** Displays bid/ask prices and volumes. Includes tabs for board lots vs. odd lots. Also shows key price levels (Ceiling, Floor, Reference).
    * **Right Column (Order Panel):**
        * `Mua` (Buy) / `Bán` (Sell) toggle.
        * Order type selection (e.g., `Lệnh 24/7`, LO, MTL).
        * Input fields for Price and Quantity with `+`/`-` steppers.
        * Display of `Sức mua` (Buying Power).
        * A large `Đặt lệnh` (Place Order) CTA button.
    * **Bottom Navigation:** `Giao dịch` (Trade) is active.

### 3.7 Trade - Margin Buy Order (`z6742151645136_...jpg`)
* **Objective:** Allow users to place a buy order using their margin account.
* **Components:**
    * Visually very similar to the regular order screen, but the `TK Margin` tab is active.
    * The **Order Panel** includes additional margin-specific information: `Tỷ lệ cho vay` (Lending Rate) and `Sức mua tối đa` (Max Buying Power).
    * **Footer Tabs:** A new set of tabs appears at the bottom for different order types: `Lệnh thường` (Regular Order), `Lệnh điều kiện` (Conditional Order), etc.

### 3.8 Opportunities - News Feed (`z6742151655617_...jpg`)
* **Objective:** Provide a curated feed of market news and analysis to help users make informed investment decisions.
* **Components:**
    * **Header:** Title `Cơ hội` (Opportunities) and a filter icon.
    * **Filter Legend:** An info card explaining the color-coding of news items (Green=Positive, Yellow=Neutral, etc.).
    * **News Cards:** A vertical feed of cards. Each card is color-coded and contains a company logo, ticker, headline, summary, and timestamp.
    * **Bottom Navigation:** `Cơ hội` (Opportunities) is active.

### 3.9 Opportunities - News Detail (`z6742151651305_...jpg`)
* **Objective:** Display the full content of a news article and provide a direct path to trade the related stock.
* **Components:**
    * **Header:** A back arrow and the news card itself serving as the header.
    * **Article Body:** The full text of the article.
    * **Interaction:** Thumbs up/down icons for user feedback.
    * **Stock Info Snippet:** An expandable card showing the stock's current price and a mini chart.
    * **Primary CTA:** A large, `Đặt lệnh` (Place Order) button at the bottom, styled as a primary action button.
    * **Disclaimer:** A footer noting that the analysis is AI-driven and not a financial recommendation.

### 3.10 Fund Certificates - Portfolio View (`z6742151633151_...jpg`)
* **Objective:** Show the user's detailed holdings and performance within the Fund Certificates product.
* **Components:**
    * **Header:** Back arrow, title `Chứng chỉ quỹ`, and tabs for `Tài sản` (Assets) / `Thị trường` (Market). "Assets" is active.
    * **Summary:** Total value and total P/L for this asset class.
    * **Holdings List:** A list of all funds owned, showing name, quantity, portfolio allocation (`Tỷ trọng`), asset value, and the P/L for that specific fund.

### 3.11 Fund Certificates - Market View (`z6742151639857_...jpg`)
* **Objective:** Allow users to discover and explore available fund certificates for investment.
* **Components:**
    * The `Thị trường` (Market) tab is active.
    * **Mascot Grid:** A signature feature. A grid of "mascots" representing different investment risk profiles (e.g., Turtle for Safe, Dragon for Adventurous) with their historical performance.
    * **All Funds List:** A filterable list of all available funds, showing their price, growth, and long-term average return.

---

## 4.0 Key User Flows & Interactions

### 4.1 Checking Portfolio and Drilling Down
1.  User opens the app to the **Home Screen (3.1)** to see the total asset chart.
2.  User taps the `Tài sản` (Assets) icon in the bottom navigation.
3.  The app navigates to the **Assets Screen (3.2)**, showing the allocation donut chart.
4.  User taps on the "Chứng khoán" (Stocks) list item.
5.  The app navigates to the dedicated **Stocks Portfolio Screen** (similar to `z6742151637291_...jpg`), showing individual stock holdings.

### 4.2 Acting on a News Opportunity
1.  User taps the `Cơ hội` (Opportunities) icon in the bottom navigation.
2.  The app navigates to the **Opportunities News Feed (3.8)**.
3.  User finds an interesting positive news card (e.g., about FPT stock) and taps on it.
4.  The app navigates to the **News Detail Screen (3.9)**.
5.  After reading, the user decides to buy. They tap the `Đặt lệnh` (Place Order) CTA at the bottom.
6.  The app navigates to the **Trade Screen (3.6)**, with the Ticker Search pre-filled with "FPT" and the "Buy" toggle selected, streamlining the process.

### 4.3 Discovering and Researching a Fund
1.  User taps the `Thị trường` (Market) icon in the bottom navigation.
2.  On the **Market Screen**, they tap the `Chứng chỉ quỹ` sub-tab.
3.  The app navigates to the **Fund Certificates Market View (3.11)**.
4.  User can either tap on a "Mascot" to see a pre-built portfolio or scroll down to the "All Funds" list to browse individual funds.
5.  Tapping on any fund or mascot would navigate to a respective detail page (not provided in screenshots) for further research before purchasing.
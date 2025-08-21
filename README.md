# YouTube Channel Performance Dashboard

## Objective

Deliver high-level insights on YouTube channel performance.\
Focus on **views, subscribers, and language distribution**.

------------------------------------------------------------------------

## Dashboard Layout

### 1. KPI Card

-   **Total Views**
-   **Total Subscribers**
-   **Total Channels**

### 2. Bar Chart

-   **View Count by Language**
    -   X: Language
    -   Y: View Count

### 3. Pie Chart

-   **Language Distribution**
    -   Language
    -   Subscriber Share

### 4. Table

-   **Top 10 Channels (By Subscriber Count)**
    -   Channel Name
    -   View Count
    -   Subscriber Count / URL

------------------------------------------------------------------------

## Dimensions

-   Channel Name
-   Language


## Measures

-   View Count =sum(view_count)
-   Subscriber Count =sum(subscriber_count)
-   Derived: Number of Channels =count(Channel_id)

## Filters

-   Dropdown for Language

------------------------------------------------------------------------


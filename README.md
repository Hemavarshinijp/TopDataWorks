# YouTube Channel Performance Dashboard

## Objective (TD (1) )

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
# YouTube Dashboard Enhancement - ( TD (2) )

## 🎯 Objective
- Analyze efficiency, coverage, and content clusters across YouTube channels.
- Enable deep exploration of topics, performance patterns, and correlations.

---

## 📊 Data Model

### Dimensions
- **Videos[language]**
- **Channels[channelname]**
- **Videos[uploader]**
- **Videos[Video Size]** (Short/Medium/Long — derived from duration)

#### Create a Derived Column for Video Size
DAX
Video Size:=
SWITCH(
    TRUE(),
    Videos[duration_sec] <= 60, "Short",
    Videos[duration_sec] <= 180, "Medium",
    "Long"
)
## Measures
Views per Subscriber :
= DIVIDE([Total_views],[Total_subscribers],0)

Average Video Duration (Min) :
= [Average_video_duration]/60

Views per Minute :
= DIVIDE([Total_views], sum(video_summary[duration_sec])/60,0)

Dropdown for Language → Videos[language]

Dropdown for Video Size → Videos[Video Size]

Range Slicer for Video Minutes (Rounded) → Create a calculated column:
= ROUND(video_summary[duration_sec] /60,0)

📈 Visualizations

##  KPI Cards
Add 3 KPI Cards:

Card 4: Views per Subscriber → Use Views per Subscriber measure.

Card 5: Average Video Duration (Min) → Use Average Video Duration (Min) measure.

Card 6: Views per Minute → Use Views per Minute measure.

## Line Chart
X-axis: Videos[language]
(Sort languages by rank → create a measure/count of videos per language and sort axis by it)

Y-axis: Videos Published → COUNTROWS(Videos)

Optional Secondary Line: Average Views per Video → DIVIDE(SUM(Videos[views]), COUNTROWS(Videos))

## Tree Map
Group: Videos[language]

Details (optional): Videos[Video Size]

Values: SUM(Videos[views]) (or COUNTROWS(Videos) if focusing on video count)

Tooltip / Data Label: Show View Share % → View Share % = DIVIDE([Total_views], CALCULATE([Total_views], ALL(video_summary[language])))

## Bubble Chart
Category: Channels[channelname] (or Videos[uploader])

X-axis: SUM(Channels[subscribers])

Y-axis: SUM(Videos[views])

Size: Views per Minute

Legend (optional): Videos[language]



# Vietnamese Music Visualization
<img src = "Images/spotify_cover.jpeg">

## Project Overview
This repository contains the final project for the **Data Visualization** course at VNU-HCMUS, Faculty of Information Technology (Class 22KHDL). The project analyzes Spotify data on Vietnamese music to uncover trends in song performance, artist popularity, and genre distribution, visualized through interactive dashboards.

- **Data Link**: [Spotify Datasets](https://developer.spotify.com/)
<img src = "Images/dataset_cover.png">

[KWORB](https://kworb.net/)
<img src = "Images/kworb.png">

---

# 1. 📌 Description
This project implements an end-to-end data visualization solution, leveraging Python libraries (Pandas, Matplotlib, Seaborn, Plotly) and dashboard tools (Power BI) to analyze Vietnamese music data from Spotify. The process began with exploratory data analysis (EDA) in Jupyter Notebooks, followed by modularizing the pipeline for data ingestion, transformation, and visualization. Interactive dashboards were developed to present insights on song popularity, streaming trends, artist metrics, and genre performance. The final step involved integrating AI (e.g., ChatGPT) for analysis.

---

# 2. ⚙️ Technologies and Tools
- **Languages/Frameworks**: Python (Pandas, NumPy, Matplotlib, Seaborn, Plotly)
- **Visualization Tools**: Power BI
- **Development**: Jupyter Notebook, Git, GitHub
- **Environment**: Anaconda, Visual Studio Code
- **AI Integration**: ChatGPT for Q&A and dashboard evaluation

---

# 3. 🎯 Project Objective

## 3.1 What is the Project Problem?
The project aims to analyze Spotify data to uncover actionable insights about Vietnamese music, such as which songs, artists, or genres perform best, and how streaming trends evolve over time. The challenge is to present complex data in an accessible, interactive format for stakeholders like music analysts, marketers, and fans.

## 3.2 What is the Context?
The datasets, sourced from Spotify API, include song metrics (popularity, streams), artist details (followers, genres), and streaming performance (daily/weekly charts). Key performance indicators (e.g., total streams, genre distribution, artist popularity) guide the visualization, emphasizing clear and impactful representations of trends.

## 3.3 Project Objectives
1. Conduct thorough EDA to understand patterns in song, artist, and genre data.
2. Develop interactive dashboards to visualize metrics like popularity, streams, and genre trends.
3. Integrate AI to enhance analysis and evaluate dashboard usability.
4. Finished dashboards for interactive data exploration.

## 3.4 Project Benefits
1. Provides actionable insights for music industry stakeholders.
2. Enhances understanding of Vietnamese music trends through visualizations.
3. Offers a scalable, interactive platform for data exploration.

## 3.5 Conclusion
The dashboards enable users to explore nuanced trends, such as genre dominance or artist performance, facilitating data-driven decisions in the music industry.

---

# 4. 🔍 Solution Pipeline

## General EDA
### Dataset Overview
The project uses three datasets:
- **Vietnamese_only_songs_cleaned**: 4683 songs with columns for ID, album, artist, duration, popularity (0–100), streams, genres, and explicit content.
<img src = "Images/vn_only_songs.png">

- **position_streams_by_time_daily/weekly_total_peak_cleaned**: Daily/weekly streaming data with total streams, peak streams, and chart positions.
<img src ="Images/weekly.png">
<img src = "Images/daily.png">

- **Vietnamese_artists**: Artist data with ID, name, followers, and genres.

### Categorical Features Analysis
- **Genres**: V-pop (29.74%), Vinahouse (19.68%), Vietnamese hip hop dominate.
<img src = "Images/genres.png">

- **Explicit Content**: Most songs are non-explicit.
<img src = "Images/explicit.png">

- **Artists**: Top artists (e.g., Sơn Tùng M-TP, Vũ Cát Tường) have the most number of songs.
<img src = "Images/artists.png">

### Numerical Features Analysis
  - **Popularity**: Ranges from 0–100; top songs have high streams.
  - **Streams**: V-pop leads with 19.8B streams.
  - **Duration**: Average ~4 minutes, stable since the 1990s.

<img src = "Images/numerical.png">

### Correlation Analysis
#### Songs
<img src = "Images/corr.png">

**Album_popularity:**
- Strong correlation with popularity (0.81): Popular albums often contain popular songs.
- Moderate correlation with track_number (0.28): Songs earlier in an album may boost its popularity.
- Moderate correlation with stream_counts (0.25): Popular albums tend to have higher streams.

**Disc_number:**
- No significant correlations (near 0): Disc number has little impact on popularity or streams.

**Duration_ms:**
- Weak negative correlation with album_popularity (-0.10) and popularity (-0.06): Longer songs may be slightly less popular.
- No significant correlations with other variables: Duration has minimal impact on streams or track position.

**Popularity:**
- Strong correlation with album_popularity (0.81): Popular songs are often in popular albums.
- Moderate correlation with stream_counts (0.33): Popular songs generally have higher streams, though promotion or virality can also drive streams.

**Track_number:**
- Moderate correlation with album_popularity (0.28): Early album tracks may contribute more to album popularity.
- No significant correlations with other variables: Track position has little effect on popularity or streams.

**Stream_counts:**
- Moderate correlation with popularity (0.33): High-stream songs are often more popular.
- Moderate correlation with album_popularity (0.25): High-stream albums tend to be more popular.

#### Daily and weekly charts
<img src = "Images/weekly_corr.png">

<img src = "Images/daily_corr.png">

- **TotalStreamCounts vs. PeakStreamCounts:** Weekly data shows a stronger correlation (0.55 vs. 0.50), indicating a closer relationship between total streams and peak streams in weekly data.
- **TotalStreamCounts vs. PeakPosition:** Weekly data has a stronger negative correlation (-0.51 vs. -0.45), suggesting total streams impact chart position more in weekly data.
- **PeakStreamCounts vs. PeakPosition:** Similar correlations in Weekly (-0.47) and Daily (-0.46), indicating a consistent relationship between peak streams and chart position across both datasets.
#### Artists
<img src = "Images/artists_corr.png">

- **Popularity vs. Followers:**
    - Correlation: 0.41 (moderate positive).
    - Artists with more followers tend to have higher popularity, but the relationship is not strong.
    - Possible reasons:
        - Some artists with many followers are less popular (e.g., inactive or no recent releases).
        - Some highly popular artists have fewer followers (e.g., new or viral artists).

### Missing Values Analysis
- Stream counts have some missing rows, because some songs have stream counts < 1000, therefore, we filled by value 999.

## Dashboard Development
### Step 1: Data Modelling
<img src ="Images/Modelling.png">

- First, we extracted the new table Date by DAX functions, then connected root dataset.
- Second, connected other tables with vietnamese_songs_only via `id`.
- Third, we created table `artists` to connect `vietnamese_artists` with `vietnamese_songs_only` via `id`, then connected `artists_genres` and `vietnamese_artists`via `Name` of artists. Finally, connected `artists` with `vietnamese_artists` via `Values` and `Name`.

### Step 2: Visualization Development
#### **Overview Dashboard**:
<img src ="Images/overview.png">

- This dashboard provides an overview of the Vietnamese music market including size, average characteristics, trends over time and distribution of key factors such as genre and popularity.

- **Key Performance Indicators (KPIs)**
    - **Dataset Scale:** 1,409 artists, 4,735 songs, 195 genres, 4.1M streams.
        - **Analysis:** Moderate dataset size supports robust analysis. Low average streams (~865/song) may indicate a niche focus or data subset.
    - **Average Characteristics:**
        - Song Duration: 4.0 minutes.
        - Popularity: 28 (0-100 scale).
        - **Analysis:** 4-minute duration fits streaming norms; popularity of 28 suggests moderate visibility, possibly due to a niche audience.
- **Trends Over Time**
    - **Song Count Trend**: Sharp increase post-2015, peaking early 2020s; low pre-2000.
        - **Analysis:** Reflects Spotify’s rise and pandemic production boost; pre-2000 gap may be data or industry limitation.
    - **Song Duration Trend:** Peaked at ~8 minutes in the 1980s, stabilized at 4 minutes late 1990s, slight recent decline.
        - **Analysis:** 1980s peak may reflect longer formats; 4-minute norm aligns with radio/streaming; decline suggests shorter song trends.
- **Distribution**
    - **Genre Distribution:**
        - V-pop: 29.74%, Vinahouse: 19.68%, Vietnamese lo-fi: 19.64%, Hip hop: 15.8%, Indie: 15.14%.
        - **Analysis:** V-pop dominates, reflecting mainstream appeal; niche genres (Vinahouse, lo-fi) thrive; concentration suggests centralized tastes or data bias.
    - **Popularity Distribution:** Most songs at 30-40 (mean 28), few at 0-10 or 50+.
        - **Analysis:** Normal distribution indicates moderate engagement; few extremes suggest stable but not viral presence.

- **Conclusion**
    - **Key Insights:** V-pop, Vinahouse, lo-fi, hip hop, and indie dominate; 4-minute duration is standard; mean popularity is 28.
    - **Analysis:** Concentrated genres offer marketing targets; 4-minute norm fits streaming; moderate popularity suggests growth potential via playlists or marketing.

#### **Songs Dashboard**:
- Dashboard provides information about each song with the main sections: song name, performing artist, popularity, song genre, highest position the song has ever reached, highest number of plays the song has achieved. 
- Along with general information about songs on the market such as: chart ranking songs by popularity, chart ranking song streams, and chart showing the relationship between popularity and album popularity.
- **General Observation**
    - **Top Songs:** "raining for hours" (Popularity: 80, Streams: 645M), "Kyoto" (76), "La Diabla" (73, Streams: 853M), "Mất kết nối" (70), "Andree Right Hand xin chào" (Streams: 199M).
    - **Insight:** High popularity correlates with high streams and top rankings, as popular songs attract more listeners.
    - **Correlation Chart:** Clear positive linear correlation between song and album popularity—popular albums tend to have popular songs, highlighting the role of album branding.
    - **Observation:** Few popular songs exist in less popular albums, emphasizing the importance of album reputation.
- **Conclusion**
    - **Key Insights:** Hits like "La Diabla," "raining for hours," and "Kyoto" have high popularity and streams (hundreds of millions), proving their viral appeal. High popularity typically leads to top streaming ranks.
    - **Correlation:** Positive linear relationship between song and album popularity; popular songs rarely appear in low-popularity albums, underscoring the importance of album branding.

#### **Genres Dashboard**:
<img src = "Images/genres_dashboard.png">

The Genres Dashboard delves into a detailed analysis of music genres within the Vietnamese music dataset on Spotify. It focuses on three primary metrics for each genre:

- **Total Streams** (cumulative streams for all songs in the genre).
- **Number of Songs** (total songs classified under the genre).
- **Number of Artists** (total artists associated with the genre). This dashboard provides a granular view of genre performance, helping stakeholders (e.g., music analysts, marketers) understand which genres dominate the market and drive listener engagement.

- **Key Performance Indicators (KPIs)**
    - **Dataset:**
        - **Total Genres:** 194 distinct genres.
        - **Total Songs:** 4,701 songs.

    - **Analysis:**
        - The dataset includes a diverse range of 194 genres, indicating a broad spectrum of musical styles within Vietnamese music on Spotify. However, as later sections reveal, the market is heavily concentrated in a few dominant genres.
        -  The song count of 4,701 is slightly lower than the 4,735 songs reported in the Overview Dashboard (Section 6.2.2), which might suggest a subset of the data was used for this analysis (e.g., excluding songs without genre tags) or minor data inconsistencies.
- **Detailed Analysis by Genre**
    - **Total Streams:**
        - **Observation:**
            - Despite the presence of 194 genres, streaming activity is heavily concentrated in the top 5 genres, consistent with findings from the Overview Dashboard:
                - **V-pop:** ~19.8 billion streams (19,839 million).
                - **Vietnam indie:** ~15.3 billion streams.
                - **Vietnamese hip hop:** ~14.9 billion streams.
                - **Vietnamese lo-fi:** ~12.3 billion streams.
                - **Vinahouse:** ~10 billion streams.
        - Other genres, such as Vietnamese bolero, bolero, and lo-fi (possibly referring to non-Vietnamese lo-fi), have significantly lower streaming numbers.
        - **Analysis:**
            - V-pop leads with 19.8 billion streams, confirming its status as Vietnam’s most mainstream genre—comparable to K-pop in South Korea or J-pop in Japan. Meanwhile, Vietnam indie (15.3B) and Vietnamese hip hop (14.9B) highlight the rise of alternative and urban music, fueled by younger Spotify users and global trends. Vietnamese lo-fi (12.3B) and Vinahouse (10B) also thrive in their niches—lo-fi for study/relaxation, and Vinahouse for dance and nightlife. The sharp drop-off beyond the top 5 genres, such as Vietnamese bolero, reveals a market heavily skewed toward modern music. Traditional genres may have stronger presence on platforms like YouTube or local radio, reflecting different audience preferences.
    - **Number of Songs:**
        - **Observation:**
            - The top 5 genres also dominate in terms of song count, with a significant gap compared to other genres:
                - **V-pop:** 4,683 songs.
                - **Vietnamese hip hop:** 3,096 songs.
                - **Vietnam indie:** 3,092 songs.
                - **Vietnamese lo-fi:** 2,479 songs.
                - **Vinahouse:** 2,389 songs.
            - Other genres have far fewer songs, though exact numbers are not provided.
        - **Analysis:**
            - V-pop dominates the dataset with 4,683 out of 4,701 songs, showing its overwhelming presence and suggesting it’s often the default genre due to broad appeal and easy categorization. Vietnamese hip hop (3,096) and Vietnam indie (3,092) also show strong output, likely driven by their popularity among younger creators. Lo-fi (2,479) and Vinahouse (2,389) follow closely, reflecting their niche roles—lo-fi for playlists, Vinahouse for the dance scene. The large gap between these top 5 and other genres (like bolero) points to a lack of diversity in production or limited appeal of traditional genres on Spotify.
    - **Number of Artists:**
        - **Observation:**
            - V-pop is associated with the most artists: 1,378.Followed by:
                - Vietnamese hip hop: 1,048 artists.
                - Vietnam indie: 1,012 artists.
                - Vietnamese lo-fi: 881 artists.
                - Vinahouse: 850 artists.
        - **Analysis:**
            - V-pop’s connection to 1,378 out of 1,409 artists highlights its dominance, showing that most artists in the dataset are involved in this genre—often alongside others due to its broad appeal. High artist counts in Vietnamese hip hop (1,048) and Vietnam indie (1,012) reflect a vibrant, accessible music scene for independent creators. Vietnamese lo-fi (881) and Vinahouse (850) also show strong representation, driven by bulk production and niche popularity. Overall, the concentration of artists in these top 5 genres aligns with streaming and song trends, confirming that modern genres dominate both music creation and listener demand on Spotify.

- **Conclusion**
    - **Key Insights:**
        - The Genres Dashboard highlights the dominance of five modern Vietnamese genres—V-pop, Vietnamese hip hop, Vietnam indie, Vietnamese lo-fi, and Vinahouse—across all key metrics: total streams, song count, and number of artists.

        - V-pop leads significantly with 19.8B streams, 4,683 songs, and 1,378 artists, underscoring its role as the default and most accessible genre on Spotify Vietnam.

        - The disparity between these top 5 genres and the remaining 189 shows a highly concentrated market, where modern, youth-driven trends define listener behavior and artist output.
    - **Analysis**
        - V-pop’s dominance reflects its cultural significance and mass appeal. Its heavy playlist presence and accessibility make it the go-to genre for casual Spotify users.

        - Genres like Vietnamese hip hop, indie, lo-fi, and Vinahouse serve niche but active audiences:

            - Hip hop & indie: Trend-focused youth.

            - Lo-fi: Study/relaxation listeners.

            - Vinahouse: Dance/club culture.

        - The gap with traditional genres (e.g., bolero) may stem from:

            - Spotify’s younger, urban demographic.

            - Underrepresentation of older audiences.

            - Cataloging biases or platform focus on trending styles.

        &rarr; This reflects a broader industry trend: streaming platforms increasingly amplify modern genres to drive engagement—often at the cost of traditional music visibility.
#### **Artists Dashboard**:
Dashboard is designed to provide a detailed analysis of individual artists within the Vietnamese music dataset on Spotify. It focuses on key metrics such as:
- **Popularity** (on a 0-100 scale, calculated by Spotify based on recent streams and listener engagement).
- **Followers** (the number of Spotify users following the artist, reflecting long-term fanbase loyalty).
- **Total Streams** (cumulative streams of the artist’s songs).
- **Genres** (the music genres associated with the artist). Additionally, the dashboard includes comparisons of artists’ positions relative to others in the Vietnamese music market, offering insights into their standing and influence.

- **Tree Map Visualization:** The dashboard features a tree map that visually compares artists based on their follower counts. The top artists by followers include:
    - **Sơn Tùng M-TP:** 6.5 million followers.
    - **Đen Vâu:** 4.3 million followers.
    - **Vũ:** 2.4 million followers.
    - **HIEUTHUHAI:** 2.2 million followers.
    - This visualization highlights the artists with the largest fanbases, emphasizing their established presence in the Vietnamese music scene.

- **Popularity Rankings:**
    - Despite having the highest follower count, Sơn Tùng M-TP has a popularity score of 65, placing him at the 6th position in terms of popularity.
    - The top artists by popularity are:
        - **HIEUTHUHAI:** 68.
        - **Anh Trai Say Hi:** 67.
        - **Dangrangto:** 67.
        - **tlinh:** 66.
    - Notably, other high-follower artists like Đen Vâu, Vũ, and Mỹ Tâm rank surprisingly low in popularity.
- **Analysis:**
    - There’s a noticeable gap between follower counts and current popularity in the Vietnamese Spotify market. Veteran artists like Sơn Tùng M-TP and Mỹ Tâm have large followings but lower popularity scores compared to trend-driven artists like HIEUTHUHAI and tlinh. This reflects Spotify’s younger user base, which favors recent, viral content. While followers indicate long-term loyalty, the popularity score reflects recent activity. Without new releases or ongoing engagement, even well-established artists may see a drop in popularity.
- **Detailed Analysis (Focus on Sơn Tùng M-TP and HIEUTHUHAI)**

    - **Sơn Tùng M-TP:** 

        <img src = "Images/sontung.png">

        - **Metrics:**
            - **Followers:** 6.5 million.
            - **Total Streams:** 865 million.
            - **Popularity:** 65.
            - **Genres:** V-pop, Vinahouse, hip-hop.
            - **Notable Songs:** "Chúng ta của hiện tại," "Muộn rồi mà sao còn."
        - **Analysis:**
            - Sơn Tùng M-TP, a major figure in V-pop, boasts 6.5 million followers and over 865 million total streams, with hits like “Chúng ta của hiện tại” and “Muộn rồi mà sao còn.” His strong fanbase reflects lasting impact and success. However, his popularity score of 65, lower than some newer artists, suggests a decline in recent engagement—likely due to fewer new releases or shifting listener trends toward genres like hip-hop.

    - **HIEUTHUHAI:**
        
        <img src = "Images/hieuthuhai.png">

        - **Metrics:**
            - **Followers:** 2.2 million.
            - **Total Streams:** 840 million.
            - **Popularity:** 68.
            - **Genres:** V-pop, Vietnamese hip-hop.
            - **Notable Songs:** "Không thể say," "Exit Sign," "Ngủ một mình."
        - **Analysis:**
            - HIEUTHUHAI leads in current popularity with a score of 68, surpassing even Sơn Tùng M-TP and tlinh. Though he has fewer followers (2.2M), his 840 million streams show strong engagement. Viral hits like “Không thể say” and “Exit Sign” highlight his appeal to younger Spotify users and the rising influence of Vietnamese hip-hop in shaping today’s music trends.

- **Conclusion** 

**Key Insight: Why do some artists with high follower counts not rank at the top in terms of popularity?**

- **Followers vs. Popularity: Loyalty vs. Trends**

    - Follower count reflects long-term loyalty and past success. Artists like Sơn Tùng M-TP and Mỹ Tâm have built large, stable fanbases over years of consistent impact.

    - Popularity, however, is dynamic—driven by recent streams, social media buzz, and chart performance. It shows who's trending now.

- Veteran artists may have high follower counts but lower popularity if they’ve released less new content recently. Meanwhile, newer artists like HIEUTHUHAI or tlinh may have fewer followers but high popularity due to recent viral hits.

&rarr; This contrast highlights the divide between legacy influence and current momentum—with followers indicating staying power and popularity showing immediate impact.



### Step 3: AI Integration
<img src = "Images/chatbot.png">

- Used ChatGPT for:
  - Q&A functionality (e.g., "What are the top songs by streams?").
  - Dashboard evaluation, suggesting improvements like reducing chart clutter.
- Implemented a chatbot in the AI Lens sponsored by ChatGPT 3.5 for user queries.
- However, the chatbot for songs and artists can only answer 7 queries for each day.

### Step 4: Evaluation
- **Usability**: Dashboards tested for filter responsiveness and clarity.
- **Insights**: Validated against EDA findings (e.g., V-pop dominance, 4-minute song duration).
- **AI Feedback**: Reduced cognitive overload by limiting metrics per dashboard.


## Key Findings
- **Genre Dominance**: V-pop, Vietnamese hip hop, Vietnam indie, Vietnamese lo-fi, and Vinahouse account for most streams and songs.
- **Song Trends**: Average song duration stabilized at ~4 minutes.
- **Popularity vs. Streams**: High-popularity songs (e.g., "La Diabla": 73 popularity, 853M streams) drive streams.
- **Artist Dynamics**: Sơn Tùng M-TP (6.5M followers) leads in followers, while HIEUTHUHAI (68 popularity) excels in recent trends.
- **Market Concentration**: Modern genres dominate the Vietnamese music market.

---

# 5. 📊 Project Results
- Developed four interactive dashboards providing comprehensive insights into Vietnamese music trends.

- Validated findings through AI analysis and user testing, ensuring actionable and clear visualizations.
- Achieved project goals of delivering stakeholder-friendly insights for the music industry.


---

# 6. 💻 Next Steps
  - Real-time data updates via Spotify API integration.
  - Mobile optimization for the Streamlit app.
  - Adding predictive analytics for song popularity trends.
  - Enhancing visualizations with 3D charts or animations.

---

# 7. Run This Project Locally

#### Prerequisites
- Python 3.11+
- pip
- Git
- Power BI/Tableau (optional for dashboard viewing)

#### Steps
1. Clone the repository:
   ```sh
   git clone https://github.com/your-repo/vietnamese-music-visualization.git
   ```
2. Open file dashboard and start exploring the dashboard.
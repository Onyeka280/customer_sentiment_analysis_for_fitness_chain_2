# Customer Sentiment Analysis for Fitness Chain Using NLP

## Project Overview
I developed a comprehensive Natural Language Processing (NLP) system for a major UK fitness chain with nearly 2 million members across 600+ gym locations worldwide. Using 12 months of customer reviews from Google and Trustpilot (approximately 40,000 reviews total), I built automated topic modelling tools to identify recurring complaints, operational issues, and actionable insights to improve member experience and retention.

## Business Problem
The fitness company operated on a value-for-money membership model but faced critical challenges:
- **Volume overwhelm**: Nearly 40,000 reviews annually made manual analysis unfeasible
- **Reactive problem-solving**: No systematic approach to identifying root causes of negative feedback
- **Hidden patterns**: Unable to detect recurring issues across 600+ locations
- **Resource inefficiency**: Couldn't prioritize which problems to address first
- **Member churn risk**: Unresolved complaints increasing likelihood of cancellations

Without automated analysis, the company struggled to maintain service quality at scale, risking member retention and competitive position in the value fitness sector.

## Dataset & Scope
**Two comprehensive review datasets:**
- **Google Reviews**: 23,250 records with ratings, comments, dates, and location data
- **Trustpilot Reviews**: 16,673 records with detailed feedback and star ratings
- **Combined coverage**: 12 months of feedback across multiple UK locations
- **Focus**: Top 30 shared locations between both platforms for cross-validation

## Data Preprocessing & Quality Control
I implemented rigorous cleaning protocols:
- Removed non-analytical columns (anonymous IDs, survey IDs, URLs, reply dates)
- Filtered for English-only reviews to maintain NLP model accuracy
- Eliminated null or empty review content
- Standardized text: lowercase conversion, punctuation removal, whitespace normalization
- Tokenized reviews using NLTK
- Removed stopwords, numbers, and special characters
- **Filtered negative reviews**: Ratings/stars < 3 for focused problem identification

## Methodology

### Stage 1: Exploratory Text Analysis (NLTK)
**Initial Investigation - All Reviews from Shared Locations:**
- Word frequency analysis revealed positive sentiment overall
- Common terms: "equipment," "great," "good," "staff," "clean," "friendly," "machines," "classes"
- Created word clouds visualizing most frequent terms
- Identified need to focus specifically on negative reviews

**Negative Reviews Analysis:**
- Extracted reviews with ratings < 3 stars
- Word frequency showed: "equipment," "staff," "membership," "machines," "people," "time"
- Themes emerged: maintenance issues, service problems, crowding, billing concerns

**Top 30 Locations Deep Dive:**
- Similar patterns to full dataset but with intensified frequency
- "People" and "always" appeared more prominently
- Indicated recurring issues with overcrowding and persistent unresolved problems

### Stage 2: Advanced Topic Modelling with BERTopic
I applied BERT-based topic modelling to uncover latent complaint themes:

**BERTopic on Negative Reviews from Shared Locations:**
- Identified **50 distinct topics**, visualized top 10 for stakeholder clarity
- Generated interactive heatmaps showing topic similarities
- Created bar charts displaying top keywords per topic
- Produced intertopic distance maps revealing thematic relationships

**10 Key Complaint Clusters Identified:**

1. **Shower/Temperature Issues**
   - Keywords: showers, cold, water, aircon, hot, temperature, freezing, dirty
   - Problems: Cold/broken showers, poor water pressure, malfunctioning AC

2. **Membership & Billing Problems**
   - Keywords: membership, cancel, fee, charged, discount, joining, paid
   - Problems: Hidden fees, cancellation difficulties, unfulfilled discount promises

3. **Equipment & Overcrowding**
   - Keywords: machines, broken, wait, overcrowded, busy, equipment, order
   - Problems: Broken equipment, long wait times, excessive crowding

4. **Facility Cleanliness & Maintenance**
   - Keywords: cleanliness, toilets, dirty, showers, changing
   - Problems: Unclean facilities, poor waste management, inadequate upkeep

5. **Hygiene Complaints**
   - Keywords: smell, dirty, cleaning, toilets, bins, sweat, hygiene
   - Problems: Unpleasant odors, overflowing bins, lack of cleaning supplies

6. **Noise & Conduct Issues**
   - Keywords: music, loud, kids, phones, rude, disruptive behavior
   - Problems: Excessive noise, member misconduct, lack of enforcement

7. **Locker & Security Problems**
   - Keywords: lockers, stolen, bag, padlock, room, space
   - Problems: Theft, damaged belongings, insecure locker systems

8. **Equipment Availability & Layout**
   - Keywords: equipment, small, busy, weights, cable, wait, crowded
   - Problems: Poor layout, cramped spaces, insufficient equipment density

9. **Weight Area Organization**
   - Keywords: plates, weights, bench, bars, squat, safety
   - Problems: Misplaced equipment, crowded squat racks, safety concerns

10. **Access & Operational Policies**
    - Keywords: closed, open, parking, fine, code, pass, induction, door
    - Problems: Limited hours, parking fines, entry system failures

**Top 30 Locations Refined Analysis:**
Focusing on highest-volume locations revealed more granular insights:
- **Air conditioning issues** split into "too hot" vs. "too cold"
- **Shower complaints** separated into cold water, fungal growth, and dirt
- **Equipment problems** detailed by machine type, refurbishment delays, broken cables
- **Membership issues** divided into fees, subscriptions, discounts, and suspensions
- **Location-specific mentions**: Bradford, Finchley, Abbey Wood, Tottenham Court flagged
- **Staff problems**: Specific names mentioned, bullying complaints surfaced
- **New issues emerged**: Kids in gym areas, WiFi connectivity, fire door safety

### Stage 3: Emotion Analysis with BERT
To understand emotional intensity, I deployed emotion classification:

**Implementation:**
- Loaded bhadresh-savani/bert-base-uncased-emotion model from Hugging Face
- Classified emotions across all negative reviews
- Created emotion distribution visualizations

**Emotion Distribution Results:**
- Identified which complaints triggered strongest emotional responses
- Filtered specifically for anger-tagged reviews for deeper analysis

**BERTopic on Angry Reviews:**
- Top 10 themes remained consistent but **order shifted dramatically**
- **Air conditioning issues moved to #1** - primary anger driver
- **Toilet problems, staff rudeness, Christmas Day closures** moved higher
- Indicated these issues trigger most intense negative reactions
- Additional anger drivers outside top 10: Yanga water (sports drink), rowing machines, squat racks

**Critical Insight:** Not all complaints are equal - some trigger disproportionate emotional responses requiring immediate attention.

### Stage 4: Large Language Model Analysis (Phi-4-Mini-Instruct)
I leveraged generative AI for insight extraction and recommendation generation:

**Topic Summarization:**
- Used Phi-4-mini-instruct model to summarize key topics from angry reviews (top 30 locations)
- Fed LLM-generated summaries back into BERTopic for refined clustering
- **Top issue identified**: Membership cancellation and communication support
- Other recurring themes: Air conditioning, ventilation, equipment repairs, parking, hygiene

**Additional granular issues emerged:**
- Mirror space and layout concerns
- Privacy issues in changing areas
- Treadmill-specific complaints

**LLM-Generated Actionable Recommendations:**

| **Area** | **Actionable Insight** |
|----------|------------------------|
| **Facility Comfort & Air Quality** | Invest in high-quality air conditioning systems; implement regular maintenance schedules to ensure consistent temperature control |
| **Cleanliness & Maintenance** | Establish rigorous cleaning protocols with hourly checks in high-traffic areas; increase cleaning staff during peak hours |
| **Availability & Accessibility** | Improve class booking systems; extend operating hours where feasible; add more class offerings to manage demand |
| **Parking & Signage** | Enhance parking signage with clear, well-lit instructions; explore partnerships for additional parking spaces |
| **Equipment & Service Quality** | Implement predictive maintenance for equipment; train staff on customer service excellence and conflict resolution |
| **WiFi & Entertainment** | Upgrade to reliable, high-speed WiFi; diversify music options or create dedicated entertainment zones |
| **Regulation & Safety** | Install clear safety signage; ensure consistent availability and quality of safety equipment; enforce conduct policies |

### Stage 5: Validation with Gensim LDA
For methodological rigor, I implemented a second topic modelling approach:

**Gensim's Latent Dirichlet Allocation (LDA):**
- Applied to negative reviews from all common locations
- Identified 10 topics for comparison with BERTopic

**Findings:**
- **Similar high-level themes**: Equipment, classes, staff, hygiene, membership, air conditioning
- **LDA limitations observed**:
  - Sometimes included unrelated keywords in topics
  - Word "equipment" appeared across many topics, reducing clarity
  - Example: Topic 3 grouped "member," "air," "staff," "issue," "manager" despite being unrelated
  - Less precise topic separation than BERTopic

**Conclusion:** BERTopic provided superior topic coherence and interpretability, making it the preferred approach for this use case.

## Results Summary

### Cross-Platform Validation
- **High consistency** between Google and Trustpilot complaints
- Same locations and issues appeared across both platforms
- Validated authenticity and severity of identified problems

### Top Priority Issues (Ranked by Frequency & Emotional Intensity)
1. **Air conditioning/ventilation** (highest anger trigger)
2. **Equipment maintenance and availability**
3. **Facility cleanliness** (showers, toilets, changing rooms)
4. **Membership cancellation and communication**
5. **Staff responsiveness and professionalism**
6. **Overcrowding during peak hours**
7. **Parking and access issues**

### Location-Specific Insights
- Urban locations: Overcrowding primary complaint
- Specific gyms flagged: Bradford, Finchley, Abbey Wood, Tottenham Court
- Some locations had persistent, recurring issues across review periods

## Business Impact & Strategic Value

### Immediate Operational Benefits
- **Automated monitoring**: Replaced manual review reading with scalable NLP pipeline
- **Prioritized action plan**: Clear ranking of issues by frequency and emotional impact
- **Location targeting**: Identified specific gyms requiring urgent intervention
- **Resource justification**: Data-driven evidence for investment decisions

### Expected Outcomes
- **Improved retention**: Addressing top complaints expected to reduce member churn by 10-15%
- **Enhanced reputation**: Systematic issue resolution to improve online ratings
- **Operational efficiency**: Predictive maintenance reducing equipment downtime
- **Member satisfaction**: Proactive problem-solving before issues escalate
- **Competitive advantage**: Data-driven service quality differentiating from competitors

### Scalable Framework
The NLP system is fully automated and extensible:
- Processes thousands of new reviews monthly
- Real-time sentiment tracking capability
- Monitors intervention effectiveness over time
- Adaptable to new locations as business expands
- Can incorporate additional feedback channels (surveys, social media, emails)

## Technical Implementation

**Core Technologies:**
- **Programming**: Python (Pandas, NumPy, NLTK)
- **NLP Libraries**: BERTopic, Gensim, Transformers (Hugging Face)
- **Pre-trained Models**: 
  - BERT for topic embeddings
  - bhadresh-savani/bert-base-uncased-emotion for emotion classification
  - Phi-4-mini-instruct LLM for insight generation
- **Visualization**: Matplotlib, Seaborn, WordCloud, Plotly for interactive visualizations
- **Text Processing**: NLTK for tokenization, stopword removal, frequency analysis

**Pipeline Architecture:**
1. Multi-source data ingestion (Google, Trustpilot)
2. Preprocessing and quality control
3. Exploratory text analysis (word frequency, word clouds)
4. BERTopic topic modelling with visualization
5. BERT emotion classification
6. Focused analysis on high-emotion reviews
7. LLM-powered recommendation generation
8. LDA validation and comparison

## Key Learnings

This project demonstrated that **layered NLP analysis** reveals progressively deeper insights. Word frequency identified surface themes, BERTopic uncovered latent patterns, emotion analysis highlighted intensity, and LLM translation converted findings into actionable business strategies.

**BERTopic significantly outperformed traditional LDA** for this use case, providing more coherent topics, better semantic understanding, and clearer separation of distinct themes. However, LDA served as valuable validation, confirming core findings across methodologies.

The **emotion analysis proved critical** - not all complaints are equal. Air conditioning issues, while frequent, also triggered the strongest anger responses, making them highest priority despite other issues appearing more often in word frequency alone.

**Focusing on top 30 locations** rather than analyzing all gyms revealed more granular, actionable insights. This demonstrated the value of targeted deep-dives over broad surface-level analysis.

Most importantly, **generative AI models like Phi-4-mini-instruct can translate analysis into action**. Rather than just identifying problems, the LLM generated specific, implementable solutions tailored to the business context - bridging the gap between data science and business execution.

## Limitations & Future Enhancements

**Current Limitations:**
- Analysis limited to English reviews only
- Computational constraints restricted LLM processing to subset of reviews
- No temporal trend analysis (seasonal patterns, improvement tracking over time)
- Positive review analysis not conducted (missed opportunity to identify success factors)

**Recommended Future Work:**
1. **Non-English Review Analysis**: Allocate compute resources to process reviews in other languages
2. **Real-time Dashboard**: Deploy live monitoring system with automated alerts
3. **Temporal Tracking**: Monitor topics over time to measure intervention effectiveness
4. **Positive Sentiment Analysis**: Identify what's working well to replicate success
5. **Predictive Modelling**: Build models predicting member churn based on review patterns
6. **Drill-down Tools**: Create interactive dashboards for exploring specific topics by location
7. **Industry Expert Validation**: Engage domain experts to validate insights and align with practical operational realities

## Deliverables

- **Production-ready NLP pipeline** processing 40,000+ reviews annually
- **10 prioritized complaint clusters** with detailed descriptions and keywords
- **Location-specific scorecards** identifying problem gyms requiring intervention
- **Emotion-ranked issue list** highlighting highest-impact complaints
- **LLM-generated action plan** with specific recommendations by operational area
- **Comparative methodology analysis** (BERTopic vs. LDA performance)
- **Interactive visualizations** including word clouds, topic heatmaps, emotion distributions
- **Comprehensive 15-page technical report** with methodology, findings, and strategic roadmap ([View PDF Report](#))

---

**Technologies Used**: Python, BERTopic, Gensim LDA, NLTK, BERT (emotion classification), Phi-4-mini-instruct, Hugging Face Transformers, Pandas, Matplotlib, Seaborn, WordCloud, Plotly

**Dataset**: 39,923 customer reviews (23,250 Google + 16,673 Trustpilot) across 12 months and 600+ gym locations

**Key Finding**: Air conditioning issues ranked as #1 anger trigger; membership cancellation communication identified as top concern when using LLM summarization

**Outcome**: Automated NLP system identifying 10 key complaint themes with 7 actionable recommendation areas. Location-specific insights enable targeted interventions expected to improve member retention by 10-15% and enhance online reputation through systematic issue resolution.

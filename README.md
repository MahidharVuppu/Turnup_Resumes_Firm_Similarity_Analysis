## Turnup_Resumes_Firm_Similarity_Analysis: 
###Abstract:
Developed a firm similarity analysis project utilizing NLP and data analysis on a corpus of resumes to determine similarities between firms. By analyzing resume data, the project identifies and quantifies shared skills, industry focuses, and role requirements across companies, offering insights into firm similarities that can support competitive benchmarking and talent alignment strategies.

### Business Problem: 
Higher similarity scores between firms could support strategic insights for competitive benchmarking and talent acquisition alignment, helping businesses better understand industry trends and similar company requirements.

### Proposed Solution:
Utilize NLP embeddings and similarity analysis methods to evaluate and rank firm similarities based on resume data. By identifying patterns in roles, skills, and industry language, we aim to draw conclusions about firm alignment and characteristics.

### Data Set Details: 
The dataset consists of 29,782 resumes converted from PDF to text, using OCR techniques, for analysis. Key fields extracted include skills, work experience, education, and industry-specific keywords.

### Constraints:
A notable constraint in this project was that, despite starting with 29,782 resumes, processing halted at document number 18,311. Resulting in us being able to use a smaller dataset of only 18,311 resumes.

### Methods:

#### 1. Embedding Creation with Sentence Transformers
We used Hugging Face’s Sentence Transformers library to create embeddings for each of the 18,311 resumes that were successfully processed. Each resume was converted to a semantic vector representation, capturing the meaning of the text. We then appended JSON objects to each resume line, containing all firms and job titles found within the resume.

#### 2. Data Structuring in Pandas
After embedding creation, we structured the data into a Pandas DataFrame, where each row represented a firm. One column contained the firm name, and the other contained its embedding vector. This structure allowed for efficient processing and setup for similarity analysis.

#### 3. Firm Similarity Analysis Techniques
We employed various methods to analyze firm similarity based on the resume data, categorized as follows:

- Closest Centroids: We computed a centroid (average embedding) for each firm, treating each firm as a cluster. Firms with centroids closest in 384 dimention vector space were considered similar, implying that their job requirements or culture might align.

- Pairwise Analysis (Average and Minimum Distance):
  Average Distance: This calculated the mean distance between all pairs of embeddings across firms, providing an overall similarity score.
  Minimum Distance: This calculated the smallest distance between any embedding pairs, revealing points of strong similarity in specific roles or requirements between firms.

- Distribution-Based Analysis (KL Divergence and Earth Mover’s Distance):
  KL Divergence: Measured the divergence between the probability distributions of embeddings, with lower scores indicating greater similarity between firms’ role or culture distribution.
  Earth Mover’s Distance (EMD): Calculated the minimum ‘cost’ needed to transform one firm’s embedding distribution into another’s, identifying firms with overlapping characteristics.

Density-Based Analysis.
  (Jaccard Similarity): Measured the overlap between sets of job titles and firms associated with each resume. A high Jaccard similarity score indicated that two firms shared common roles or industry demands.

### Results:
After testing each method, Earth Mover’s Distance (EMD) provided the most accurate similarity results. EMD was particularly effective because it measured the overall ‘cost’ required to align one firm’s embedding distribution with another, making it highly sensitive to minor differences in job roles and skill requirements across firms. This sensitivity enabled EMD to capture nuanced similarities and differences, giving it an edge over simpler measures like centroid distance and pairwise average. From a constrain point of view, EMD was the most accurate similarity results requiring the least computing power, as it was able to directly compare to each firm rather than overal centriods, which could skew the overall results. 

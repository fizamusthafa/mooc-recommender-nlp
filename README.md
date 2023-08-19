# Open Online Course Recommender

This repository contains code for an Open Online Course recommender system. The recommender suggests online courses based on the content of the courses using natural language processing techniques.

## Project Overview

The Open Online Course Recommender is designed to help users discover suitable online courses by analyzing the content of course descriptions, summaries, instructors, and subjects. The recommender uses a combination of text processing, vectorization, and cosine similarity to provide relevant course recommendations.

## Natural Language Processing Techniques

The Open Online Course Recommender employs various natural language processing (NLP) techniques to process and analyze course data:

* **Text Preprocessing**: The course descriptions, summaries, instructors, and subjects are preprocessed by tokenizing the text into individual words. This step helps in breaking down the text into its fundamental units for further analysis.
* **Stemming:**: Stemming is applied to the words to reduce them to their root forms. This helps in reducing variations of words to a common form, improving the efficiency of subsequent analyses.
* **Vectorization**: The text data is converted into numerical vectors using techniques like Count Vectorization. This process represents each course as a vector of word frequencies, allowing mathematical operations to be performed on the text data.
* **Cosine Similarity**: Cosine similarity is used to measure the similarity between courses based on their vectorized representations. Courses with similar content will have a higher cosine similarity score, indicating their relevance to each other.

## Dataset
The dataset used in this project is sourced from [Kaggle](https://www.kaggle.com/datasets/imuhammad/edx-courses). The dataset contains information about 976 courses that are currently available on the edx.org platform. It provides insights into various online university-level courses across different disciplines.

### About the Dataset
* **Context:** edX is a massive open online course (MOOC) provider founded by Harvard and MIT. It hosts a wide range of online university-level courses in different disciplines.
* **Content:** The dataset contains information about 976 courses that are currently available on the edx.org platform.

## Web Application
The project also has a web application using Streamlit that allows you to interact with the Open Online Course Recommender in a user-friendly way. The web app allows you to select a course and receive recommendations for similar courses based on the course tags.
![alt text](https://github.com/fizamusthafa/mooc-recommender-nlp/blob/master/assets/example-02.png)

## Discussion
In the process of developing the Open Online Course Recommender, I modified the recommendation algorithm to provide more focused results within the same subject area. The *recommend* function was modified as follows:
```
def recommend(mooc_title):
    index = newdf[newdf['title'].str.lower() == mooc_title.lower()].index[0]
    distances = sorted(enumerate(similarity[index]), reverse=True, key=lambda x: x[1])
    selected_course = newdf.loc[index]
    
    # Filter recommended courses by the same subject as the selected course
    similar_courses = [
        newdf.iloc[i[0]] for i in distances[1:6]
        if selected_course.displayed_subject in newdf.iloc[i[0]].displayed_subject
    ]
    
    return similar_courses
```
However, it was observed that this modification led to limited recommendations. This limitation is attributed to the relatively small size of the dataset, resulting in a scarcity of courses within the same subject area. Consequently, this leads to a reduced number of recommendations. This situation underscores the critical importance of utilizing a diverse and comprehensive dataset to achieve higher accuracy in recommendations.

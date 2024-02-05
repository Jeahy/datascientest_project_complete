# New York Times API Data Pipeline - Course Project

<img src="https://github.com/Jeahy/datascientest_project_complete/blob/main/images/nyt_developers.png" align="centre">

#### Final project of the DataScientest Data Engineer course
created in collaboration with [KSuljic](https://github.com/KSuljic) and [AdelRCh](https://github.com/AdelRCh)



## Architecture 
![Pipeline Architecture](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/architecture.png)

#### Pipeline Consists of various modules:

1. Data Mining
   - https://developer.nytimes.com/apis
   - requests library
3. Database
   - MongoDB
   - database: NY_Project
   - collections: ny_articles, ny_articles_aggregated_data, times_newswire
   - JSON format
5. Data Aggregation
   - PyMongo Pipeline
   - saving aggregated data in collection
7. Data Serving
   - Website
     - Dash/Plotly
   - API
     - FastApi
     - Basic Authentication
9. Dockerization
    - Docker-Compose
    - Network
    - several ports
    - volume

#### My contributions:
- Data Mining: script to load book review data in database (that we didn't need in the end)
- Data Aggregation: of the data for parts of the Dash website
- Data Serving: part of the Dash website
- Data Serving: API



## Project Task
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/project_task.png)

## Data Aggregation
```
pipeline = [
    {
        '$group': {
            '_id': '$news_desk',
            # 'section_word_count': {'$sum': '$word_count'},
            'section_word_count': {'$avg': '$word_count'},
            'section_article_count': {'$sum': 1},
            'newest_articles': {
                '$push': {
                    'headline': '$headline',
                    'web_url': '$web_url',
                    'pub_date': '$pub_date'
                }
            }
        }
    },
    {
        '$group': {
            '_id': None,
            'average_word_count': {'$avg': '$section_word_count'},
            'total_article_count': {'$sum': '$section_article_count'},
            'sections': {
                '$push': {
                    'section': '$_id',
                    'average_word_count': {'$avg': '$section_word_count'},
                    'article_count': '$section_article_count'
                }
            },
            'all_articles': {'$push': '$newest_articles'}
        }
    },
    {
        '$project': {
            'average_word_count': 1,
            'total_article_count': 1,
            'sections': 1,
            # Flatten the array of arrays
            'flattened_articles': {'$reduce': {
                'input': '$all_articles',
                'initialValue': [],
                'in': {'$concatArrays': ['$$value', '$$this']}
            }}
        }
    },
    {
        '$unwind': '$flattened_articles'
    },
    {
        '$sort': {'flattened_articles.pub_date': -1}
    },
    {
        '$limit': 5
    },
    {
        '$group': {
            '_id': '$_id',
            'average_word_count': {'$first': '$average_word_count'},
            'total_article_count': {'$first': '$total_article_count'},
            'sections': {'$first': '$sections'},
            'newest_articles': {'$push': '$flattened_articles'}
        }
    }
]
```
## Dash Website
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/dash_page.png)

The Dash page provides:
- some basic stats: number of articles and average wordcount
- 5 latest articels that have been loaded into the database
- live article search
- on another page the average word count per article per section



## API
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/api1.png)
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/api2.png)





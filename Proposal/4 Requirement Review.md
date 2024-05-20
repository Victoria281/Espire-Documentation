## 4.1 Description of the proposed solution
![[Frame 8.png]]
This is an overview of our workflow diagram for the website. The team aims to fulfil the following deliverables:

1. An interactive website providing a structured layout for students to engage in
2. Well-designed flow that enables students to efficiently post articles and review their collection of articles
3. A fully hosted frontend and backend server

## 4.2 Application Structure

### 4.2.1 System Architecture
![[System Architecture.png]]
<span style="text-decoration:underline;">Tech Stack</span>
Frontend: ReactJS with Redux state management 
Backend: Golang
Database: PostgreSQL

<span style="text-decoration:underline;">Implementation technologies</span>
1. Collaboration: Figjam, Github, Visual Studio Code 
2. Prototyping: Figma
3. Potential Libraries: JSON web token

## 4.3 Application Functionalities
#### 4.3.1 Features

**Core**
1. Article Uploading 
2. Web scraping
3. Account Management and Role-Based Authentication
4. Article Management

**Extension**
5. Save system
6. Search functionality
7. Tag management

**Extended**
8. Recommendation algorithm 
9. Mobile Application

#### 4.3.2 Main functionalities

| Main Idea             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 1. Posting an article | We aim to efficiently guide users in posting articles through three methods. Manual Upload Though tedious, there will be the implementation of several interactive components to speed up the upload process Web scraping This implementation will lead the users to the manual upload page where they can edit the information to their liking Forking another user’s article Users will be able to add their personal touch to article posts they like  Credits will be given to the user from whom the article was forked from |
| 2. Databank           | The databank focuses on recommending article posts made by other users. The system will prioritize posts that are in our user’s interests through the information gained in the onboarding process and other users that they follow                                                                                                                                                                                                                                                                                               |
| 3. Commenting System  | To facilitate a better understanding of the articles they post, we engage in a commenting system that allows academic personnel to leave their insights that will help the user improve                                                                                                                                                                                                                                                                                                                                           |

#### 4.3.3 Frontend Interfaces

**Student Interfaces**

| Requirements   | Pages                         | Description                                                                                                                                       |
| -------------- | ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- |
| Home page      | 1.1 Loading Screen            | -                                                                                                                                                 |
|                | 1.2 Home Screen               | -                                                                                                                                                 |
| Authentication | 2.1 Login Screen              | Login with a username and password                                                                                                                |
|                | 2.2 Register Screen           | Sign up with email, username and password                                                                                                         |
|                | 2.3 On-boarding               | Allow new users to select their favourite tags                                                                                                    |
| Library        | 3.1 Library screen            | View your collection and saved article posts                                                                                                      |
|                | 3.2 Collection Screen         | View articles in the collection and synthesise their statistics                                                                                   |
| Post           | 4.1 Article Information       | View information in one article which includes basic information, tags, quotes/statistics and flashcards                                          |
|                | 4.2a Post Methods             | Show ways users can post an article such as manually inputting, searching for a post on the same article that was created before and web scraping |
|                | 4.2b Web Scraping             | Use an external tool to scrape for information through the link provided                                                                          |
|                | 4.2c Edit Article Information | Users should edit the information in the article post to their liking                                                                             |
| Databank       | 5.1 Explore Screen            | Show users article posts that might interest them                                                                                                 |
|                | 5.2 View article              | Allow users to view the information about the article posts                                                                                       |
|                | 5.3 Fork article              | Allow users to make a copy of their favourite article post and personalise it                                                                     |
|                | 5.4 User Screen               | Allow users to view other users and follow them                                                                                                   |
| Dashboard      | 6.1 Dashboard Screen          | Display user statistics                                                                                                                           |


#### 4.3.4 Data Models
##### 4.3.4.1 ERD diagram
![[ERD.png]]
##### 4.3.4.2 Database Tables and description
###### 4.3.4.2a User
| Column Name |           Type           | Nullable |    Default Value   | Constraint Types |
|:-----------:|:------------------------:|:--------:|:------------------:|:----------------:|
| id          | uuid                     | Not Null | uuid_generate_v4() | Primary Key      |
| name        | character varying(255)   | Not Null |                    |                  |
| password    | text                     | Not Null |                    |                  |
| role        | text                     | Null     |                    |                  |
| createdAt   | timestamp with time zone | Not Null | now()              |                  |
| updatedAt   | timestamp with time zone | Not Null | now()              |                  |
| deletedAt   | timestamp with time zone | Null     |                    |                  |

###### 4.3.4.2b UserCollection
| Column Name |           Type           | Nullable |    Default Value   |   Constraint Type   |
|:-----------:|:------------------------:|:--------:|:------------------:|:-------------------:|
| id          | uuid                     | Not Null | uuid_generate_v4() | Primary Key         |
| uid         | uuid                     | Null     |                    | Foreign Key (Users) |
| name        | text                     | Not Null |                    |                     |
| createdAt   | timestamp with time zone | Not Null | now()              |                     |
| updatedAt   | timestamp with time zone | Not Null | now()              |                     |
| deletedAt   | timestamp with time zone | Null     |                    |                     |
| deletedAt   | timestamp with time zone | Null     |                    |                     |

###### 4.3.4.2c ArticleCollection
|  Column Name  |           Type           | Nullable |    Default Value   |      Constraint Type     |
|:-------------:|:------------------------:|:--------:|:------------------:|:------------------------:|
| id            | uuid                     | Not Null | uuid_generate_v4() | Primary Key              |
| article_id    | uuid                     | Null     |                    | Foreign Key (Articles)   |
| collection_id | uuid                     | Null     |                    | Foreign Key (Collection) |
| createdAt     | timestamp with time zone | Not Null | now()              |                          |
| updatedAt     | timestamp with time zone | Not Null | now()              |                          |
| deletedAt     | timestamp with time zone | Null     |                    |                          |
| deletedAt     | timestamp with time zone | Null     |                    |                          |

###### 4.3.4.2d Articles
| Column Name |           Type           | Nullable |    Default Value   |   Constraint Type   |
|:-----------:|:------------------------:|:--------:|:------------------:|:-------------------:|
| id          | uuid                     | Not Null | uuid_generate_v4() | Primary Key         |
| uid         | uuid                     | Null     |                    | Foreign Key (Users) |
| parentid    | uuid                     | Null     |                    | Foreign Key (Users) |
| name        | text                     | Not Null |                    |                     |
| use         | text                     | Not Null |                    |                     |
| description | text                     | Not Null |                    |                     |
| createdAt   | timestamp with time zone | Not Null | now()              |                     |
| updatedAt   | timestamp with time zone | Not Null | now()              |                     |
| deletedAt   | timestamp with time zone | Null     |                    |                     |

###### 4.3.4.2e ArticleLinks
| Column Name |           Type           | Nullable |    Default Value   |     Constraint Type    |
|:-----------:|:------------------------:|:--------:|:------------------:|:----------------------:|
| id          | uuid                     | Not Null | uuid_generate_v4() | Primary Key            |
| article_id  | uuid                     | Null     |                    | Foreign Key (Articles) |
| isMain      | integer                  | Not Null | 0                  |                        |
| link        | text                     | Not Null |                    |                        |
| createdAt   | timestamp with time zone | Not Null | now()              |                        |
| updatedAt   | timestamp with time zone | Not Null | now()              |                        |
| deletedAt   | timestamp with time zone | Null     |                    |                        |
###### 4.3.4.2f ArticleQuotes 
| Column Name |           Type           | Nullable |    Default Value   |     Constraint Type    |
|:-----------:|:------------------------:|:--------:|:------------------:|:----------------------:|
| id          | uuid                     | Not Null | uuid_generate_v4() | Primary Key            |
| article_id  | uuid                     | Null     |                    | Foreign Key (Articles) |
| grp_num     | integer                  | Null     | 0                  | Foreign Key (Users)    |
| priority    | integer                  | Null     | 0                  | Foreign Key (Pens)     |
| fact        | text                     | Not Null |                    |                        |
| createdAt   | timestamp with time zone | Not Null | now()              |                        |
| updatedAt   | timestamp with time zone | Not Null | now()              |                        |
| deletedAt   | timestamp with time zone | Null     |                    |                        |

###### 4.3.4.2g ArticleFlashcard
| Column Name |           Type           | Nullable |    Default Value   |     Constraint Type    |
|:-----------:|:------------------------:|:--------:|:------------------:|:----------------------:|
| id          | uuid                     | Not Null | uuid_generate_v4() | Primary Key            |
| article_id  | uuid                     | Null     |                    | Foreign Key (Articles) |
| answer      | text                     | Null     |                    |                        |
| question    | text                     | Null     |                    |                        |
| tries       | integer                  | Not Null | 0                  |                        |
| wrong       | integer                  | Not Null | 0                  |                        |
| createdAt   | timestamp with time zone | Not Null | now()              |                        |
| updatedAt   | timestamp with time zone | Not Null | now()              |                        |
| deletedAt   | timestamp with time zone | Null     |                    |                        |

###### 4.3.4.2h CollectionAttempts
|     Column Name     |           Type           | Nullable |    Default Value   |         Constraint Type        |
|:-------------------:|:------------------------:|:--------:|:------------------:|:------------------------------:|
| id                  | uuid                     | Not Null | uuid_generate_v4() | Primary Key                    |
| uid                 | uuid                     | Null     |                    | Foreign Key (Users)            |
| collection_id       | uuid                     | Null     |                    | Foreign Key (Collection)       |
| articleflashcard_id | uuid                     | Null     |                    | Foreign Key (ArticleFlashcard) |
| attemptnum          | integer                  | Not Null | 0                  |                                |
| score               | integer                  | Not Null | 0                  |                                |
| createdAt           | timestamp with time zone | Not Null | now()              |                                |
| updatedAt           | timestamp with time zone | Not Null | now()              |                                |
| deletedAt           | timestamp with time zone | Null     |                    |                                |

###### 4.3.4.2i UserFollowers
| Column Name |           Type           | Nullable |    Default Value   |   Constraint Type   |
|:-----------:|:------------------------:|:--------:|:------------------:|:-------------------:|
| id          | uuid                     | Not Null | uuid_generate_v4() | Primary Key         |
| follower_id | uuid                     | Null     |                    | Foreign Key (Users) |
| followed_id | uuid                     | Null     |                    | Foreign Key (Users) |
| createdAt   | timestamp with time zone | Not Null | now()              |                     |
| updatedAt   | timestamp with time zone | Not Null | now()              |                     |
| deletedAt   | timestamp with time zone | Null     |                    |                     |
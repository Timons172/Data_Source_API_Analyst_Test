# GitHub API Test

## Project Overview

This project demonstrates the usage of the GitHub REST API to extract, process, and analyze data as part of the DataSource Analyst Challenge.
The focus is on programmatically interacting with the GitHub API to retrieve repositories, commits, and content data while implementing pagination, error handling, and rate limit management.
The code is implemented in Python using Google Colab.

---

## Contents
- [Objective](#objective)
- [Features](#features)  
- [Setup Instructions](#setup-instructions)  
- [Project Structure](#project-structure)  
- [Endpoints Used](#endpoints-used)
- [Additional Context and Comments](#additional-context-and-comments)
- [Results](#results)

---

## Objective
The goal of this project is to demonstrate:
- Proficiency in working with APIs
- Ability to handle data extraction, pagination, and error handling
- Understanding of rate limit management and troubleshooting

---

## Features
- Search public repositories based on a query string
- Fetch commit history for a specific repository
- Retrieve file and directory contents from repositories
- Implement pagination and error handling
- Log errors and save results to JSON for further analysis

---

## Setup Instructions
- Python 3.x installed
- Google Colab for code execution
- A valid GitHub Personal Access Token with the following permissions:
  - `public repo`

### Steps
1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/Data-Source-API-Analyst-Test.git
   cd Data-Source-API-Analyst-Test
2. Open GitHub_API_Test.ipynb in Google Colab
3. Replace "your-token" in the code with your GitHub Personal Access Token
4. Run the notebook to execute API calls and retrieve data

## Project Structure
```
Data-Source-API-Analyst-Test/  
    README.md                   # Project documentation  
    /Content/
        API_Documentation.md    # Detailed API usage documentation  
        github_api_test.py      # API extraction script  
    /Postman_Collection/
        GitHub_API_Test.ipynb   # Colab notebook for API extraction  
        repositories.json       # Sample extracted repository data  
        commits.json            # Sample extracted commit data  
        contents.json           # Sample extracted content data  
```

## Endpoints Used
- Authentication: GET /user
  (Validate the token and access level)
- Search Repositories: GET /search/repositories
  (Retrieve a list of repositories matching a search query)
- Fetch Commits: GET /repos/{owner}/{repo}/commits
  (Get the commit history of a repository)
- Fetch Contents: GET /repos/{owner}/{repo}/contents/{path}
  (Retrieve files or directory contents of a repository)
- Rate Limit: GET /rate_limit
  (Monitor the remaining request quota)

Detailed documentation for each endpoint can be found in API_Documentation.md

## Additional Context and Comments
1. GitHub API Exploration:  
   The project heavily relies on the GitHub REST API. Extensive research into rate limits, request headers, and response handling was conducted to ensure reliability
2. Error Handling:
   - Unknown response structures are logged for manual inspection
   - Common errors can be found in API_Documentation.md
3. Pagination and Rate Limits:  
   Pagination is managed dynamically with a fetch_all_pages function. The function adapts to empty responses or errors by breaking the loop or retrying the request
4. Extensibility:  
   The script is designed to be modular and easily extensible for additional GitHub API endpoints or changes in API versions
5. Future improvements could include integrating automated tests for API endpoints and adding support for GraphQL queries

## Results
Successfully retrieved and saved:  
- Repository data for the query "python"  
- Commit history for octocat/Hello-World  
- Directory contents of Timons172/Library-Management-System  
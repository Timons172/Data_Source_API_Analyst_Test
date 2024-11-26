# API Documentation

## Overview
This document provides a detailed explanation of the GitHub API endpoints used for the DataSource Analyst Challenge.
It covers authentication, key endpoints, pagination, error handling, and rate limit management.

---

## Contents
[1. Authentication](#1-authentication)  
[2. Search Repositories](#2-search-repositories)  
[3. Fetch Commits](#3-fetch-commits)  
[4. Fetch Contents](#4-fetch-contents)  
[5. Rate Limits](#5-rate-limits)  
[6. Pagination](#6-pagination)  
[7. Error Handling](#7-error-handling)  
[8. Testing](#8-testing)  
[9. Notes](#9-notes)  

---

## 1. Authentication

### Endpoint
    GET /user

### Purpose
- Verify the authentication token and confirm access to GitHub API.

### Request
    GET https://api.github.com/user
    Headers:
        Authorization: Bearer <your_token>
        Accept: application/vnd.github+json
        X-GitHub-Api-Version: 2022-11-28

### Response
    200 - OK (Authentication successful)  
    401 - Unauthorized (Invalid token or insufficient permissions)

---

## 2. Search Repositories

### Endpoint
    GET /search/repositories

### Purpose
- Search for public repositories based on a query string.

### Request
    GET https://api.github.com/search/repositories?q=<query>&per_page=<number>&page=<number>
    Headers:
        Authorization: Bearer <your_token>
        Accept: application/vnd.github+json
        X-GitHub-Api-Version: 2022-11-28

### Parameters
    q (string): The search query (e.g., “python”)
	per_page (integer): Number of results per page (default: 30, max: 100)
    page (integer): Page number to retrieve

### Response
	200 - OK (Returns a list of repositories matching the query)
	403 - Forbidden (Rate limit exceeded)

---

## 3. Fetch Commits

### Endpoint
    GET /repos/{owner}/{repo}/commits

### Purpose
- Retrieve commit history for a specific repository.

### Request
    GET https://api.github.com/repos/{owner}/{repo}/commits?per_page=<number>&page=<number>
    Headers:
        Authorization: Bearer <your_token>
        Accept: application/vnd.github+json
        X-GitHub-Api-Version: 2022-11-28

### Parameters
	owner (string): Repository owner
	repo (string): Repository name
	per_page (integer): Number of results per page (default: 30, max: 100)
	page (integer): Page number to retrieve

### Response
	200 - OK (List of commits)
	403 - Forbidden (Rate limit exceeded)

---

## 4. Fetch Contents

### Endpoint
    GET /repos/{owner}/{repo}/contents/{path}

### Purpose
- Retrieve the contents of a directory or file in a repository.

### Request
    GET https://api.github.com/repos/{owner}/{repo}/contents/{path}
    Headers:
        Authorization: Bearer <your_token>
        Accept: application/vnd.github+json
        X-GitHub-Api-Version: 2022-11-28

### Parameters
	owner (string): Repository owner
	repo (string): Repository name
	path (string): File or directory path (leave empty for root)

### Response
	200 - OK (Returns the directory or file contents)
	403 - Forbidden (Rate limit exceeded)
	404 - Not Found (Invalid path, owner, or repo)

---

## 5. Rate Limits

### Endpoint
    GET /rate_limit

### Purpose
- Check the current rate limit status for authenticated requests.

### Request
    GET https://api.github.com/rate_limit
    Headers:
        Authorization: Bearer <your_token>
        Accept: application/vnd.github+json
        X-GitHub-Api-Version: 2022-11-28

### Response
	200 - OK (Provides rate limit details)
	403 - Forbidden (Invalid token)

---

## 6. Pagination

### Purpose
- Handle large datasets by fetching results across multiple pages.

### Parameters
	per_page (integer): Number of items per page
	page (integer): Page number to retrieve

### Implementation
    def fetch_all_pages(endpoint, headers, params):
        all_results = []
        page = 1
        while True:
            print(f"Fetching page {page}...")
            check_rate_limit()
            results = fetch_function(*args, **kwargs, page=page)
            if not results:
                print("No more results to fetch.")
                break
            all_results.extend(results)
            page += 1
            time.sleep(0.5)
        return all_results

---

## 7. Error Handling

### Common Errors
    1. 401 (Unauthorized)
        - Ensure the token is valid and included in the Authorization header
        - Verify token permissions in the GitHub settings
    2. 403 (Forbidden)
        - Rate limit exceeded; check /rate_limit to monitor limits
        - Wait until reset time before retrying requests
    3. 404 (Not Found)
        - Ensure correct values for owner, repo, or path

---

## 8. Testing

### Tools
- Google Colab: Used for scripting, testing, and validating API responses

### Validation
- Sample responses were printed to verify correctness
- Errors were captured and handled with appropriate fallback mechanisms

---

## 9. Notes
- Rate Limits: Authenticated requests have a limit of 5000 requests per hour
- Security: Do not expose your personal access token in public repositories
- Documentation: Refer to GitHub REST API Docs for additional details

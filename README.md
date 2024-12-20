# Data-Source-API-Analyst-Test

## Table of Contents

- [Introduction](#introduction)
- [Client Requirements](#client-requirements)
- [Step 1: Exploring GitHub API](#step-1-exploring-github-api)
- [Step 2: Setting Up GitHub Repository](#step-2-setting-up-github-repository)
- [Step 3: Data Extraction Using Google Colab](#step-3-data-extraction-using-google-colab)
- [Step 4: Troubleshooting Guide](#step-4-troubleshooting-guide)
- [Step 5: Results](#step-5-results)
- [Step 6: Reflection](#step-6-reflection)

## Introduction

This repository contains the homework assignment for the role of API Data Source Analyst. The goal of the assignment is to demonstrate an understanding of working with APIs, the ability to handle data extraction requirements, and an approach to troubleshooting.

## Client Requirements

Core Functional Requirements

- **Repository Search Functionality**
    - The system must allow searching for public repositories on GitHub using various criteria, such as keywords, programming languages, or repository topics.
    - Search results should include essential metadata, such as repository name, owner, description, stars, forks, and primary programming language.

- **Commit History Retrieval**
    - The system must retrieve the full commit history for a specified repository.
    - Commit data must include commit messages, author information, timestamps, and commit SHA identifiers.
    - The solution must handle paginated commit data efficiently.

- **Repository Content Access**
    - The system must support accessing the contents of a repository or specific files and directories within it.
    - Metadata for files (e.g., file type, size, encoding) must be retrievable.
    - The solution must allow navigation through nested directory structures.

- **Authentication**
    - The system must utilize a secure authentication mechanism through a GitHub Personal Access Token (PAT).
    - The authentication process should ensure compliance with GitHub's API requirements and allow for extended rate limits for requests.

- **Error Handling and Logging**
    - The system must include robust error-handling mechanisms to address issues such as:
        Authentication errors (401 Unauthorized).
        Rate limit exceedances (403 Forbidden).
        Invalid endpoints or parameters (404 Not Found).
        Network issues (Connection Timeout or Connection Errors).
    - Detailed logging must be implemented for all API interactions to facilitate debugging and monitoring.

- **Rate Limit Management**
    - The system must monitor API usage and implement mechanisms to handle rate limits effectively.
    - If the rate limit is reached, the system should delay further requests until the reset period.

## Step 1: Exploring GitHub API

### Client Needs

- Search for repositories (public)
- Commits
- Repository contents

### Selected API Endpoints

#### Search Repositories:
- **Endpoint**: `GET /search/repositories`
- **Description**: Search for public repositories based on a query.
- **Documentation**: [Search repositories](https://docs.github.com/en/rest/search#search-repositories)

#### List Commits:
- **Endpoint**: `GET /repos/{owner}/{repo}/commits`
- **Description**: Get a list of commits in a repository.
- **Documentation**: [List commits](https://docs.github.com/en/rest/commits/commits#list-commits)

#### Get Repository Content:
- **Endpoint**: `GET /repos/{owner}/{repo}/contents/{+path}`
- **Description**: Get the contents of a file or directory in a repository.
- **Documentation**: [Get repository content](https://docs.github.com/en/rest/repos/contents#get-repository-content)

### API Features

- **Authentication**: Uses a Personal Access Token (PAT) to increase request limits.
- **Pagination**: Handles pages using `page` and `per_page` parameters.
- **Rate Limits**: Authenticated requests have a limit of 5000 requests per hour.
- **Error Handling**: Implements handling of HTTP errors and API-specific errors.

## Step 2: Setting Up GitHub Repository

A new public repository `Data-Source-API-Analyst-Test` has been created.

### Repository Structure

Data-Source-API-Analyst-Test/

- `README.md`: The main file describing the project's purpose and approach.
- `Content/`:
  - `api_documentation.md`: Detailed documentation on API usage.
  - `github_api_extraction.ipynb`: Jupyter Notebook with Python code for authentication, data extraction, error handling, rate limits, and pagination.
  - `troubleshooting_guide.md`: Guide to resolving common issues.
  - `data_cleaning_approach.md`: Document describing the data cleaning approach.

## Step 3: Data Extraction Using Google Colab

Data extraction has been implemented using a Jupyter Notebook (`github_api_extraction.ipynb`) in Google Colab.

### Features

- **Authentication**: Secure handling of the Personal Access Token.
- **Functions**: Modular functions for each API endpoint.
- **Pagination and Rate Limits**: Functions to handle pages and respect rate limits.
- **Error Handling**: Comprehensive error handling and logging.
- **Documentation**: Each function is documented with docstrings and comments.
- **Best Practices**: Adherence to PEP 8 coding style and industry standards.

### Notebook Content

- **Import Libraries**: Import necessary Python libraries.
- **Authentication**: Setup using a secure method.
- **Helper Functions**: Functions for handling rate limits, errors, and pagination.
- **API Functions**:
  - `search_repositories()`: Search for public repositories.
  - `get_commits()`: Get commits from a repository.
  - `get_repo_contents()`: Access repository contents.
- **Usage Examples**: Demonstration of each function with sample data.
- **Conclusion**: Summary of the work done and possible next steps.

### Function Documentation

Each function in `github_api_extraction.ipynb` is documented with detailed docstrings describing its purpose, parameters, return values, and possible exceptions.

#### Example:

```python
def search_repositories(query, per_page=30, max_pages=5):
    """
    Search for public repositories based on a query.

    Parameters:
        query (str): The search query.
        per_page (int, optional): Number of results per page. Default is 30.
        max_pages (int, optional): Maximum number of pages to retrieve. Default is 5.

    Returns:
        list: A list of found repositories.

    Raises:
        HTTPError: If an HTTP error occurs.
        Exception: For other errors.
    """
    ...
```

## Step 4: Troubleshooting Guide

A troubleshooting guide (`Content/troubleshooting_guide.md`) has been created, covering common issues such as authentication errors, rate limit exceedances, and network errors.

### Content

- **Common Issues and Solutions**:
  - **401 Unauthorized Error**: Check the authentication token.
  - **403 Forbidden Error**: Handle rate limits and access permissions.
  - **404 Not Found Error**: Verify endpoints and parameters.
  - **ConnectionError or Timeout**: Retry on network errors.
  - **JSON Decode Error**: Ensure the response format is correct.
- **Rate Limit Handling**: Describes how to manage rate limits using response headers.
- **Tips for Effective Troubleshooting**: Best practices for debugging, including logging and using community resources for solutions.

## Step 5: Results

The result files are saved in the GitHub repository:

- `Content/github_api_extraction.ipynb`: Jupyter Notebook with complete code and documentation.

## Step 6: Reflection
Reflection

Completing this assignment has allowed me to deepen my understanding of the GitHub API and best practices for API interaction and data extraction. Key takeaways include:

- `API Research`: Understanding the endpoints, parameters, and constraints is crucial before implementation.
- `Authentication and Security`: Handling authentication securely and efficiently maximizes rate limits and ensures compliance.
- `Error Handling`: Implementing comprehensive error handling and logging facilitates debugging and improves robustness.
- `Rate Limit Management`: Being aware of rate limits and implementing mechanisms to handle them prevent disruptions in data extraction.
- `Code Organization`: Writing modular, reusable code with proper documentation enhances maintainability and scalability.
- `Data Cleaning`: Planning for data validation and cleaning ensures the extracted data is reliable and suitable for analysis.
- `Documentation`: Thorough documentation of the approach, code, and troubleshooting guides aids in collaboration and future development.
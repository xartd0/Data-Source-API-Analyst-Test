# API Documentation
## Overview
This document provides detailed information about the GitHub API endpoints used to meet the client's needs.
## Authentication

    Method: Personal Access Token (PAT)
    Header: `Authorization: token <YOUR_PERSONAL_ACCESS_TOKEN>`
    Note: Authentication increases the rate limit to 5,000 requests per hour.

## Endpoints
### 1. Search Repositories

    Endpoint: [GET https://api.github.com/search/repositories](https://api.github.com/search/repositories)
    Parameters:
        `q` (string): The search query.
        `sort` (string, optional): The sort field. Can be `stars`, `forks`, `help-wanted-issues`, or `updated`.
        `order` (string, optional): `asc` or `desc`. Default: `desc`.
        `per_page` (integer, optional): Number of results per page. Default: 30.
        `page` (integer, optional): Page number.
    Usage:
        Example: Search for repositories related to "machine learning".

        [GET https://api.github.com/search/repositories?q=machine+learning&per_page=30&page=1](https://api.github.com/search/repositories?q=machine+learning&per_page=30&page=1)

    Documentation: [Search repositories](https://docs.github.com/en/rest/search#search-repositories)

### 2. List Commits

    Endpoint: [GET https://api.github.com/repos/{owner}/{repo}/commits](https://api.github.com/repos/{owner}/{repo}/commits)
    Parameters:
        `sha` (string, optional): SHA or branch to start listing commits from.
        `path` (string, optional): Only commits containing this file path will be returned.
        `author` (string, optional): GitHub login or email address by which to filter commits.
        `since` (string, optional): ISO 8601 date. Only commits after this date will be returned.
        `until` (string, optional): ISO 8601 date. Only commits before this date will be returned.
        `per_page` (integer, optional): Number of results per page. Default: 30.
        `page` (integer, optional): Page number.
    Usage:
        Example: List commits from the main branch of the repository octocat/Hello-World.

        [GET https://api.github.com/repos/octocat/Hello-World/commits?sha=main&per_page=30&page=1](https://api.github.com/repos/octocat/Hello-World/commits?sha=main&per_page=30&page=1)

    Documentation: [List commits](https://docs.github.com/en/rest/commits/commits#list-commits)

### 3. Get Repository Contents

    Endpoint: [GET https://api.github.com/repos/{owner}/{repo}/contents/{+path}](https://api.github.com/repos/{owner}/{repo}/contents/{+path})
    Parameters:
        `ref` (string, optional): The name of the commit/branch/tag. Default: repository default branch.
    Usage:
        Example: Get contents of the root directory of octocat/Hello-World.

        [GET https://api.github.com/repos/octocat/Hello-World/contents/](https://api.github.com/repos/octocat/Hello-World/contents/)

    Documentation: [Get repository content](https://docs.github.com/en/rest/repos/contents#get-repository-content)

## Pagination

    Use `per_page` and `page` parameters to handle pagination.
    The `Link` header in the response contains URLs for next, prev, first, and last pages.

## Rate Limits

    Unauthenticated requests: 60 requests per hour.
    Authenticated requests: 5,000 requests per hour.
    Checking Rate Limit:
        Endpoint: [GET https://api.github.com/rate_limit](https://api.github.com/rate_limit)
    Headers:
        `X-RateLimit-Limit`: The maximum number of requests you're permitted to make per hour.
        `X-RateLimit-Remaining`: The number of requests remaining in the current rate limit window.
        `X-RateLimit-Reset`: The time at which the current rate limit window resets in UTC epoch seconds.

## Error Handling

    Common HTTP Status Codes:
        200 OK: The request was successful.
        401 Unauthorized: Authentication failed or missing.
        403 Forbidden: Access denied, or rate limit exceeded.
        404 Not Found: Resource not found.
        422 Unprocessable Entity: Validation error.
    Error Response Format:
        JSON object containing `message` and `documentation_url` fields.

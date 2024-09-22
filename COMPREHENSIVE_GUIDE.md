# Twitter Clone Project: Comprehensive Guide

## Table of Contents
1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Project Structure](#project-structure)
4. [Setup Instructions](#setup-instructions)
   - [Set up the project](#step-1-set-up-the-project)
   - [Set up a virtual environment](#step-2-set-up-a-virtual-environment)
   - [Install dependencies](#step-3-install-dependencies)
   - [Set up the database](#step-4-set-up-the-database)
   - [Set up GitHub Actions workflow](#step-5-set-up-github-actions-workflow)
   - [Set up a sample test](#step-6-set-up-a-sample-test)
   - [Initialize Git repository](#step-7-initialize-git-repository)
   - [Run the tests](#step-8-run-the-tests)
5. [Dependencies](#dependencies)
6. [GitHub Actions Workflow](#github-actions-workflow)
7. [Sample Test](#sample-test)
8. [Next Steps](#next-steps)

## Project Overview

This is a Twitter clone project for demonstration purposes. It serves as a template for building a social media application using Python and Flask.

## Prerequisites

Before you begin, ensure you have the following installed on your system:
- Python 3.7.13
- PostgreSQL
- Visual Studio Code (VSCode)
- Git

## Project Structure

The project structure should look like this:

```
twitter-clone-test/
├── .github/
│   └── workflows/
│       └── public_workflow.yml
├── tests/
│   └── test_sample.py
├── README.md
├── requirements.txt
├── SETUP_INSTRUCTIONS.md
└── COMPREHENSIVE_GUIDE.md (this file)
```

## Setup Instructions

Follow these steps to set up the Twitter clone project from scratch in Visual Studio Code (VSCode).

### Step 1: Set up the project

1. Open VSCode and create a new folder named `twitter-clone-test`.
2. Open a terminal in VSCode and navigate to the project folder.

### Step 2: Set up a virtual environment

1. Create a virtual environment:
   ```
   python -m venv venv
   ```
2. Activate the virtual environment:
   - On Windows: `venv\Scripts\activate`
   - On macOS/Linux: `source venv/bin/activate`

### Step 3: Install dependencies

1. Create a `requirements.txt` file in the root directory with the content from the [Dependencies](#dependencies) section.
2. Install the dependencies:
   ```
   pip install -r requirements.txt
   ```

### Step 4: Set up the database

1. Create a new PostgreSQL database named `warbler-test`.
2. Update the database connection string in your application configuration to:
   ```
   postgresql://postgres:postgres@localhost:5432/warbler-test
   ```

### Step 5: Set up GitHub Actions workflow

1. Create a `.github/workflows` directory in your project root.
2. Create a file named `public_workflow.yml` in the `.github/workflows` directory with the content from the [GitHub Actions Workflow](#github-actions-workflow) section.

### Step 6: Set up a sample test

1. Create a `tests` directory in your project root.
2. Create a file named `test_sample.py` in the `tests` directory with the content from the [Sample Test](#sample-test) section.

### Step 7: Initialize Git repository

1. Initialize a new Git repository:
   ```
   git init
   ```
2. Create a `.gitignore` file to exclude unnecessary files:
   ```
   venv/
   __pycache__/
   *.pyc
   .pytest_cache/
   ```
3. Make your initial commit:
   ```
   git add .
   git commit -m "Initial commit"
   ```

### Step 8: Run the tests

1. Run the tests using pytest:
   ```
   pytest
   ```

## Dependencies

The project uses the following dependencies, which are listed in the `requirements.txt` file:

```
Flask==2.0.1
Flask-SQLAlchemy==2.5.1
Flask-WTF==0.15.1
Flask-Login==0.5.0
Flask-Migrate==3.1.0
SQLAlchemy==1.4.23
Werkzeug==2.0.1
psycopg2-binary==2.9.1
pytest==6.2.5
flake8==3.9.2
beautifulsoup4==4.10.0
```

## GitHub Actions Workflow

The project includes a GitHub Actions workflow for running tests on pull requests. The workflow is defined in `.github/workflows/public_workflow.yml`:

```yaml
name: Tests

on: [pull_request]

permissions:
  contents: read

jobs:
  build:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:latest
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
          POSTGRES_DB: warbler-test
        ports:
          - 5432:5432
        options: --health-cmd pg_isready --health-interval 10s --health-timeout 5s --health-retries 5

    steps:
    - uses: actions/checkout@v3
      with:
        fetch-depth: 0
    - name: Set up Python 3.7.13
      uses: actions/setup-python@v3
      with:
        python-version: "3.7.13"
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install flake8 pytest bs4 Flask-Migrate psycopg2-binary
        if [ -f requirements.txt ]; then pip install -r requirements.txt; fi
    - name: Run the tests
      run: |
        export DATABASE_URL="postgresql://postgres:postgres@localhost:5432/warbler-test"
        pytest
```

## Sample Test

A sample test is included in `tests/test_sample.py`:

```python
def test_sample():
    assert True, "This test should always pass"
```

## Next Steps

After setting up the project, consider the following next steps:

- Implement the core functionality of your Twitter clone using Flask and SQLAlchemy.
- Create additional tests for your application's features.
- Set up a development database and configure your application to use it.
- Implement user authentication and authorization using Flask-Login.
- Create templates for your views using a templating engine like Jinja2.

Remember to commit your changes regularly and push them to a remote repository if you're using GitHub or a similar platform.

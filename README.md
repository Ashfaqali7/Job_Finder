# Job_Finder

An automated job searching and matching tool that helps users find relevant job opportunities based on their skills.

## Overview

Job_Finder automates the process of searching for jobs, filtering based on your skills, and even creating tailored resumes for each opportunity. The system uses a workflow-driven approach to execute various tasks including job scraping, AI-based filtering, resume optimization, and application tracking.

## Workflow

The system is driven by a workflow defined in `workflow.json` which consists of the following key components:

### 1. Job Scraping
- Uses HTTP Request node to fetch job listings from LinkedIn
- Configured to search for React.js jobs (can be modified for other technologies)
- Returns up to 100 job listings per execution

### 2. AI-Based Job Filtering
- Uses OpenAI's GPT-4.1-MINI model to analyze job descriptions
- Filters jobs based on candidate's skills (modifi according to your needs):
  - Core skills: React.js, Next.js, Node.js, JavaScript (ES6+), TypeScript
  - Backend & Database: Express, MongoDB, Firebase, Supabase
  - Frontend & UI: HTML5, CSS, Tailwind CSS, Bootstrap, Material-UI, Shadcn UI
  - DevOps & Tooling: Docker, CI/CD (Git), n8n
- Only considers jobs that require at least two core skills as relevant

### 3. Resume Optimization
- Retrieves original resume from Google Docs
- For each relevant job, uses AI to optimize the resume specifically for that position
- Creates a new Google Doc with the tailored resume

### 4. Application Tracking
- Stores job details in a Google Sheet for tracking purposes
- Includes job title, company name, description, and application materials

### 5. Automation Schedule
- Workflow is triggered automatically every 3 hours
- Implements rate limiting with wait times to avoid overwhelming services

## Prerequisites

- OpenAI API key
- Google Docs and Sheets API access
- n8n workflow engine

## Setup

1. Configure the LinkedIn job search URL in the HTTP Request node
2. Set up your Google Docs and Sheets credentials
3. Update the candidate's skills and resume content in the appropriate nodes
4. Configure the Google Sheet ID for application tracking
5. Set up the OpenAI API credentials

## How It Works

1. The workflow starts automatically every 3 hours
2. Fetches current job listings from LinkedIn based on configured search
3. Processes each job through an AI validation system to check relevance
4. For relevant jobs:
   - Creates a tailored resume optimized for that specific position
   - Saves the resume to Google Docs
   - Records job details in a Google Sheet for tracking
5. Waits for a specified interval before processing the next batch

## Customization

To adapt this workflow for different skills or job platforms:
- Modify the job search URL in the HTTP Request node
- Update the candidate's skills in the Validator node prompt
- Adjust the resume content in the Resume Writer node
- Change the filtering criteria in the AI prompts
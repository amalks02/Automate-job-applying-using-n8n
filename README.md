## Automated Job Application Workflow (n8n + Google Gemini + Gmail + Google Sheets)
### Project Description

This project automates the end-to-end process of job discovery, evaluation, and application using n8n
.
The workflow runs daily, fetches job listings from LinkedIn RSS feeds, extracts relevant details with Google Gemini LLMs, evaluates suitability based on a candidate’s resume, generates personalized cover letters, and sends job applications via Gmail.
All processed jobs are also stored in Google Sheets for tracking.

### Features

✅ Job Fetching – Fetches LinkedIn job listings daily via RSS feed.
✅ Job Parsing – Uses Gemini Model 1 to extract job details (company, role, benefits, description, contact, domain).
✅ Filtering – Only processes jobs with contact person details.
✅ Job Match Scoring – Uses Gemini Model 2 to rate job fit against candidate’s skills/resume.
✅ Cover Letter Generation – Gemini Model 3 creates tailored cover letters per job.
✅ Data Processing – JS code nodes remove nesting and format JSON outputs.
✅ Google Sheets Integration – Saves job details, scores, and cover letters for future reference.
✅ Email Notification – Sends customized applications to the hiring contact via Gmail.

## Workflow Setup
### Nodes Overview

- Schedule Trigger – Runs daily at 10:00 AM.

- RSS Read Node – Reads LinkedIn jobs feed.

- Loop Over Items – Iterates through job postings.

- HTTP Request Node – Fetches full LinkedIn job page.

- Gemini Model 1 (Job Extractor) – Extracts job data in JSON structure:

{
  "Company Name": "",
  "Job role": "",
  "Benefits": "",
  "Job Description": "",
  "Location": "",
  "Contact": "",
  "Company domain": "",
  "Contact Email": ""
}


- JS Code Node – Removes nesting from Gemini response.

- IF Node – Filters only jobs containing contact person details.

- Gemini Model 2 (Scoring Bot) – Scores job fit based on candidate resume (out of 5).

{ "Score": "" }


- JS Code Node – Cleans score output.

- Gemini Model 3 (Cover Letter Generator) – Generates personalized cover letters.

{ "Cover letter": "" }


- JS Code Node – Cleans cover letter output.

- Google Sheets Node – Appends processed job details, score, and cover letter.

- Gmail Node – Sends application email with cover letter to hiring contact.

## Run Instructions
🔹 Run Locally

- Install n8n
:

- npm install n8n -g
- n8n start


- Import workflow JSON (exported from n8n).

- Configure credentials:

  Google Gemini API (LLM)

  Google Sheets API (for storing results)

  Gmail API (for sending applications)

- Set RSS feed URL for LinkedIn jobs.

🔹 Run the workflow manually or let the Schedule Trigger run daily at 10 AM.

🔹 Run with n8n Cloud

- Sign up at n8n.io Cloud
.

- Import the workflow.

- Add credentials (Gemini, Google Sheets, Gmail).

- Deploy – workflow will run daily as configured.

# AI-Powered Ed-Tech Reviewer for Google Docs

![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)
![Built with: Google Apps Script](https://img.shields.io/badge/Built_with-Google_Apps_Script-orange.svg)

An AI-powered tool for Google Docs that automates the creation of comprehensive educational technology reviews.

### Demo

*(This is where you should include a short screen recording GIF of the tool in action. Replace the `URL_TO_YOUR_DEMO_GIF` placeholder below with a direct link to your hosted GIF.)*

<p align="center">
  <img src="URL_TO_YOUR_DEMO_GIF" alt="Demo of the AI Ed-Tech Reviewer" width="600"/>
</p>

### Why I Built This

As an instructional design intern at the University of Florida, I saw firsthand how much time and effort goes into evaluating new educational technologies. The process involves extensive research, testing, and documentation. I developed this tool to dramatically streamline that workflow, allowing educators and instructional designers to generate a comprehensive, well-formatted first draft of a review in under two minutes, freeing them up to focus on higher-level analysis and pedagogy.

### Features

*   **One-Click Generation:** Run the entire review process from a simple menu item in Google Docs.
*   **Context-Aware Analysis:** Prompts the user for their institution to generate a review that is tailored and relevant.
*   **Sophisticated AI Prompting:** Utilizes a detailed, structured master prompt to ensure high-quality, consistent output from the AI.
*   **Dynamic Document Creation:** Automatically generates a new, cleanly formatted Google Doc for each review based on a customizable template.
*   **Zero Dependencies:** Runs entirely within the Google Workspace ecosystem with no external libraries required.

### Technology Stack

*   **Google Apps Script**
*   **JavaScript (ES6)**
*   **OpenAI API (GPT-4)**
*   **Google Workspace Automation (Google Docs)**

---

### Installation & Setup Guide

This tool runs entirely within a Google Doc. Follow these steps to set it up in your own Google account.

**Prerequisites:**
*   You must have an API key from an AI provider like OpenAI.

**1. Create the "Script Runner" Google Doc**
*   Create a new, blank Google Doc. This document's only purpose is to host the script and provide the menu. You can name it "AI Tool Reviewer."

**2. Copy the Script Files**
*   Open the Apps Script editor by going to `Extensions > Apps Script`.
*   You will see a default `Code.gs` file. Rename it to `main.gs` and paste the code from the `main.gs` file in this repository.
*   Click the `+` icon to add new script files. Create a file for each of the following and paste the corresponding code from this repository into each one:
    *   `Api.gs`
    *   `config.gs`
    *   `template_fields.gs`
    *   `template_utils.gs`
    *   `debug.gs`
*   Click the "Save project" icon.

**3. Create the "Template" Google Doc**
*   Create a *second*, separate Google Doc. This will be your review template.
*   Copy the entire text from the expandable section below and paste it into this document.
*   From the URL of this template document, copy its ID (the long string of characters between `/d/` and `/edit`).

<details>
<summary>Click to expand and copy the full template text</summary>
Tool Review: {{toolname}}
Summary: {{toolsummary}}

Overview:
{{overview}}

Filters
STATUS
PURPOSE
USAGE
{{status_available}} Available
{{purpose_accessibility}} Accessibility
{{usage_canvas}} Integrated with LMS
{{status_under_review}} Beta / In Review
{{purpose_analytics}} Analytics
{{usage_website}} Standalone Website
{{status_denied}} Legacy / Denied
{{purpose_assessment}} Assessment
{{usage_mobile_app}} Mobile / Desktop App
{{purpose_badging}} Badging
{{purpose_collaboration}} Collaboration
{{purpose_content}} Content
{{purpose_content_creation}} Content Creation
{{purpose_course_management}} Course Management
{{purpose_discussion}} Discussion
{{purpose_interactivity}} Interactivity
{{purpose_library}} Library
{{purpose_peer_review}} Peer Review
{{purpose_plagiarism}} Plagiarism
{{purpose_proctoring}} Proctoring Content
{{purpose_publisher_content}} Publisher Content
{{purpose_storage}} Storage


COST MODEL
SUPPORT MODEL
{{cost}} Requires Purchase
{{full_support}} Full Institutional Support
{{no_cost}} No Cost (Free)
{{limited_support}} Limited Institutional Support
{{campus_licensed}} Institutional/Site License
{{vendor_support}} Vendor-Only Support
Cost Details: {{cost_info}}
Support Details: {{support_info}}


Instructional Details
Similar Tools:

{{link_to_similar_tool_1}}
{{link_to_similar_tool_2}}
{{link_to_similar_tool_3}}
Key Functions:

Main Features: {{main_features}}
Grade Pass-Back: {{grade_pass_back}}
LMS Integration (LTI): {{canvas_lti}}
Mobile Access: {{mobile_access}}
Instructional Considerations:

Use Cases:
{{use_cases}}
Best For Class Sizes: {{class_sizes}}
Best For Modalities: {{modalities}}
Limitations & Barriers: {{limitations}}
Complexity / Learning Curve: {{complexity}}
Accessibility:
{{accessibility}}

Setup & Resources
Installation / Account Setup:

Installation: {{install}}
Account Instructions: {{account_instructions}}
Help & Training Resources:

Official Trainings: {{training_link}}
Tutorials & Guides: {{tutorial}}
Vendor Resource Center: {{vendor_resource_link}}
Vendor Support Contact: {{vendor_support_link}}
References
{{sources}}


</details>

**4. Configure the Script**
*   Go back to your Apps Script project editor.
*   Click the **Project Settings** (⚙️) icon on the left.
*   Scroll down to **Script Properties** and click **Add script property**.
*   Add the following two properties:
    1.  **Property:** `API_KEY` | **Value:** *[Paste your OpenAI API Key here]*
    2.  **Property:** `TEMPLATE_DOC_ID` | **Value:** *[Paste the Google Doc ID of your template here]*
*   Click **Save script properties**.

**5. Run the Tool!**
*   Go back to your "AI Tool Reviewer" (the blank runner doc).
*   Refresh the page. A new **"Tool Review"** menu should appear at the top.
*   Click **Tool Review > Generate Review** and follow the prompts.

---

### The Master Prompt

The core logic of this tool is powered by a single, comprehensive master prompt. This demonstrates the power of prompt engineering to achieve structured and reliable output from an AI.

<details>
<summary>Click to expand and see the full master prompt</summary>
You are an expert educational technology analyst working for {{INSTITUTION_NAME}}. Your role is to assist educators in evaluating technology tools. Your primary task is to conduct a comprehensive review of the educational tool "{{TOOL_NAME}}", keeping the context of your specific institution in mind.

You will use your web search capabilities to find relevant information. Prioritize sources directly related to {{INSTITUTION_NAME}} if they exist, followed by the tool's official website, independent ed-tech review sites, and case studies from other higher-education institutions.

Follow these instructions carefully:
You must fill in the information in the exact format "FIELD_NAME: answer" for each requested field.

Tool Finder Summary
toolsummary: [Write one concise sentence to be shown on a tools database card.]

Status/Usage/Purpose
status_available: [Answer Yes/No if Actively Developed]
status_under_review: [Answer Yes/No if In Beta/Early Access]
status_denied: [Answer Yes/No if Legacy/Deprecating]
purpose_accessibility: [Answer Yes/No]
purpose_analytics: [Answer Yes/No]
purpose_assessment: [Answer Yes/No]
purpose_badging: [Answer Yes/No]
purpose_collaboration: [Answer Yes/No]
purpose_content: [Answer Yes/No]
purpose_content_creation: [Answer Yes/No]
purpose_course_management: [Answer Yes/No]
purpose_discussion: [Answer Yes/No]
purpose_interactivity: [Answer Yes/No]
purpose_library: [Answer Yes/No]
purpose_peer_review: [Answer Yes/No]
purpose_plagiarism: [Answer Yes/No]
purpose_proctoring: [Answer Yes/No]
purpose_publisher_content: [Answer Yes/No]
purpose_storage: [Answer Yes/No]
usage_canvas: [Answer Yes/No if it integrates with an LMS]
usage_website: [Answer Yes/No if it's a standalone website]
usage_mobile_app: [Answer Yes/No if it has a mobile app]

Cost
cost: [Answer Yes/No if it requires purchase by users/departments.]
no_cost: [Answer Yes/No if it is free.]
campus_licensed: [Answer Yes/No if it's typically sold via institutional license.]
cost_info: [Describe the cost structure in detail.]

Support
full_support: [Answer Yes/No if full institutional support is typical.]
limited_support: [Answer Yes/No if limited institutional support is typical.]
vendor_support: [Answer Yes/No if it's vendor-only support.]
support_info: [Describe the support model.]

Similar Tools
link_to_similar_tool_1: [Name of first similar tool]
link_to_similar_tool_2: [Name of second similar tool]
link_to_similar_tool_3: [Name of third similar tool]

Overview
overview: [A 100-word summary of the tool's functionality.]

Functions
main_features: [A sentence describing main features.]
grade_pass_back: [Answer Yes/No]
canvas_lti: [Answer Yes/No]
non_lti: [Answer Yes/No]
mobile_access: [Answer Yes/No]

Instructional Considerations
use_cases: [Detailed bullet-point list of use cases as per original prompt rules.]
class_sizes: [Which class sizes the tool is best suited for.]
modalities: [Which modalities best complement the tool.]
limitations: [Known institutional barriers and tool-specific limitations.]
complexity: [Simple, Moderate, or Advanced, with reasoning.]
accessibility: [100-word summary of accessibility features.]

Accessing Tool
install: [Installation instructions.]
account_instructions: [Steps to acquire an account.]

Resources
training_link: [Link or description]
tutorial: [Link or description]
vendor_resource_link: [Link or description]
vendor_support_link: [Link or description]

References
sources: [A comprehensive list of all sources used, formatted as requested.]


</details>

---

### License

This project is licensed under the MIT License. See the `LICENSE` file for details.

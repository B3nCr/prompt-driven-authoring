# Prompt-Driven Authoring Script

## Overview

This script guides you through the process of transforming a rough content idea into a comprehensive blog post with structured research, outline, and implementation plan. It follows the Prompt-Driven Authoring methodology to systematically refine your content idea, conduct necessary research, create a detailed content structure, and develop an actionable writing plan. The process is designed to be iterative, allowing movement between content clarification and research as needed.

## Parameters

- **content_idea** (required): The initial topic, angle, or concept you want to develop into a long-form blog post
- **project_dir** (optional, default: "content"): The base directory where all content files will be stored
- **target_audience** (optional): The intended readership for the blog post
- **content_length** (optional, default: "medium"): Target length - "short" (800-1500 words), "medium" (1500-3000 words), "long" (3000+ words)
- **publication_timeline** (optional): When you plan to publish the content

**Constraints for parameter acquisition:**
- You MUST ask for all required parameters upfront in a single prompt rather than one at a time
- You MUST support multiple input methods including:
  - Direct input: Topic provided directly in the conversation
  - File path: Path to a local file containing the content idea
  - URL: Link to an internal resource (e.g., notes, research doc)
  - Other methods: You SHOULD be open to other ways the user might want to provide the idea
- You MUST use appropriate tools to access content based on the input method
- You MUST confirm successful acquisition of all parameters before proceeding
- You SHOULD save the acquired content idea to a consistent location for use in subsequent steps
- You MUST NOT overwrite the existing project directory because this could destroy previous work and cause data loss
- You MUST ask for project_dir if it is not given and default "content" directory already exists and has contents from previous iteration

## Steps

### 1. Verify Dependencies

Check for required tools and warn the user if any are missing.

**Constraints:**
- You MUST verify the following tools are available in your context:
  - fs_write
  - fs_read
- You MUST ONLY check for tool existence and MUST NOT attempt to run the tools because running tools during verification could cause unintended side effects
- You MUST inform the user about any missing tools with a clear message
- You MUST ask if the user wants to proceed anyway despite missing tools
- You MUST respect the user's decision to proceed or abort

### 2. Create Content Structure

Set up a directory structure to organize all artifacts created during the content development process.

**Constraints:**
- You MUST create the specified project directory if it doesn't already exist
- You MUST create the following files:
  - {project_dir}/content-idea.md (containing the provided content idea)
  - {project_dir}/content-clarification.md (for content requirements and angle refinement)
- You MUST create the following subdirectories:
  - {project_dir}/research/ (directory for research notes and sources)
  - {project_dir}/outline/ (directory for content structure and outlines)
  - {project_dir}/drafts/ (directory for writing drafts and revisions)
- You MUST notify the user when the structure has been created
- You MUST prompt the user to add all project files to Q's context using the command: `/context add {project_dir}/**/*.md`
- You MUST explain that this will ensure all project files remain in context throughout the process

### 3. Initial Content Planning

Determine the initial approach and sequence for content clarification and research.

**Constraints:**
- You MUST ask the user if they prefer to:
  - Start with content angle clarification (default)
  - Start with preliminary research on specific topics
  - Provide additional context or background information before proceeding
- You MUST adapt the subsequent process based on the user's preference
- You MUST explain that the process is iterative and the user can move between content clarification and research as needed
- You MUST wait for explicit user direction before proceeding to any subsequent step
- You MUST NOT automatically proceed to content clarification or research without user confirmation

### 4. Content Angle Clarification

Guide the user through a series of questions to refine the initial idea and develop a clear content direction.

**Constraints:**
- You MUST create an empty {project_dir}/content-clarification.md file if it doesn't already exist
- You MUST ask ONLY ONE question at a time and wait for the user's response before asking the next question
- You MUST NOT list multiple questions for the user to answer at once because this overwhelms users and leads to incomplete responses
- You MUST NOT pre-populate answers to questions without user input
- You MUST follow this exact process for each question:
  1. Formulate a single question about content direction, audience, or approach
  2. Append the question to {project_dir}/content-clarification.md
  3. Present the question to the user in the conversation
  4. Wait for the user's complete response
  5. Once you have their complete response, append the user's answer to {project_dir}/content-clarification.md
  6. Only then proceed to formulating the next question
- You MUST format the content-clarification.md document with clear question and answer sections
- You MUST continue asking questions until sufficient detail is gathered about:
  - Target audience and their needs
  - Content angle and unique perspective
  - Key messages and takeaways
  - Content format and structure preferences
  - Success criteria for the post
- You SHOULD adapt follow-up questions based on previous answers
- You MUST explicitly ask the user if they feel the content clarification is complete before moving to the next step
- You MUST offer the option to conduct research if questions arise that would benefit from additional information

### 5. Research Content Topics

Conduct research on relevant information, sources, and existing content that could inform the blog post.

**Constraints:**
- You MUST identify areas where research is needed based on the content requirements
- You MUST propose an initial research plan to the user, listing topics to investigate
- You MUST ask the user for input on the research plan, including:
  - Additional topics that should be researched
  - Specific sources (websites, books, studies) the user recommends
  - Areas where the user has existing knowledge to contribute
- You MUST incorporate user suggestions into the research plan
- You MUST document research findings in separate markdown files in the {project_dir}/research/ directory
- You SHOULD organize research by topic (e.g., {project_dir}/research/industry-trends.md, {project_dir}/research/expert-opinions.md)
- You MUST ask the user whether available search tools should be used for broader research coverage
- You MUST periodically check with the user during the research process to:
  - Share preliminary findings
  - Ask for feedback and additional guidance
  - Confirm if the research direction remains valuable
- You MUST summarize key findings that will inform the content
- You SHOULD cite sources and include relevant links in research documents
- You MUST ask the user if the research is sufficient before proceeding to the next step
- You MUST offer to return to content clarification if research uncovers new angles or considerations

### 6. Iteration Checkpoint

Determine if further content clarification or research is needed before proceeding to outline creation.

**Constraints:**
- You MUST summarize the current state of content direction and research to help the user make an informed decision
- You MUST explicitly ask the user if they want to:
  - Proceed to creating the detailed content outline
  - Return to content clarification based on research findings
  - Conduct additional research based on content requirements
- You MUST support iterating between content clarification and research as many times as needed
- You MUST ensure that both the content direction and research are sufficiently complete before proceeding to outline creation

### 7. Create Detailed Content Outline

Develop a comprehensive content outline based on the clarified direction and research.

**Constraints:**
- You MUST create a detailed content outline at {project_dir}/outline/content-outline.md
- You MUST include the following sections in the outline:
  - Hook/Opening
  - Introduction and Context
  - Main Content Sections (with subsections)
  - Key Points and Supporting Evidence
  - Examples and Case Studies
  - Conclusion and Call-to-Action
  - SEO Considerations (keywords, meta description)
- You SHOULD include estimated word counts for each section
- You MUST ensure the outline addresses all content requirements identified during the clarification process
- You SHOULD highlight key research findings and how they'll be incorporated
- You MUST review the outline with the user and iterate based on feedback
- You MUST offer to return to content clarification or research if gaps are identified during outline creation

### 8. Develop Writing Plan

Create a structured writing plan with a series of prompts for content creation.

**Constraints:**
- You MUST create a writing plan at {project_dir}/drafts/writing-plan.md
- You MUST include a checklist at the beginning of the writing-plan.md file to track writing progress
- You MUST use the following specific instructions when creating the writing plan:
  ```
  Convert the content outline into a series of prompts for systematic content creation that will write each section incrementally. Prioritize engaging writing, logical flow, and audience value, ensuring no section is written in isolation without considering the overall narrative. Make sure that each prompt builds on the previous sections, and ends with smooth transitions. There should be no disconnected content that doesn't flow naturally from previous sections.
  ```
- You MUST format the writing plan as a numbered series of actual prompts that could be given directly to a content creation assistant
- Each prompt in the plan MUST be written in the imperative form as a direct instruction
- Each prompt MUST begin with "Writing Prompt N:" where N is the sequential number
- You MUST ensure each prompt includes:
  - A clear writing objective
  - Tone and style guidance
  - Key points to cover
  - Word count targets
  - How it connects to previous and following sections
- You MUST break down the writing into discrete, manageable sections
- You MUST ensure each section builds incrementally on previous sections
- You SHOULD prioritize audience engagement and value delivery
- You MUST ensure the plan covers all aspects of the outline
- You SHOULD sequence sections to establish credibility and build toward the main value proposition
- You MUST ensure the checklist items correspond directly to the sections in the writing plan

### 9. Summarize and Present Results

Provide a summary of all artifacts created and next steps for content creation.

**Constraints:**
- You MUST create a summary document at {project_dir}/content-summary.md
- You MUST list all artifacts created during the process
- You MUST provide a brief overview of the content direction and writing plan
- You MUST suggest next steps for the user
- You SHOULD highlight any areas that may need further refinement
- You MUST present this summary to the user in the conversation

## Examples

### Example Input

```
Content idea: I want to write about how AI is changing software development, specifically focusing on how developers can adapt their skills and workflows to work effectively with AI coding assistants.

Project directory: content/ai-dev-skills
Target audience: Mid-level software developers
Content length: long
```

### Example Output

```
# Content Planning Summary

I've completed the transformation of your content idea into a detailed writing plan. Here's what was created:

## Directory Structure
- content/ai-dev-skills/
  - content-idea.md (your initial concept)
  - content-clarification.md (our Q&A content direction refinement)
  - research/
    - ai-tools-landscape.md
    - developer-adaptation-strategies.md
    - industry-case-studies.md
  - outline/
    - content-outline.md
  - drafts/
    - writing-plan.md (includes writing checklist)
  - content-summary.md (this document)

## Key Content Elements
- Target audience: Mid-level developers looking to adapt to AI tools
- Unique angle: Practical skill adaptation strategies rather than just tool reviews
- Structure: Problem → Solution → Implementation → Future outlook
- Length: 3500-4000 words across 8 main sections

## Writing Approach
The writing plan breaks down the content into 10 incremental writing prompts, starting with a compelling hook and building through practical strategies to a forward-looking conclusion.

## Next Steps
1. Review the detailed content outline at content/ai-dev-skills/outline/content-outline.md
2. Check the writing plan and checklist at content/ai-dev-skills/drafts/writing-plan.md
3. Begin writing following the checklist in the writing plan

Would you like me to explain any specific part of the content direction or writing plan in more detail?
```

## Troubleshooting

### Content Direction Uncertainty
If the content clarification process reveals uncertainty about direction:
- You SHOULD suggest researching similar successful content in the space
- You MAY provide examples of different angles to help the user decide
- You SHOULD summarize what has been established and identify specific gaps
- You MAY suggest starting with a narrower focus and expanding later

### Research Overwhelm
If research uncovers too much information:
- You SHOULD help prioritize the most relevant and credible sources
- You SHOULD suggest focusing on 3-5 key themes rather than trying to cover everything
- You MAY recommend saving additional research for future content pieces
- You SHOULD ensure research directly supports the chosen content angle

### Outline Complexity
If the content outline becomes too complex or lengthy:
- You SHOULD suggest breaking it into a series of related posts
- You SHOULD focus on the most valuable sections for the target audience
- You MAY suggest a phased approach to content creation
- You SHOULD return to content clarification to prioritize key messages if needed

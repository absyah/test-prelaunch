# 🤖 AI Tasks Suggestion 

## 🔥 Problem Statement

You are asked to develop a feature to generate tasks list from single key goal, for example:
"Steps to complete Stripe Implementation in Web Application".

You can review and edit those generated tasks to make adjustments.

## 🚒 Solution

- Integrates OpenAI to generate task lists using the GPT-4 model or higher.
- Processes requests to OpenAI asynchronously via a background job.
- Delivers real-time results to the frontend using Rails ActionCable.

### 🗣️ AI Prompts

**System Prompt** 
```
You are a technical project leader in software development.
Given a goal, you break it down into a structured list of detailed tasks.
Each task should have a clear title and a concise but informative description.
Your response must be formatted as an array of task objects, where each object contains a 'title' and 'description' attribute.
```

**User Prompt**

```
Generate a list of tasks with a name and description for this goal: <goal>
```

## 🧯Process Flow

This program leverages OpenAI to generate tasks based on a given goal. The generated tasks are temporarily stored in a cache with a unique key and broadcasted to the user interface for review before being saved to the database.

![Untitled Diagram drawio](https://github.com/user-attachments/assets/e46f32fa-d95b-4cd5-b00d-af9e08e21d86)

## 📺Video Demo

https://www.loom.com/share/a9e3b866a5214f63b1ef7db9f5c244a0?sid=eb6f66ee-79dd-470c-94e3-1a174b17e262


## 📂 Updated Application Structure

- *services/* -- Manages external / 3rd party interaction.
   - `ai_task_suggestion_service.rb` -- Sends a request with system and user prompt to generate tasks list, handling OpenAI response parsing as well.
- *jobs/* -- Manages background processing.
   - `generate_ai_tasks_job.rb` -- Responsibles to handle heavy load processes, in this case OpenAI request.
- *channels/* -- Manages real-time update.
   - `ai_tasks_channel.rb` -- Handles subscription of OpenAI response for real-time update to the user interface.
- *spec/* -- Provides unit tests of the system.
- *test/* -- Provides fixtures for data mockup and end-to-end testing with Selenium

## 🚀 Getting Started

### Start
- create `.env` file with following content:
  -  `OPENAI_API_KEY=<your_openai_api_key>`
- `docker compose up`

### Run tests

#### e2e testing with Selenium
- `docker compose exec rails rails test`

#### Unit testing with RSpec
- `docker compose exec rails rspec`



# Calendar-Scheduler-Agent-AMD-MI300-GPU
AI Scheduling Assistant on AMD Instinct MI300

# AI-Powered Scheduling Assistant

[![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![LangChain](https://img.shields.io/badge/LangChain-0.1+-green.svg)](https://langchain.com/)
[![LangGraph](https://img.shields.io/badge/LangGraph-0.1+-orange.svg)](https://langchain.com/langgraph)
[![Google Calendar API](https://img.shields.io/badge/Google%20Calendar%20API-v3-red.svg)](https://developers.google.com/calendar)

An intelligent AI-powered meeting scheduling assistant that automates meeting coordination using Agentic AI, Google Calendar integration, and priority-based conflict resolution.

## 🚀 Features

- **🤖 Agentic AI Architecture**: Uses LangGraph with React Agent for complex reasoning
- **📅 Real-time Calendar Integration**: Direct Google Calendar API access with OAuth2
- **⚡ Priority-Based Scheduling**: Intelligent meeting classification (P0/P1/P2)
- **🔄 Conflict Resolution**: Automatic conflict detection and smart rescheduling
- **🌍 Timezone Support**: Built-in IST timezone handling
- **📝 Natural Language Processing**: Parse meeting requests in plain English
- **⚡ Sub-second Performance**: Optimized for real-time scheduling

## 🏗️ Architecture

### Core Components

1. **LangGraph Agent Framework**
   - React Agent with Tool Calling
   - Qwen2.5-14B-Instruct LLM
   - Structured Output Parsing with Pydantic

2. **Google Calendar Integration**
   - OAuth2 Authentication
   - Real-time Calendar Scanning
   - Multi-user Event Retrieval

3. **Intelligent Conflict Resolution**
   - Priority-based Meeting Classification
   - Automatic Conflict Detection
   - Smart Rescheduling Logic

## 📋 Prerequisites

- Python 3.8+
- Google Calendar API credentials
- vLLM inference server running locally
- Required Python packages (see Installation)

## 🛠️ Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd AI-Scheduling-Assistant
   ```

2. **Install dependencies**
   ```bash
   pip install langchain
   pip install langgraph
   pip install langchain-openai
   pip install langchain-core
   pip install google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client
   pip install pydantic
   ```

3. **Set up Google Calendar API**
   - Create a Google Cloud Project
   - Enable Google Calendar API
   - Create OAuth2 credentials
   - Download credentials and place in `Keys/` directory

4. **Configure vLLM server**
   ```bash
   # Start vLLM server with Qwen model
   vllm serve Qwen/Qwen2.5-14B-Instruct --host 0.0.0.0 --port 3000
   ```

5. **Set up authentication tokens**
   - Place user authentication tokens in `Keys/` directory
   - Format: `{username}.token`

## 🚀 Quick Start

1. **Start the vLLM server**
   ```bash
   vllm serve Qwen/Qwen2.5-14B-Instruct --host 0.0.0.0 --port 3000
   ```

2. **Run the scheduling assistant**
   ```bash
   python agent.py
   ```

3. **Example usage**
   ```python
   # The system will process meeting requests like:
   email_content = "Hi, I need to schedule a client demo meeting on Monday 2025-07-21 at 9:00 AM IST."
   ```

## 📊 Priority System

### Meeting Classification

| Priority | Type | Keywords | Rules |
|----------|------|----------|-------|
| **P0** | OUTAGE (CRITICAL) | emergency, urgent, ASAP, outage, crash, failure, breach, crisis, critical | Override ALL conflicts, schedule immediately |
| **P1** | CLIENT/CUSTOMER (HIGH) | client, customer, demo, feedback, requirements, quarterly review | Override internal meetings only, business hours |
| **P2** | INTERNAL (STANDARD) | team, 1-on-1, sprint, project, catchup, planning, retrospective, brainstorming | Can be rescheduled, business hours only |

### Priority Resolution Matrix

| Request Type | vs Outage | vs Client | vs Internal | vs Leave/External |
|--------------|-----------|-----------|-------------|-------------------|
| **Outage**   | Override  | Override  | Override    | Override          |
| **Client**   | Defer     | Defer     | Override    | Defer             |
| **Internal** | Defer     | Defer     | Defer       | Defer             |

## 🔧 Configuration

### Environment Variables

```bash
# vLLM Server Configuration
VLLM_BASE_URL=http://localhost:3000/v1
VLLM_API_KEY=your_api_key

# Google Calendar Configuration
GOOGLE_CALENDAR_CREDENTIALS_PATH=Keys/
```

### Valid Users

Currently supported users:
- `userone.amd@gmail.com`
- `usertwo.amd@gmail.com`
- `userthree.amd@gmail.com`

## 📁 Project Structure

```
AI-Scheduling-Assistant/
├── agent.py                          # Main scheduling agent
├── Documentation/                    # Project documentation
│   ├── README.md                     # This file
│   └── project_description.md        # Detailed project description
├── Keys/                             # Authentication tokens
├── JSON_Samples/                     # Input/Output JSON examples
├── Test_Cases/                       # Test scenarios
└── real_test_cases/                  # Real-world test cases
```

## 🧪 Testing

Run test cases to verify functionality:

```bash
# Test specific scenarios
python -c "from agent import *; # Run test cases"
```

## 📈 Performance

- **Execution Time**: Sub-second response times
- **Accuracy**: 100% priority rule compliance
- **Scalability**: Supports multiple users simultaneously
- **Reliability**: OAuth2 authentication with error handling

## 🔍 API Reference

### Main Functions

#### `retrive_calendar_events(users, start, end)`
Fetches calendar events for multiple users within a time range.

**Parameters:**
- `users`: List of user email addresses
- `start`: ISO-8601 start time
- `end`: ISO-8601 end time

**Returns:** List of user events with detailed information

#### `Structured_Output_llm`
Pydantic model for structured scheduling output.

**Fields:**
- `start_time`: Proposed start time
- `end_time`: Proposed end time
- `duration`: Meeting duration in minutes
- `optimal_start_time`: Conflict-free start time
- `optimal_end_time`: Conflict-free end time

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [LangChain](https://langchain.com/) for the agent framework
- [LangGraph](https://langchain.com/langgraph) for complex reasoning capabilities
- [Google Calendar API](https://developers.google.com/calendar) for calendar integration
- [Qwen](https://huggingface.co/Qwen) for the language model

## 📞 Support

For support and questions:
- Create an issue in the repository
- Contact the development team
- Check the documentation in the `Documentation/` folder

---

**Built with ❤️ using Agentic AI for intelligent meeting scheduling** 

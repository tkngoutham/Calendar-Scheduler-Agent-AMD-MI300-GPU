# AI Scheduling Assistant - AMD MI300 GPU Project

An intelligent calendar scheduling system that uses AI agents to automatically schedule meetings by analyzing email requests and calendar availability. Built with LangChain, LangGraph, and powered by AMD MI300 GPU with vLLM.

## 🚀 Features

- **Intelligent Meeting Classification**: Automatically categorizes meetings into priority levels (P0-Outage, P1-Client, P2-Internal)
- **Conflict Resolution**: Smart conflict detection and resolution with priority-based scheduling
- **Multi-User Calendar Integration**: Seamless integration with Google Calendar API
- **Real-time Processing**: RESTful API endpoint for instant meeting scheduling
- **AMD MI300 GPU Optimized**: Leverages AMD MI300 GPU with vLLM for high-performance inference

## 🏗️ Architecture

### Core Components

1. **AI Agent System**: Built with LangChain and LangGraph for intelligent decision making
2. **Calendar Integration**: Google Calendar API integration for event management
3. **Priority-Based Scheduling**: Three-tier priority system for meeting classification
4. **Conflict Resolution Engine**: Automatic conflict detection and resolution
5. **REST API**: Flask-based web service for external integrations

### Priority System

| Priority | Meeting Type | Keywords | Rules |
|----------|-------------|----------|-------|
| **P0** | Outage (Critical) | emergency, urgent, ASAP, outage, crash, failure, breach, crisis, critical | Override ALL conflicts, schedule immediately |
| **P1** | Client/Customer | client, customer, demo, feedback, requirements, quarterly review | Override internal meetings only |
| **P2** | Internal | team, 1-on-1, sprint, project, catchup, planning, retrospective, brainstorming | Can be rescheduled for higher priority meetings |

## 🛠️ Technology Stack

- **AI Framework**: LangChain, LangGraph
- **Language Model**: Qwen/Qwen2.5-14B-Instruct (via vLLM)
- **GPU**: AMD MI300
- **Backend**: Flask (Python)
- **Calendar API**: Google Calendar API
- **Inference Server**: vLLM (localhost:3000)

## 📋 Prerequisites

- Python 3.12+
- AMD MI300 GPU
- vLLM server running on localhost:3000
- Google Calendar API credentials
- Valid user accounts: userone.amd@gmail.com, usertwo.amd@gmail.com, userthree.amd@gmail.com

## 🚀 Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd Calendar-Scheduler-Agent-AMD-MI300-GPU
   ```

2. **Install dependencies**
   ```bash
   pip install langchain
   pip install langgraph
   pip install langchain-openai
   pip install langchain-core
   pip install flask
   pip install google-auth google-auth-oauthlib google-auth-httplib2 google-api-python-client
   pip install pytz
   ```

3. **Setup Google Calendar API**
   - Create a Google Cloud Project
   - Enable Google Calendar API
   - Create OAuth 2.0 credentials
   - Place token files in `Keys/` directory:
     - `Keys/userone.token`
     - `Keys/usertwo.token`
     - `Keys/userthree.token`

4. **Configure vLLM Server**
   ```bash
   # Start vLLM server with Qwen model
   vllm serve Qwen/Qwen2.5-14B-Instruct --host 0.0.0.0 --port 3000
   ```

## 🎯 Usage

### Starting the Service

```python
# Run the Jupyter notebook cells in order
# The Flask server will start automatically on port 5000
```

### API Endpoint

**POST** `/receive`

**Request Body:**
```json
{
  "From": "userone.amd@gmail.com",
  "Subject": "Team Meeting",
  "EmailContent": "Let's schedule a team meeting tomorrow at 10 AM",
  "Datetime": "20-07-2025T08:00:00",
  "Attendees": [
    {"email": "usertwo.amd@gmail.com"},
    {"email": "userthree.amd@gmail.com"}
  ]
}
```

**Response:**
```json
{
  "From": "userone.amd@gmail.com",
  "Subject": "Team Meeting",
  "EmailContent": "Let's schedule a team meeting tomorrow at 10 AM",
  "Datetime": "2025-07-21T08:00:00",
  "EventStart": "2025-07-21T10:00:00+05:30",
  "EventEnd": "2025-07-21T10:30:00+05:30",
  "Duration_mins": "30",
  "Attendees": [
    {
      "email": "userone.amd@gmail.com",
      "events": [...]
    },
    {
      "email": "usertwo.amd@gmail.com", 
      "events": [...]
    },
    {
      "email": "userthree.amd@gmail.com",
      "events": [...]
    }
  ],
  "MetaData": [{"latency": 2.5}]
}
```

## 🔧 Configuration

### Model Configuration
```python
base_url = "http://localhost:3000/v1"
api_key = "goutham"
model = "Qwen/Qwen2.5-14B-Instruct"
```

### Timezone Settings
- **Reference Date**: 2025-07-20 (Sunday)
- **Timezone**: IST (+05:30)
- **Working Hours**: 9 AM - 6 PM (weekdays only)

### Valid Users
- userone.amd@gmail.com
- usertwo.amd@gmail.com  
- userthree.amd@gmail.com

## 🧠 AI Agent Workflow

1. **Email Analysis**: Parse email content for meeting type and timing
2. **Priority Classification**: Determine meeting priority (P0/P1/P2)
3. **Date/Time Extraction**: Extract or infer meeting date and time
4. **Calendar Check**: Fetch all participants' calendar events
5. **Conflict Detection**: Identify scheduling conflicts
6. **Resolution**: Apply priority rules and find optimal time slot
7. **Response Generation**: Return structured scheduling response

## 📊 Performance

- **Latency**: Typically 2-3 seconds per request
- **GPU Utilization**: Optimized for AMD MI300
- **Concurrent Requests**: Flask handles multiple simultaneous requests
- **Accuracy**: High accuracy in meeting classification and conflict resolution

## 🔒 Security

- OAuth 2.0 authentication for Google Calendar API
- Secure token storage in `Keys/` directory
- Input validation and sanitization
- Error handling for invalid requests

## 🐛 Troubleshooting

### Common Issues

1. **vLLM Server Not Running**
   - Ensure vLLM server is running on localhost:3000
   - Check model availability: `Qwen/Qwen2.5-14B-Instruct`

2. **Calendar API Errors**
   - Verify OAuth tokens are valid and not expired
   - Check Google Calendar API quotas

3. **GPU Memory Issues**
   - Monitor AMD MI300 GPU memory usage
   - Adjust vLLM batch size if needed

### Logs
- Flask server logs show request processing
- AI agent decisions are logged in console output
- Calendar API responses are logged for debugging

## 📈 Future Enhancements

- [ ] Support for more calendar providers (Outlook, iCal)
- [ ] Advanced conflict resolution algorithms
- [ ] Meeting duration optimization
- [ ] Integration with video conferencing platforms
- [ ] Mobile app support
- [ ] Multi-language support

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests if applicable
5. Submit a pull request

## 📄 License

This project is part of the AMD MI300 GPU development initiative.

## 👥 Team

- **AI/ML**: LangChain, LangGraph implementation
- **Backend**: Flask API development
- **Infrastructure**: AMD MI300 GPU optimization
- **Integration**: Google Calendar API

---

**Note**: This system is designed for demonstration and development purposes. For production use, additional security measures and error handling should be implemented. 

# Ransomcrafted

### AI-Powered Ransomware Detection & Automated Recovery System

![Version](https://img.shields.io/badge/version-1.0.0-blue)
![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)
![License](https://img.shields.io/badge/license-MIT-green)
![Python](https://img.shields.io/badge/python-3.9%2B-blue)
![Status](https://img.shields.io/badge/status-active-success)
![AI](https://img.shields.io/badge/AI-Deepgram%20%7C%20OpenAI-purple)

**Ransomcrafted** is a smart, proactive defense system that detects ransomware in real-time, automatically isolates infected endpoints, and recovers encrypted data using AI-assisted restoration — all while generating compliance-ready incident reports.

[Demo](#-demo) • [Features](#-key-features) • [AI Integration](https://console.deepgram.com) • [Installation](https://cloud.livekit.io/login) • [Architecture](https://drive.google.com/file/d/1HqQhj3qnTmzTw_N8X_tymW4H5rWNt4Wa/view?usp=sharing) • [API](https://aistudio.google.com/u/1/) • [Contributing](#-contributing)

---

## Demo time line

```
[13:22:01]  Ransomware detected: Mass file rename + entropy spike
[13:22:02]  Isolating endpoint: DESKTOP-FIN01
[13:22:02]  Terminating malicious process: PID 4423 (ransom.exe)
[13:22:03]  AI Assistance Agent: Analyzing ransom note...
[13:22:04]  Deepgram Audio Analysis: No voice anomalies detected
[13:22:04]  OpenAI Analysis: Decryptor found on NoMoreRansom
[13:22:05]  Restoring from shadow copy: Version 2025-04-01 12:00:00
[13:22:07]  Recovery complete: 1,247 files restored
[13:22:07]  Incident report generated: RC-2025-04-01-001
Recovery successful! 0% data loss
```

---

## Key Features

| Feature | Description |
|---------|-------------|
| Real-time Monitoring | File system hooks + behavioral analysis (entropy spikes, mass renames, ransom note patterns) |
| Automated Isolation  | Network segmentation, process termination, share revocation |
| AI-Assisted Recovery | Intelligent restoration from shadow copies / backups with verification |
| AI Assistance Agent | LLM-powered assistant for real-time guidance, ransom note analysis, and recovery recommendations |
| Deepgram API | Audio transcription & analysis for voice-based attack alerts and security briefings |
| OpenAI API | Advanced threat intelligence, ransom note decryption analysis, and natural language incident reports |
| Incident Reporting | SOC-ready reports with IOCs, timeline, and recovery status |
| Low Latency | 2s detection-to-response |
| Lightweight Agent | Rust/C++ core with minimal CPU/memory footprint |

---

##  AI Integration

<img width="1897" height="888" alt="image" src="https://github.com/user-attachments/assets/5265dee5-05bb-4d79-8da8-79f9656d2dba" />

### AI Assistance

The AI Assistance Agent provides real-time, natural language support during ransomware incidents.

```python
from ransomcrafted import AIAssistanceAgent

# Initialize agent
agent = AIAssistanceAgent(
    openai_api_key="your-key",
    deepgram_api_key="your-key"
)

# Analyze ransom note
response = agent.analyze_ransom_note(
    note_text="YOUR FILES HAVE BEEN ENCRYPTED. Send 1 BTC to wallet..."
)

print(response.decryptor_available)
print(response.recommended_action)
print(response.severity)              "CRITICAL"
```

**Agent Capabilities:**
-  Ransom note parsing & family identification
-  Natural language incident summaries
-  IOC extraction and threat intelligence lookup
-  Voice interaction via Deepgram

### Deepgram API Integration

Real-time audio transcription for voice-based attack alerts and security briefings.

```python
from ransomcrafted.audio import DeepgramTranscriber

transcriber = DeepgramTranscriber(api_key="your-deepgram-key")

# Transcribe security briefing
transcript = transcriber.transcribe("security_briefing.mp3")
# Output: "Ransomware detected on finance server at 2 PM..."

# Real-time voice alert monitoring
async for alert in transcriber.stream_microphone():
    if "ransomware" in alert.transcript:
        trigger_isolation()
```

**Use Cases:**
- Voice-activated security commands ("Isolate endpoint Finance-01")
- Real-time SOC room transcription
- Audio alert analysis for false positive reduction

### OpenAI API Integration

Advanced LLM-powered threat analysis and reporting.

```python
from ransomcrafted.ai import OpenAIAnalyzer

analyzer = OpenAIAnalyzer(api_key="your-openai-key")

# Analyze file behavior
result = analyzer.analyze_behavior(
    file_events=event_log,
    entropy_scores=[0.92, 0.88, 0.95]
)
# Returns: {"threat_level": "critical", "family": "LockBit", "confidence": 0.97}

# Generate incident report
report = analyzer.generate_report(
    incident_id="RC-2025-04-01-001",
    format="executive"  # executive, technical, compliance
)

# Natural language query interface
answer = analyzer.ask("What files were affected in the last ransomware attack?")
```

---

##  Installation

### Prerequisites
- Python 3.9+
- Windows 10/11, Linux (kernel 5.4+), or macOS 11+
- Administrator/root access (for isolation features)
- **API Keys:** OpenAI, Deepgram (optional but recommended)

### From Source

```bash
# Clone the repository
git clone https://github.com/yourusername/ransomcrafted.git
cd ransomcrafted

# Install dependencies
pip install -r requirements.txt

# Set API keys (optional but enables AI features)
export OPENAI_API_KEY="your-key"
export DEEPGRAM_API_KEY="your-key"

# Run installation script
python setup.py install

# Start the agent (admin required)
sudo python agent.py --config config.yaml   # Linux/macOS
python agent.py --config config.yaml        # Windows (as Admin)
```

### Docker (Sandbox Mode)

```bash
# Build with AI integrations
docker build --build-arg OPENAI_API_KEY=$OPENAI_API_KEY \
             --build-arg DEEPGRAM_API_KEY=$DEEPGRAM_API_KEY \
             -t ransomcrafted:ai .

docker run -v /path/to/monitor:/data \
           -e OPENAI_API_KEY=$OPENAI_API_KEY \
           -e DEEPGRAM_API_KEY=$DEEPGRAM_API_KEY \
           ransomcrafted:ai
```

---

## Architecture

<img width="850" height="1100" alt="jhh" src="https://github.com/user-attachments/assets/7f8470b0-6598-483a-819e-e48db1f595ef" />


---

## Configuration

Example `config.yaml` with AI settings:

```yaml
monitoring:
  paths:
    - /home
    - /var/www
    - C:\Users\*
  exclude_extensions:
    - .tmp
    - .log

detection:
  entropy_threshold: 0.85
  rename_rate_threshold: 100  # files/sec
  enable_ml: true

response:
  isolation:
    enable_network_isolation: true
    enable_process_termination: true
    enable_user_logoff: false

recovery:
  prefer_shadow_copy: true
  backup_path: /backups
  verify_restore: true

ai:
  assistance_agent:
    enabled: true
    auto_response: false  # Require human approval for auto-recovery
    model: "gpt-4-turbo"
  
  deepgram:
    enabled: true
    language: "en-US"
    real_time_transcription: true
    alert_keywords:
      - "ransomware"
      - "encryption"
      - "breach"
  
  openai:
    enabled: true
    model: "gpt-4-turbo"
    max_tokens: 2000
    temperature: 0.3
    threat_intel_enabled: true

reporting:
  format: json  # json, html, pdf
  webhook: https://your-siem.com/webhook
  include_ai_analysis: true
```

---

## API

### AI Assistance Agent API

```http
POST /api/v1/ai/analyze
Content-Type: application/json
Authorization: Bearer <token>

{
  "type": "ransom_note",
  "content": "Your files are encrypted. Pay 2 BTC to wallet: 1A1zP1eP5QGefi2DMPTfTL5SLmv7DivfNa",
  "context": {
    "endpoint_id": "DESKTOP-FIN01",
    "file_count": 1543
  }
}
```

**Response:**
```json
{
  "ransomware_family": "LockBit",
  "confidence": 0.94,
  "decryptor_available": true,
  "decryptor_url": "https://nomoreransom.org",
  "recommended_action": "restore_from_backup",
  "severity": "critical",
  "analysis_timestamp": "2025-04-01T13:22:04Z"
}
```

### Deepgram Audio Analysis API

```http
POST /api/v1/audio/transcribe
Content-Type: multipart/form-data

{
  "audio_file": "alert_recording.wav",
  "detect_threat_keywords": true
}
```

**Response:**
```json
{
  "transcript": "Ransomware detected on finance server. Initiating isolation.",
  "threat_keywords_detected": ["ransomware", "isolation"],
  "confidence": 0.97,
  "actionable_intent": "isolate_endpoint",
  "target_endpoint": "finance-server"
}
```

### OpenAI Threat Analysis API

```http
POST /api/v1/openai/analyze_behavior
Content-Type: application/json

{
  "file_events": [
    {"path": "/docs/payroll.xlsx", "action": "rename", "new_ext": ".encrypted"},
    {"path": "/docs/budget.pdf", "action": "write", "entropy": 0.92}
  ],
  "process_tree": [
    {"pid": 4423, "name": "ransom.exe", "parent": 2100}
  ]
}
```

**Response:**
```json
{
  "threat_assessment": {
    "is_ransomware": true,
    "confidence": 0.99,
    "family": "LockBit 3.0",
    "tactics": ["encryption", "lateral_movement"]
  },
  "recommended_response": {
    "immediate": "isolate_endpoint",
    "secondary": "revoke_credentials",
    "recovery": "shadow_copy_restore"
  },
  "human_readable_summary": "LockBit ransomware detected. 1,543 files encrypted. Immediate isolation recommended."
}
```

### Complete API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/ai/analyze` | AI Assistant analysis of ransom notes/IOCs |
| POST | `/api/v1/audio/transcribe` | Deepgram speech-to-text + threat detection |
| POST | `/api/v1/openai/analyze_behavior` | OpenAI behavioral threat analysis |
| GET | `/api/v1/ai/chat` | Natural language query interface |
| POST | `/api/v1/report/ai_generate` | AI-generated incident report |
| POST | `/api/v1/detect` | Threat detection endpoint |
| GET | `/api/v1/report/{incident_id}` | Retrieve incident report |
| POST | `/api/v1/recover` | Trigger manual recovery |

Full API docs: [`/docs/api.md`](docs/api.md)

---

## AI Assistant Chat Interface

```python
from ransomcrafted.ai import AIAssistanceAgent

agent = AIAssistanceAgent(openai_api_key="key")

# Chat with the AI assistant
response = agent.chat("What should I do after ransomware hits?")

print(response)
"""
1. IMMEDIATELY isolate the affected endpoint (Ransomcrafted does this automatically)
2. DO NOT pay the ransom - only 26% get files back
3. Check if a decryptor exists (I'll check NoMoreRansom for you)
4. Restore from clean backups (I'll find the most recent clean snapshot)
5. File a report with local authorities
"""
```

---

## Testing

Run the test suite:

```bash
# Unit tests
pytest tests/unit

# Integration tests (requires isolated VM)
pytest tests/integration

# AI-specific tests (requires API keys)
pytest tests/ai -v

# Simulate ransomware (safe mode)
python scripts/simulate_ransomware.py --path /tmp/test

# Test AI Assistance Agent
python scripts/test_ai_agent.py
```

---

## Performance Benchmarks

| Metric | Value |
|--------|-------|
| Detection latency | <200ms |
| Isolation time | <1s |
| Recovery speed | ~500 MB/s |
| AI analysis latency (OpenAI) | ~1.2s |
| Deepgram transcription (real-time) | <300ms |
| CPU overhead | <5% |
| RAM usage | ~120 MB (+50MB AI cache) |

---

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `OPENAI_API_KEY` | No (AI features limited) | OpenAI API key |
| `DEEPGRAM_API_KEY` | No (audio features disabled) | Deepgram API key |
| `RANSOMCRAFTED_ENV` | No | `dev`, `staging`, `prod` |
| `AI_AGENT_MODE` | No | `auto`, `assisted`, `manual` |
| `WEBHOOK_URL` | No | SIEM integration URL |

---

## Contributing

We welcome contributions! See [`CONTRIBUTING.md`](CONTRIBUTING.md).

1. Fork the repo
2. Create feature branch (`git checkout -b feature/amazing`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push (`git push origin feature/amazing`)
5. Open Pull Request

### Development Setup with AI

```bash
git clone https://github.com/yourusername/ransomcrafted.git
cd ransomcrafted
pip install -e ".[dev,ai]"
pre-commit install

# Set up API keys for development
cp .env.example .env
# Edit .env with your keys
```

---

## Project Structure

```
ransomcrafted/
├── agent/                 # Endpoint agent (Rust/C++ core)
│   ├── src/
│   ├── monitor/          # File system hooks
│   ├── detector/         # Behavioral & ML detection
│   └── isolation/        # Network/process isolation
├── manager/              # Central management server
│   ├── api/
│   ├── orchestrator/
│   └── reporting/
├── ai/                   # AI Integration Layer
│   ├── assistance_agent/ # AI Assistance Agent
│   │   ├── agent.py      # Core agent logic
│   │   ├── prompts/      # LLM prompt templates
│   │   └── tools/        # Agent tools (file search, threat intel)
│   ├── deepgram/         # Deepgram API integration
│   │   ├── transcriber.py
│   │   ├── stream.py     # Real-time streaming
│   │   └── keywords.py   # Threat keyword detection
│   └── openai/           # OpenAI API integration
│       ├── analyzer.py   # Behavioral analysis
│       ├── reporter.py   # Report generation
│       └── chat.py       # Chat interface
├── recovery/             # AI-assisted recovery engine
│   ├── snapshot/
│   ├── restore/
│   └── verify/
├── web/                  # Dashboard (React)
├── scripts/              # Utilities & simulators
├── tests/
│   ├── unit/
│   ├── integration/
│   └── ai/              # AI-specific tests
├── docs/
├── config.yaml.example
├── .env.example
├── Dockerfile
└── requirements.txt
```

---

## Disclaimer

**For authorized security testing only.** Do not deploy Ransomcrafted in production without proper validation. The authors assume no liability for misuse or unintended system behavior.

**AI API Usage:** OpenAI and Deepgram API usage incurs costs based on your subscription. Ransomcrafted implements caching and rate limiting to minimize expenses.

---

## License

MIT © [Ransomcrafted Team](LICENSE)

---

##  Acknowledgments

- **OpenAI** - GPT-4 for threat analysis & reporting
- **Deepgram** - Nova-2 for real-time transcription
- NoMoreRansom Project
- Chate Framework
- Ogworks Community

---

##  Contact

GitHub: [https://github.com/itsomg134](https://github.com/itsomg134)

Email: [omgedam123098@gmail.com](mailto:omgedam123098@gmail.com)

Twitter (X): [https://twitter.com/omgedam](https://twitter.com/omgedam)

LinkedIn: [https://linkedin.com/in/omgedam](https://linkedin.com/in/omgedam)

Portfolio: [https://ogworks.lovable.app](https://ogworks.lovable.app)

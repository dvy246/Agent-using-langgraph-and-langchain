# Fixed README with Enhanced Flow Description

```markdown
# 🛡️ Heimdall – Multi-Agent Financial Intelligence

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Heimdall is a multi-agent orchestration system designed to reason about financial data from multiple perspectives. It combines specialist supervisors, custom-built tools, and retrieval pipelines to create structured, validated insights — with a human-in-the-loop when needed.

Think of it as an AI research team in a box: one orchestrator delegates missions, supervisors lead domain experts, and writers synthesize everything into a clear, validated report.

## 🌍 Why Heimdall?

In finance and research, information doesn't live in one place. It's scattered across filings, news, markets, and models. A single agent often falls short in reasoning through this complexity.

Heimdall solves this by:
- Breaking work into missions with a planner
- Delegating to specialized supervisors (valuation, risk, ESG, etc.)
- Synthesizing results through joint report writers
- Validating outputs with both AI and humans before publishing

This makes it adaptable to domains where accuracy, transparency, and reliability matter.

## 🧠 System Flow

```
[ Orchestrator ]
        |
        v
[ Mission Planner Agent ]
        |
        v
[ Main Supervisor ]
        |
        v
+-----------------------------------+
| 5 Domain Supervisors              |
| - ESG Analyst Supervisor          |
| - Valuation Supervisor            |
| - Risk Research Supervisor        |
| - Competitive Analysis Supervisor |
| - Industry Analysis Supervisor    |
+-----------------------------------+
        |
        v
[ Joint Report Writer ]
        |
        v
[ Validation Supervisor ]
        |
        v
[ Human-in-the-Loop (optional) ]
       | \
       |  \
       |   → If issues → back to Joint Report Writer
        v
[ Final Report Writer ]
```

## 🔄 How the Flow Works

### 1. Orchestrator
The entry point that initiates the analysis process. It receives the initial query and coordinates the entire workflow, ensuring proper data flow between components.

### 2. Mission Planner Agent
Breaks down complex financial queries into specialized missions for each domain supervisor. It defines:
- Specific objectives for each domain
- Required data sources
- Analysis parameters
- Success criteria

### 3. Main Supervisor
Coordinates parallel execution of domain-specific analyses and manages communication between specialized agents. It:
- Distributes missions to appropriate domain supervisors
- Monitors progress and handles timeouts
- Aggregates preliminary results

### 4. Domain Supervisors
Five specialized agents conducting focused analysis:

- **ESG Analyst Supervisor**: Evaluates Environmental, Social, and Governance factors, sustainability practices, and ethical considerations
- **Valuation Supervisor**: Performs financial modeling, discounted cash flow analysis, and company valuation assessments
- **Risk Research Supervisor**: Identifies and assesses market, credit, operational, and geopolitical risks
- **Competitive Analysis Supervisor**: Analyzes market position, competitor benchmarking, and competitive advantages
- **Industry Analysis Supervisor**: Examines sector trends, regulatory impacts, and macroeconomic factors

### 5. Joint Report Writer
Synthesizes findings from all domain supervisors into a cohesive draft report. It ensures:
- Consistent tone and structure throughout
- Logical flow between sections
- Elimination of contradictory information
- Proper citation of data sources

### 6. Validation Supervisor
Performs quality assurance through automated evaluation. It uses a specialized evaluation chain that:

```python
def evaluate_report(report: str):
    # Professional editor prompt to assess report quality
    eval_chain = prompt | model | StrOutputParser
    # Revision chain for failed reports
    revise_chain = revise_prompt | model | StrOutputParser
    # Routing logic to determine pass/fail
    router = RunnableLambda(lambda x: route(x))
    
    conditional = RunnableBranch(
        (lambda x: router.invoke(eval_chain.invoke(report)) == 'revise', 
         revise_chain, 
         RunnablePassthrough())
    )
    return conditional.invoke({'report': report})

def route(output: str):
    # Decision logic for report quality
    small = output.lower().strip()
    if any(i in small for i in ['fail', 'needs improvement', 'needs revision']):
        return "revise"
    else:
        return 'pass'
```

The validation assesses:
- **Clarity**: Language clarity and understandability
- **Objectivity**: Neutral and unbiased tone
- **Completeness**: Thoroughness of analysis and coverage of key areas
- **Logical Consistency**: Whether recommendations follow logically from evidence

### 7. Human-in-the-Loop (Optional)
Provides expert review where:
- Financial experts can provide feedback
- Regulatory compliance can be verified
- Complex judgments can be made
- Reports can be approved or sent for revision

### 8. Final Report Writer
Incorporates all feedback and produces the polished final output with:
- Professional formatting
- Executive summary
- Key findings highlighted
- Data visualizations (if applicable)
- Actionable recommendations

The system supports iterative refinement, where reports that don't meet validation criteria are automatically sent back to the Joint Report Writer for improvement.

## 📂 Project Structure

```
.
├── agents/              # Agent definitions
├── tools/               # Financial, market, valuation, and RAG tools
├── config/              # Configurations (logging, settings)
├── utils/               # Utility helpers
├── data/                # Local dbs, caches (ignored in git)
├── logs/                # Runtime logs (ignored in git)
├── notebooks/           # Prototyping + experiments
├── tests/               # Unit tests
│
├── graph.py             # LangGraph workflow builder
├── state.py             # Global state definitions
├── main.py              # Entry point
├── Dockerfile           # Container setup
├── requirements.txt     # Dependencies
├── README.md            # This file
└── LICENSE
```

## ⚙️ Installation

### Prerequisites
- Python 3.10+
- Git
- (Optional) Docker

### Steps

**MacOS / Linux**
```bash
git clone https://github.com/your-username/heimdall.git
cd heimdall
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

**Windows (PowerShell)**
```powershell
git clone https://github.com/your-username/heimdall.git
cd heimdall
python -m venv venv
.\venv\Scripts\activate
pip install -r requirements.txt
```

### Environment Variables

Create a `.env` file in root:

```env
ALPHAVANTAGE_API_KEY=your_api_key
OPENAI_API_KEY=your_api_key
```

## ▶️ Usage

**Run locally:**
```bash
python main.py
```

**Run with Docker:**
```bash
docker build -t heimdall .
docker run --env-file .env heimdall
```

## 🧪 Testing
```bash
pytest tests/
```

## 🛠️ Tech Stack
- Python 3.10+
- LangGraph for orchestration
- SQLite for local persistence
- Docker for containerization
- Pytest for testing

## 🚧 Roadmap
- [ ] Add real-time streaming data support
- [ ] Improve orchestration with adaptive mission planning
- [ ] CI/CD integration with GitHub Actions
- [ ] Expand test coverage and logging

## 📜 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
```

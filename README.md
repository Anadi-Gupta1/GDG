# 🚀 Quick Start: Generate Personalized Financial Advice  

### **Prerequisites**  
1. Google Cloud Account + [Enable Gemini API](https://ai.google.dev/)
2. Python 3.10+  

---

## 🔧 Installation  
```bash
pip install google-cloud-aiplatform python-dotenv
```

---

## 📄 Code Example: Gemini-Powered Risk Assessment  
Create `main.py`:  
```python
import os
from dotenv import load_dotenv
from google.cloud import aiplatform

# Load Gemini API key
load_dotenv()
aiplatform.init(project=os.getenv("GOOGLE_CLOUD_PROJECT"))

def generate_financial_advice(user_input: str) -> str:
    """
    Uses Gemini Pro to generate risk-aware financial advice.
    """
    model = aiplatform.Endpoint(
        endpoint_name="projects/your-project/locations/us-central1/endpoints/your-gemini-endpoint"
    )
    
    prompt = f"""
    As a financial advisor, analyze this user scenario:
    {user_input}
    
    Provide a step-by-step plan considering:
    - Risk tolerance
    - Market trends (as of 2024)
    - Tax implications
    Format: Bullet points with emojis.
    """
    
    response = model.predict(instances=[{"content": prompt}])
    return response.predictions[0]["content"]

# Example usage
if __name__ == "__main__":
    user_scenario = "I’m 28, earn $85k/year, and want to invest $20k in tech stocks and ETFs."
    advice = generate_financial_advice(user_scenario)
    print(f"📈 Gemini Advisor Recommendation:\n{advice}")
```

---

## 🛠️ Run It  
1. Set credentials:  
```bash
echo "GOOGLE_CLOUD_PROJECT=your-project-id" > .env
```
2. Execute:  
```bash
python main.py
```

---

## 📍 Sample Output  
```plaintext
📈 Gemini Advisor Recommendation:
1. 💼 Portfolio Split: 
   - 60% ETFs (VOO, QQQ) for broad market exposure
   - 30% Tech stocks (AI-focused companies like NVDA, MSFT)
   - 10% Cash reserve for dips

2. ⚠️ Risk Notes: 
   - Tech sector volatility: 25% avg swing (2024 forecast)
   - Hedge with 2026 LEAP puts on 10% of tech holdings

3. 💸 Tax Optimization: 
   - Use Roth IRA for $6k of investments (post-tax growth)
   - Tax-loss harvesting threshold: 15% loss
```

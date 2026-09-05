# Making a Request
# Request ပို့ခြင်း
Request = API ဆီ ပို့တဲ့ တောင်းဆိုချက်။

Making your first request to the Anthropic API is straightforward once you understand the basic setup and structure. This guide walks through the essential steps to get Claude responding to your prompts using Python.
အခြေခံ ပြင်ဆင်မှုနဲ့ ဖွဲ့စည်းပုံ နားလည်ရင် Anthropic API ဆီ ပထမ request ပို့တာ မခက်ဘူး။ ဒီလမ်းညွှန်က Python သုံးပြီး Claude က သင့် prompt ကို ဖြေအောင် လုပ်တဲ့ အဓိက အဆင့်တွေကို လျှောက်ပြမယ်။

## Setting Up Your Environment
## ပတ်ဝန်းကျင် ပြင်ဆင်ခြင်း
Environment = ကုဒ် ခိုင်းဖို့ လိုအပ်တဲ့ package နဲ့ setting တွေ။

Before making any API calls, you need to install the required packages and configure your API key securely.
API မခေါ်ခင်၊ လိုအပ်တဲ့ package တွေ တပ်ဆင်ပြီး API key ကို လုံလုံခြုံခြုံ ပြင်ဆင်ရမယ်။

First, install the necessary dependencies in your Jupyter notebook:
အရင်ဆုံး Jupyter notebook ထဲမှာ လိုအပ်တဲ့ package တွေ တပ်ဆင်ပါ။

`%pip install anthropic python-dotenv`

ကုဒ်အဓိပ္ပာယ်: `anthropic` နဲ့ `python-dotenv` နှစ်ခု တပ်ဆင်တယ်။

Next, create a .env file in the same directory as your notebook to store your API key securely:
နောက်တစ်ဆင့်၊ notebook ရှိတဲ့ ဖိုလ်ဒါထဲမှာ `.env` ဖိုင်လုပ်ပြီး API key ကို လုံလုံခြုံခြုံ သိမ်းပါ။

`ANTHROPIC_API_KEY="your-api-key-here"`

ကုဒ်အဓိပ္ပာယ်: API key ကို ဒီနေရာမှာ ထည့်သိမ်းတယ်။

This approach keeps your API key out of your code and prevents accidentally committing it to version control. Always add .env to your .gitignore file.
ဒီနည်းက API key ကို ကုဒ်ထဲ မထည့်အောင် ကာကွယ်တယ်။ Git ထဲ မတော်တဆ မတင်မိအောင်လည်း ကာကွယ်တယ်။ `.env` ကို `.gitignore` ဖိုင်ထဲ အမြဲ ထည့်ပါ။

Load the environment variables and create your API client:
Environment variable တွေ ဖွင့်ပြီး API client ဖန်တီးပါ။
Client = API ကို ခေါ်ပေးတဲ့ အရာ။

```
from dotenv import load_dotenv
load_dotenv()

from anthropic import Anthropic

client = Anthropic()
model = "claude-sonnet-4-0"
```

ကုဒ်အဓိပ္ပာယ်: `.env` က API key ဖတ်တယ်။ Anthropic client စတင်တယ်။ သုံးမယ့် model နာမည် သတ်မှတ်တယ်။

## The Create Function
## Create Function
`client.messages.create()` = Claude ဆီ message ပို့တဲ့ အဓိက function။

The core of making API requests is the client.messages.create() function. This function requires three key parameters:
API request ပို့တဲ့ အူတိုင်က `client.messages.create()` function ဖြစ်တယ်။ ဒီ function မှာ အဓိက parameter ၃ ခု လိုတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623269%2F03_-_003_-_Making_a_Request_09.1748623269461.png

model - The name of the Claude model you want to use
model - သုံးချင်တဲ့ Claude model နာမည်

max_tokens - A safety limit on response length (not a target)
max_tokens - အဖြေအရှည်အတွက် လုံခြုံရေး ကန့်သတ် (ပစ်မှတ် အရှည် မဟုတ်)

messages - The conversation history you're sending to Claude
messages - Claude ဆီ ပို့တဲ့ စကားပြောမှတ်တမ်း

The max_tokens parameter acts as a safety mechanism. If you set it to 1000, Claude will stop generating after 1000 tokens even if it has more to say. Claude doesn't try to reach this limit - it just writes what it thinks is appropriate and stops if it hits the maximum.
`max_tokens` parameter က လုံခြုံရေး ယန္တရား ဖြစ်တယ်။ ၁၀၀၀ ထားရင်၊ Claude မှာ ပြောစရာ ကျန်နေတောင် token ၁၀၀၀ မှာ ရပ်မယ်။ Claude က ဒီကန့်သတ်ကို ရောက်အောင် မရေးဘူး။ သင့်တယ်ထင်တဲ့စာ ရေးပြီး၊ အများဆုံး ရောက်မှ ရပ်တယ်။

## Understanding Messages
## Messages ကို နားလည်ခြင်း

Messages represent the conversation between you and Claude, similar to a chat application. There are two types of messages:
Messages ဆိုတာ သင်နဲ့ Claude ကြား စကားပြောမှတ်တမ်း။ Chat app နဲ့ တူတယ်။ Message အမျိုးအစား ၂ ခု ရှိတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623270%2F03_-_003_-_Making_a_Request_13.1748623270369.png

User messages - Content you want to send to Claude (written by humans)
User messages - Claude ဆီ ပို့ချင်တဲ့ စာ (လူရေးထားတာ)

Assistant messages - Responses that Claude has generated
Assistant messages - Claude ထုတ်တဲ့ အဖြေများ

Each message is a dictionary with a role (either "user" or "assistant") and content (the actual text).
Message တစ်ခုချင်းက dictionary ဖြစ်တယ်။ `role` ပါတယ် (`"user"` သို့မဟုတ် `"assistant"`)။ `content` မှာ တကယ့်စာ ပါတယ်။

## Making Your First Request
## ပထမ Request ပို့ခြင်း

Here's a complete example of making a request to Claude:
Claude ဆီ request ပို့တဲ့ ဥပမာ အပြည့်:

```
message = client.messages.create(
    model=model,
    max_tokens=1000,
    messages=[
        {
            "role": "user",
            "content": "What is quantum computing? Answer in one sentence"
        }
    ]
)
```

ကုဒ်အဓိပ္ပာယ်: Sonnet model သုံးပြီး၊ token အများဆုံး ၁၀၀၀၊ user က quantum computing ကို စာကြောင်းတစ်ကြောင်းနဲ့ ဖြေခိုင်းတယ်။

When you run this code, Claude will process your request and return a response object containing the generated text along with metadata about the request.
ဒီကုဒ်ကို ခိုင်းရင်၊ Claude က သင့် request ကို စီမံပြီး response object ပြန်ပေးမယ်။ ထွက်လာတဲ့စာနဲ့ request အကြောင်း metadata (အပိုအချက်အလက်) ပါတယ်။

## Extracting the Response
## အဖြေကို ထုတ်ယူခြင်း

The response object contains a lot of information, but you usually just want the generated text. Access it using:
Response object ထဲမှာ အချက်အလက် များတယ်။ ဒါပေမဲ့ အများအားဖြင့် ထွက်လာတဲ့စာပဲ လိုတယ်။ ဒီလို ယူပါ:

`message.content[0].text`

ကုဒ်အဓိပ္ပာယ်: ပထမ content block ထဲက စာသားကို ထုတ်ယူတယ်။

This gives you clean, readable output like: "Quantum computing is a type of computation that leverages quantum mechanics principles like superposition and entanglement to process information using quantum bits (qubits), potentially solving certain complex problems exponentially faster than classical computers."
ဒါက ဖတ်လွယ်တဲ့ သန့်တဲ့ အဖြေ ပေးတယ်။ ဥပမာ: "Quantum computing is a type of computation that leverages quantum mechanics principles like superposition and entanglement to process information using quantum bits (qubits), potentially solving certain complex problems exponentially faster than classical computers."
ရိုးရိုးပြောရင်: Quantum computing ဆိုတာ superposition နဲ့ entanglement လို quantum စည်းမျဉ်းတွေ သုံးပြီး qubit နဲ့ တွက်တဲ့ နည်း။ တချို့ ခက်ခဲတဲ့ ပြဿနာကို ပုံမှန်ကွန်ပျူတာထက် အများကြီး မြန်မြန် ဖြေရှင်းနိုင်တယ်။

With these basics in place, you can start experimenting with different prompts and building more complex interactions with Claude.
ဒီအခြေခံတွေ ရပြီဆိုရင်၊ prompt အမျိုးမျိုး စမ်းပြီး Claude နဲ့ ပိုရှုပ်ထွေးတဲ့ အပြန်အလှန်လုပ်မှုတွေ တည်ဆောက်လို့ရပြီ။

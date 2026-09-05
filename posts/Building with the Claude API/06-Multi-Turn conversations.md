# Multi-Turn Conversations
# အလှည့်လိုက် စကားပြောခြင်း
Multi-turn = အပြန်အလှန် အကြိမ်များစွာ စကားပြောတာ။

When working with the Anthropic API and Claude, there's a crucial concept you need to understand: Claude doesn't store any of your conversation history. Each request you make is completely independent, with no memory of previous exchanges.
Anthropic API နဲ့ Claude သုံးတဲ့အခါ နားလည်ရမယ့် အရေးကြီး အယူအဆ: Claude က သင့် စကားပြောမှတ်တမ်းကို မသိမ်းဘူး။ Request တစ်ခုချင်းစီက သီးသန့်။ ရှေ့က စကားကို မှတ်မထားဘူး။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623270%2F03_-_004_-_Multi-Turn_Conversations_01.1748623269971.png

This means if you want to have a multi-turn conversation where Claude remembers context from earlier messages, you need to handle the conversation state yourself.
ဒါကြောင့် Claude က ရှေ့က message တွေကို မှတ်ထားတဲ့ multi-turn စကားပြော လုပ်ချင်ရင်၊ စကားပြောအခြေအနေ (state) ကို ကိုယ်တိုင် ကိုင်တွယ်ရမယ်။

## The Problem with Stateless Conversations
## မှတ်ဉာဏ်မရှိတဲ့ စကားပြောရဲ့ ပြဿနာ
Stateless = ရှေ့က စကားကို မမှတ်ထားတာ။

Let's say you ask Claude "What is quantum computing?" and get a good response. Then you follow up with "Write another sentence" - Claude has no idea what you're referring to. It will write a sentence about something completely random because it has no memory of the quantum computing discussion.
ဥပမာ Claude ကို "What is quantum computing?" မေးပြီး ကောင်းတဲ့ အဖြေ ရတယ်။ နောက် "Write another sentence" လို့ ဆက်မေးရင် Claude က ဘာကို ဆိုလိုလဲ မသိဘူး။ Quantum computing အကြောင်းကို မှတ်မထားလို့၊ တခြား ကျပန်းအကြောင်း စာကြောင်း ရေးလိမ့်မယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623270%2F03_-_004_-_Multi-Turn_Conversations_02.1748623270625.png

## How Multi-Turn Conversations Work
## Multi-Turn စကားပြော ဘယ်လို အလုပ်လုပ်လဲ

To maintain conversation context, you need to do two things:
စကားပြော အကြောင်းအရာ (context) မပျောက်အောင် လုပ်ရမယ့်အချက် ၂ ခု:

- Manually maintain a list of all messages in your code
- ကုဒ်ထဲမှာ message အားလုံးရဲ့ စာရင်းကို ကိုယ်တိုင် သိမ်းထားပါ

- Send the complete message history with every request
- Request တိုင်းမှာ စကားပြောမှတ်တမ်း အပြည့် ပို့ပါ

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623271%2F03_-_004_-_Multi-Turn_Conversations_05.1748623271251.png

Here's the flow that actually works:
တကယ် အလုပ်လုပ်တဲ့ စီးဆင်းမှု:

1. Send your initial user message to Claude
1. ပထမ user message ကို Claude ဆီ ပို့ပါ

2. Take Claude's response and add it to your message list as an assistant message
2. Claude ရဲ့ အဖြေကို ယူပြီး message စာရင်းထဲ assistant message အဖြစ် ထည့်ပါ

3. Add your follow-up question as another user message
3. နောက်ဆက်တွဲ မေးခွန်းကို user message အသစ်အဖြစ် ထည့်ပါ

4. Send the entire conversation history to Claude
4. စကားပြောမှတ်တမ်း အပြည့်ကို Claude ဆီ ပို့ပါ

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623271%2F03_-_004_-_Multi-Turn_Conversations_08.1748623271832.png

## Building Helper Functions
## Helper Function များ တည်ဆောက်ခြင်း
Helper function = ထပ်ခါထပ်ခါ သုံးရလွယ်အောင် ရေးထားတဲ့ အကူအညီ function။

To make conversation management easier, you can create three helper functions:
စကားပြော စီမံရ လွယ်အောင် helper function ၃ ခု လုပ်လို့ရတယ်။

```
def add_user_message(messages, text):
    user_message = {"role": "user", "content": text}
    messages.append(user_message)

def add_assistant_message(messages, text):
    assistant_message = {"role": "assistant", "content": text}
    messages.append(assistant_message)

def chat(messages):
    message = client.messages.create(
        model=model,
        max_tokens=1000,
        messages=messages,
    )
    return message.content[0].text
```

ကုဒ်အဓိပ္ပာယ်:
- `add_user_message` = user စာကို မှတ်တမ်းထဲ ထည့်တယ်
- `add_assistant_message` = Claude အဖြေကို မှတ်တမ်းထဲ ထည့်တယ်
- `chat` = မှတ်တမ်းအပြည့်ကို Claude ဆီ ပို့ပြီး စာသားအဖြေ ပြန်ယူတယ်

## Putting It All Together
## အားလုံး ပေါင်းသုံးခြင်း

Here's how you use these functions to maintain a conversation:
ဒီ function တွေနဲ့ စကားပြောကို ဘယ်လို ထိန်းမလဲ:

```
# Start with an empty message list
messages = []

# Add the initial user question
add_user_message(messages, "Define quantum computing in one sentence")

# Get Claude's response
answer = chat(messages)

# Add Claude's response to the conversation history
add_assistant_message(messages, answer)

# Add a follow-up question
add_user_message(messages, "Write another sentence")

# Get the follow-up response with full context
final_answer = chat(messages)
```

ကုဒ်အဓိပ္ပာယ်: မှတ်တမ်း ဗလာနဲ့ စတယ်။ ပထမ မေးခွန်း ထည့်တယ်။ Claude ဖြေတယ်။ အဖြေကို မှတ်တမ်းထဲ ထည့်တယ်။ "Write another sentence" ထပ်ထည့်တယ်။ မှတ်တမ်းအပြည့်နဲ့ ပြန်ခေါ်တယ်။

Now Claude will understand that "Write another sentence" refers to expanding on the quantum computing definition, because you've provided the complete conversation context.
အခု Claude က "Write another sentence" ဆိုတာ quantum computing အဓိပ္ပာယ်ကို ဆက်ရေးခိုင်းတာလို့ နားလည်မယ်။ ဘာလို့လဲဆိုတော့ စကားပြော context အပြည့် ပေးထားလို့။

These helper functions will be useful throughout your work with Claude, making it much easier to build applications that can maintain meaningful conversations over multiple exchanges.
ဒီ helper function တွေက Claude နဲ့ အလုပ်လုပ်တဲ့အခါ အမြဲ အသုံးဝင်မယ်။ အကြိမ်များစွာ အဓိပ္ပာယ်ရှိအောင် စကားပြောနိုင်တဲ့ app တည်ဆောက်ရ ပိုလွယ်လာမယ်။

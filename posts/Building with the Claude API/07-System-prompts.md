# System Prompts
# System Prompt များ
System prompt = Claude ကို ဘယ်လို ပုံစံနဲ့ ဖြေရမလဲ ပြောတဲ့ ညွှန်ကြားချက်။

System prompts are a powerful way to customize how Claude responds to user input. Instead of getting generic answers, you can shape Claude's tone, style, and approach to match your specific use case.
System prompt တွေက Claude က user စာကို ဘယ်လို ပြန်ဖြေမလဲ ပြင်တဲ့ ခိုင်မာတဲ့ နည်း။ ရိုးရိုးအဖြေ မယူဘဲ၊ သင့်အလုပ်နဲ့ ကိုက်အောင် Claude ရဲ့ အသံထား၊ ပုံစံ၊ ချဉ်းကပ်ပုံကို ပုံဖော်လို့ရတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623273%2F03_-_006_-_System_Prompts_00.1748623272065.png

## Why System Prompts Matter
## System Prompt ဘာကြောင့် အရေးကြီးလဲ

Consider building a math tutor chatbot. When a student asks "How do I solve 5x + 2 = 3 for x?", you want Claude to act like a real tutor, not just spit out the answer. A good math tutor should:
သင်္ချာဆရာ chatbot တည်ဆောက်တယ်လို့ စဉ်းစားပါ။ ကျောင်းသားက "How do I solve 5x + 2 = 3 for x?" မေးရင်၊ Claude က အဖြေတန်းမပေးဘဲ တကယ့်ဆရာလို ပြုမူစေချင်တယ်။ ကောင်းတဲ့ သင်္ချာဆရာက:

- Initially give hints rather than complete solutions
- အရင်က အဖြေအပြည့် မပေးဘဲ ညွှန်ကြားချက် (hint) ပေးတယ်

- Patiently walk students through problems step by step
- စိတ်ရှည်ရှည်နဲ့ ပြဿနာကို အဆင့်ဆင့် ခေါ်သွားတယ်

- Show solutions for similar problems as examples
- ဆင်တူ ပြဿနာတွေရဲ့ အဖြေကို ဥပမာအဖြစ် ပြတယ်

You definitely don't want Claude to:
Claude ကို ဒီလို မလုပ်စေချင်ဘူး:

- Immediately give direct answers
- ချက်ချင်း အဖြေတိုက်ရိုက် ပေးတာ

- Tell students to just use a calculator
- ကျောင်းသားကို calculator သုံးရုံပဲ လို့ ပြောတာ

## How System Prompts Work
## System Prompt ဘယ်လို အလုပ်လုပ်လဲ

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623273%2F03_-_006_-_System_Prompts_05.1748623273817.png

System prompts provide Claude with guidance on how to respond. You define them as plain strings and pass them into the create function call. The key benefits are:
System prompt က Claude ကို ဘယ်လို ဖြေရမလဲ လမ်းညွှန်ပေးတယ်။ ရိုးရိုးစာသားအဖြစ် ရေးပြီး `create` function ခေါ်တဲ့အခါ ထည့်ပို့တယ်။ အဓိက အကျိုးတွေက:

- System prompts provide Claude guidance on how to respond
- System prompt က Claude ကို ဘယ်လို ဖြေရမလဲ လမ်းညွှန်ပေးတယ်

- Claude will try to respond in the same way someone in the specified role would respond
- Claude က သတ်မှတ်ထားတဲ့ အခန်းကဏ္ဍ (role) က လူတစ်ယောက်လို ဖြေအောင် ကြိုးစားတယ်

- Helps keep Claude on task
- Claude ကို အလုပ်ပေါ်မှာ ဆက်နေအောင် ကူညီတယ်

Here's the basic structure:
အခြေခံ ဖွဲ့စည်းပုံ:

```
system_prompt = """
You are a patient math tutor.
Do not directly answer a student's questions.
Guide them to a solution step by step.
"""

client.messages.create(
    model=model,
    messages=messages,
    max_tokens=1000,
    system=system_prompt
)
```

ကုဒ်အဓိပ္ပာယ်: စိတ်ရှည်တဲ့ သင်္ချာဆရာ role ပေးတယ်။ ကျောင်းသားမေးခွန်းကို တိုက်ရိုက် မဖြေနဲ့။ အဆင့်ဆင့် လမ်းညွှန်ပါ။ အဲဒီစာကို `system=` နဲ့ `create` ဆီ ပို့တယ်။

## Seeing the Difference
## ကွာခြားချက် ကြည့်ခြင်း

Without a system prompt, Claude gives a complete step-by-step solution immediately. This might be helpful, but it doesn't encourage the student to think through the problem themselves.
System prompt မပါရင် Claude က အဆင့်ဆင့် အဖြေအပြည့် ချက်ချင်း ပေးတယ်။ အကူအညီဖြစ်နိုင်တယ်။ ဒါပေမဲ့ ကျောင်းသား ကိုယ်တိုင် စဉ်းစားအောင် မတွန်းအားပေးဘူး။

With the math tutor system prompt, Claude's response changes dramatically. Instead of providing the full solution, Claude asks guiding questions like "What do you think would be a good first step to isolate x? Consider what operation we might need to perform on both sides to start moving terms around."
သင်္ချာဆရာ system prompt ပါရင် Claude ရဲ့ အဖြေ သိသိသာသာ ပြောင်းသွားတယ်။ အဖြေအပြည့် မပေးဘဲ၊ လမ်းညွှန်မေးခွန်း မေးတယ်။ ဥပမာ: "x ကို သီးသန့်ခွဲဖို့ ပထမအဆင့် ဘာကောင်းမလဲ။ နှစ်ဘက်လုံးမှာ ဘယ်လုပ်ဆောင်ချက် လုပ်ရင် စကားလုံးတွေ ရွှေ့လို့ရမလဲ စဉ်းစားပါ။"

## Building a Flexible Chat Function
## ပျော့ပြောင်းတဲ့ Chat Function တည်ဆောက်ခြင်း

Rather than hard-coding system prompts, you can make your chat function more reusable by accepting system prompts as parameters:
System prompt ကို ကုဒ်ထဲ ပုံသေ မရေးဘဲ၊ parameter အဖြစ် လက်ခံအောင် လုပ်ရင် `chat` function ကို ပိုပြန်သုံးလို့ရတယ်။

```
def chat(messages, system=None):
    params = {
        "model": model,
        "max_tokens": 1000,
        "messages": messages,
    }
    
    if system:
        params["system"] = system
    
    message = client.messages.create(**params)
    return message.content[0].text
```

ကုဒ်အဓိပ္ပာယ်: `system` ရှိမှ params ထဲ ထည့်တယ်။ ပြီးမှ `create` ခေါ်တယ်။ အဖြေစာသား ပြန်ပေးတယ်။

This approach handles an important detail: Claude's API doesn't accept `system=None`, so you need to conditionally include the system parameter only when it's provided.
ဒီနည်းက အရေးကြီး အသေးစိတ်တစ်ခု ကိုင်တယ်: Claude API က `system=None` ကို လက်မခံဘူး။ ဒါကြောင့် system prompt ပေးမှသာ `system` parameter ထည့်ရမယ်။

Now you can call your chat function with or without a system prompt:
အခု `chat` function ကို system prompt ပါ/မပါ ခေါ်လို့ရပြီ။

```
# Without system prompt
answer = chat(messages)

# With system prompt
system = """
You are a patient math tutor.
Do not directly answer a student's questions.
Guide them to a solution step by step.
"""
answer = chat(messages, system=system)
```

ကုဒ်အဓိပ္ပာယ်: ပထမခေါ်တာမှာ system prompt မပါ။ ဒုတိယမှာ သင်္ချာဆရာ prompt ထည့်ပြီး ခေါ်တယ်။

System prompts are essential for creating AI applications that behave consistently and appropriately for their intended purpose. They transform generic AI responses into specialized, role-appropriate interactions.
System prompt တွေက ရည်ရွယ်ချက်နဲ့ ကိုက်အောင် တည်ငြိမ်စွာ ပြုမူတဲ့ AI app လုပ်ဖို့ မဖြစ်မနေ လိုတယ်။ ရိုးရိုး AI အဖြေကို၊ အခန်းကဏ္ဍနဲ့ ကိုက်တဲ့ အထူးပြု အပြန်အလှန်လုပ်မှု ဖြစ်အောင် ပြောင်းပေးတယ်။

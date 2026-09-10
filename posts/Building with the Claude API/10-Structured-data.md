# Structured Data
# ဖွဲ့စည်းပုံရှိတဲ့ ဒေတာ
Structured data = JSON, ကုဒ်၊ စာရင်း စသဖြင့် ပုံစံတကျ ဒေတာ။

When you need Claude to generate structured data like JSON, Python code, or bulleted lists, you'll often run into a common problem: Claude wants to be helpful and add explanatory text around your content. While this is usually great, sometimes you need just the raw data with nothing else.
JSON, Python ကုဒ်၊ ဗုလက်စာရင်းလို ဖွဲ့စည်းပုံရှိတဲ့ ဒေတာ Claude ထုတ်စေချင်ရင်၊ မကြာခဏ တွေ့ရတဲ့ ပြဿနာ: Claude က ကူညီချင်လို့ ရှင်းလင်းချက် စာတွေ ပတ်ပြီး ထည့်တယ်။ အများအားဖြင့် ကောင်းတယ်။ ဒါပေမဲ့ တစ်ခါတလေ ကုန်ကြမ်းဒေတာပဲ လိုတယ်။ တခြားဘာမှ မလိုဘူး။

Consider building a web app that generates AWS EventBridge rules. Users enter a description, click generate, and expect to see clean JSON they can immediately copy and use. If Claude returns the JSON wrapped in markdown code blocks with explanatory text, users can't simply copy the entire response - they have to manually select just the JSON portion.
AWS EventBridge rule ထုတ်တဲ့ ဝက်ဘ် app လုပ်တယ်လို့ စဉ်းစားပါ။ User က ဖော်ပြချက် ရိုက်၊ generate နှိပ်၊ ကူးယူသုံးလို့ရတဲ့ သန့်တဲ့ JSON မျှော်တယ်။ Claude က JSON ကို markdown code block နဲ့ ရှင်းလင်းချက် ပတ်ပြီး ပေးရင်၊ အဖြေအပြည့် ကူးလို့ မရဘူး။ JSON အပိုင်းကို ကိုယ်တိုင် ရွေးရတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623326%2F03_-_011_-_Structured_Data_02.1748623325858.png

## The Problem with Default Responses
## ပုံမှန် အဖြေရဲ့ ပြဿနာ

By default, when you ask Claude to generate JSON, you might get something like this:
ပုံမှန်အားဖြင့် Claude ကို JSON ထုတ်ခိုင်းရင်၊ ဒီလို ရနိုင်တယ်။

```
```json
{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"],
  "detail": {
    "state": ["running"]
  }
}
```

This rule captures EC2 instance state changes when instances start running.
ဒီ rule က EC2 instance တွေ စပြီး running ဖြစ်တဲ့အခါ အခြေအနေပြောင်းတာကို ဖမ်းတယ်။

The JSON is correct, but it's wrapped in markdown formatting and includes explanatory text. For a web app where users need to copy the raw JSON, this creates friction in the user experience.
JSON က မှန်တယ်။ ဒါပေမဲ့ markdown ပုံစံနဲ့ ရှင်းလင်းချက် ပတ်ထားတယ်။ User က ကုန်ကြမ်း JSON ကူးရမယ့် ဝက်ဘ် app မှာ၊ ဒါက သုံးရတာ ကြမ်းစေတယ်။

## The Solution: Assistant Message Prefilling + Stop Sequences
## ဖြေရှင်းချက်: Assistant Message ကြိုဖြည့်ခြင်း + Stop Sequence များ
Prefill = Claude အဖြေကို ကိုယ်တိုင် ကြိုရေးပေးတာ။ Stop sequence = သတ်မှတ်စာသား ပေါ်ရင် ရပ်ခိုင်းတာ။

You can combine assistant message prefilling with stop sequences to get exactly the content you want. Here's how it works:
Assistant message ကြိုဖြည့်တာနဲ့ stop sequence ကို ပေါင်းသုံးရင်၊ လိုချင်တဲ့ အကြောင်းအရာပဲ ရတယ်။ ဘယ်လို အလုပ်လုပ်လဲ:

```
messages = []

add_user_message(messages, "Generate a very short event bridge rule as json")
add_assistant_message(messages, "```json")

text = chat(messages, stop_sequences=["```"])
```

ကုဒ်အဓိပ္ပာယ်: User က JSON တောင်းတယ်။ Assistant ဘက်မှာ `````json`` ကြိုဖြည့်တယ်။ ````` တွေ့ရင် ရပ်ခိုင်းတယ်။

This technique works by:
ဒီနည်း ဘယ်လို အလုပ်လုပ်လဲ:

1. The user message tells Claude what to generate
1. User message က Claude ကို ဘာထုတ်ရမလဲ ပြောတယ်

2. The prefilled assistant message makes Claude think it already started a markdown code block
2. ကြိုဖြည့်ထားတဲ့ assistant message က markdown code block စပြီးသား လို့ Claude ကို ထင်စေတယ်

3. Claude continues by writing just the JSON content
3. Claude က JSON အကြောင်းအရာပဲ ဆက်ရေးတယ်

4. When Claude tries to close the code block with ```, the stop sequence immediately ends generation
4. Claude က code block ကို ``` နဲ့ ပိတ်ဖို့ လုပ်ရင်၊ stop sequence က စာထုတ်တာ ချက်ချင်း ရပ်တယ်

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623327%2F03_-_011_-_Structured_Data_15.1748623326804.png

The result is clean JSON with no extra formatting:
ရလဒ်က ပုံစံအပို မပါတဲ့ သန့်တဲ့ JSON:

```
{
  "source": ["aws.ec2"],
  "detail-type": ["EC2 Instance State-change Notification"],
  "detail": {
    "state": ["running"]
  }
}
```

## Processing the Response
## အဖြေကို စီမံခြင်း

You might notice some extra newline characters in the response. These are easy to handle:
အဖြေထဲမှာ စာကြောင်းအသစ် အပိုတွေ ပါနေတာ တွေ့နိုင်တယ်။ ဒါတွေကို ကိုင်ရ လွယ်တယ်။

```
import json

# Clean up and parse the JSON
clean_json = json.loads(text.strip())
```

ကုဒ်အဓိပ္ပာယ်: `strip()` နဲ့ နေရာလွတ် ဖြတ်တယ်။ `json.loads` နဲ့ JSON ဖတ်တယ်။

## Beyond JSON
## JSON အပြင်

This technique isn't limited to JSON generation. Use it anytime you need structured data without commentary:
ဒီနည်းက JSON ထုတ်တာပဲ မဟုတ်ဘူး။ ရှင်းလင်းချက် မပါတဲ့ ဖွဲ့စည်းပုံရှိဒေတာ လိုတိုင်း သုံးပါ။

- Python code snippets
- Python ကုဒ် အပိုင်းလေးများ

- Bulleted lists
- ဗုလက်စာရင်းများ

- CSV data
- CSV ဒေတာ

- Any formatted content where you want just the content, not explanations
- ပုံစံချထားတဲ့ အကြောင်းအရာ၊ ရှင်းလင်းချက် မလိုဘဲ အကြောင်းအရာပဲ လိုတာ

The key is identifying what Claude naturally wants to wrap your content in, then using that as your prefill and stop sequence. For code, it's usually markdown code blocks. For lists, it might be different formatting markers.
အဓိကက Claude က ဘာနဲ့ ပတ်ချင်လဲ ရှာရတာ။ အဲဒါကို prefill နဲ့ stop sequence အဖြစ် သုံးပါ။ ကုဒ်အတွက် အများအားဖြင့် markdown code block။ စာရင်းအတွက် တခြား ပုံစံအမှတ် ဖြစ်နိုင်တယ်။

This approach gives you precise control over Claude's output format, making it much easier to integrate AI-generated content into applications where clean, structured data is essential.
ဒီနည်းက Claude အဖြေပုံစံကို တိတိကျကျ ထိန်းလို့ရတယ်။ သန့်တဲ့ ဖွဲ့စည်းပုံရှိဒေတာ လိုတဲ့ app ထဲ AI အဖြေ ပေါင်းထည့်ရ ပိုလွယ်လာတယ်။

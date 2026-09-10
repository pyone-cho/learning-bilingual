# Response Streaming
# အဖြေကို အပိုင်းလိုက် စီးထုတ်ခြင်း
Streaming = စာအပြည့် မစောင့်ဘဲ၊ ထွက်လာသလို အပိုင်းလိုက် ပြတာ။

When building chat applications with Claude, there's a significant user experience challenge: responses can take 10-30 seconds to generate, leaving users staring at a loading spinner. The solution is response streaming, which lets users see text appear chunk by chunk as Claude generates it, creating a much more responsive feel.
Claude နဲ့ chat app တည်ဆောက်တဲ့အခါ user အတွေ့အကြုံ ပြဿနာ ကြီးတစ်ခု ရှိတယ်။ အဖြေထုတ်တာ ၁၀-၃၀ စက္ကန့် ကြာနိုင်တယ်။ User က စောင့်နေတဲ့ အကွက်လေးပဲ ကြည့်နေရတယ်။ ဖြေရှင်းချက်က response streaming။ Claude စာထုတ်နေစဉ် အပိုင်းလေးတွေ အလိုက် ပြတယ်။ ဒါကြောင့် ပိုမြန်မြန် တုံ့ပြန်သလို ခံစားရတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623337%2F03_-_009_-_Response_Streaming_00.1748623336822.png

## The Problem with Standard Responses
## ပုံမှန် အဖြေရဲ့ ပြဿနာ

In a typical chat setup, your server sends a user message to Claude and waits for the complete response before sending anything back to the client. This creates an awkward delay where users have no feedback that anything is happening.
ပုံမှန် chat မှာ server က user message ကို Claude ဆီ ပို့ပြီး၊ အဖြေအပြည့် ရမှသာ client ဆီ ပြန်ပို့တယ်။ ဒါကြောင့် စောင့်ရတာ ကြာပြီး၊ တစ်ခုခု လုပ်နေတယ်ဆိုတဲ့ တုံ့ပြန်မှု user မရဘူး။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623338%2F03_-_009_-_Response_Streaming_02.1748623337803.png

## How Streaming Works
## Streaming ဘယ်လို အလုပ်လုပ်လဲ

With streaming enabled, Claude immediately sends back an initial response indicating it has received your request and is starting to generate text. Then you receive a series of events, each containing a small piece of the overall response.
Streaming ဖွင့်ထားရင် Claude က ချက်ချင်း ပထမအကြောင်းပြန်တယ်။ Request လက်ခံပြီး စာစထုတ်ပြီလို့ ပြောတယ်။ ပြီးရင် event တွေ ဆက်လာတယ်။ တစ်ခုချင်းမှာ အဖြေရဲ့ အပိုင်းလေး ပါတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623338%2F03_-_009_-_Response_Streaming_03.1748623338384.png

Your server can forward these text chunks to your client application as they arrive, allowing users to see the response building up word by word. All of these events are part of a single request to Claude.
Server က စာအပိုင်းလေးတွေ ရောက်လာသလို client app ဆီ ပြန်ပို့နိုင်တယ်။ User က စကားလုံးအလိုက် အဖြေ တည်ဆောက်လာတာ မြင်ရတယ်။ ဒီ event အားလုံးက Claude ဆီ တောင်းဆိုချက် တစ်ခုတည်းထဲမှာပဲ။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623339%2F03_-_009_-_Response_Streaming_04.1748623338949.png

## Understanding Stream Events
## Stream Event များကို နားလည်ခြင်း
Event = streaming လုပ်နေစဉ် Claude က ပို့တဲ့ အဖြစ်အပျက် / အချက်ပြမှု။

When you enable streaming, Claude sends back several types of events:
Streaming ဖွင့်ရင် Claude က event အမျိုးအစား များစွာ ပြန်ပို့တယ်။

- MessageStart - A new message is being sent
- MessageStart - message အသစ် စပို့ပြီ

- ContentBlockStart - Start of a new block containing text, tool use, or other content
- ContentBlockStart - စာ၊ tool use၊ သို့မဟုတ် တခြားအကြောင်းအရာ ပါတဲ့ block အသစ် စတယ်

- ContentBlockDelta - Chunks of the actual generated text
- ContentBlockDelta - တကယ့် ထွက်လာတဲ့ စာအပိုင်းလေးတွေ

- ContentBlockStop - The current content block has been completed
- ContentBlockStop - လက်ရှိ content block ပြီးပြီ

- MessageDelta - The current message is complete
- MessageDelta - လက်ရှိ message ပြီးပြီ

- MessageStop - End of information about the current message
- MessageStop - လက်ရှိ message အကြောင်း အချက်အလက် ဆုံးပြီ

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623339%2F03_-_009_-_Response_Streaming_11.1748623339633.png

The `ContentBlockDelta` events contain the actual generated text that you'll want to display to users.
`ContentBlockDelta` event တွေထဲမှာ user ကို ပြချင်တဲ့ တကယ့်စာ ပါတယ်။

## Basic Streaming Implementation
## Streaming အခြေခံ အကောင်အထည်ဖော်ခြင်း

To enable streaming, add stream=True to your messages.create call:
Streaming ဖွင့်ဖို့ `messages.create` ခေါ်တဲ့အခါ `stream=True` ထည့်ပါ။

```
messages = []
add_user_message(messages, "Write a 1 sentence description of a fake database")

stream = client.messages.create(
    model=model,
    max_tokens=1000,
    messages=messages,
    stream=True
)

for event in stream:
    print(event)
```

ကုဒ်အဓိပ္ပာယ်: `stream=True` ထားပြီး Claude ခေါ်တယ်။ ရောက်လာတဲ့ event တစ်ခုချင်းကို ပုံနှိပ်ပြတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623340%2F03_-_009_-_Response_Streaming_12.1748623340577.png

## Simplified Text Streaming
## စာသား Streaming ပိုလွယ်တဲ့နည်း

Rather than manually parsing events, you can use the SDK's simplified streaming interface that extracts just the text content:
Event တွေကို ကိုယ်တိုင် ခွဲဖတ်မယ့်အစား၊ SDK ရဲ့ လွယ်တဲ့ streaming မျက်နှာပြင် သုံးလို့ရတယ်။ စာသားပဲ ထုတ်ပေးတယ်။

```
with client.messages.stream(
    model=model,
    max_tokens=1000,
    messages=messages
) as stream:
    for text in stream.text_stream:
        print(text, end="")
```

ကုဒ်အဓိပ္ပာယ်: `text_stream` က စာအပိုင်းလေးတွေပဲ ပေးတယ်။ `end=""` ထားလို့ စာကြောင်းအသစ် မခွဲဘဲ ဆက်ရေးတယ်။

This approach automatically filters out everything except the actual text content, which is usually what you need for displaying responses to users.
ဒီနည်းက တကယ့်စာသားကလွဲရင် ကျန်တာ အလိုအလျောက် ဖယ်တယ်။ User ကို အဖြေပြဖို့ အများအားဖြင့် ဒါပဲ လိုတယ်။

## Getting the Complete Message
## Message အပြည့် ရယူခြင်း

While streaming individual chunks is great for user experience, you often need the complete message for storage or further processing. After streaming completes, you can get the assembled final message:
အပိုင်းလေးတွေ စီးထုတ်တာ user အတွက် ကောင်းတယ်။ ဒါပေမဲ့ သိမ်းဖို့၊ ဆက်စီမံဖို့ message အပြည့် မကြာခဏ လိုတယ်။ Streaming ပြီးရင် ပေါင်းပြီးသား နောက်ဆုံး message ယူလို့ရတယ်။

```
with client.messages.stream(
    model=model,
    max_tokens=1000,
    messages=messages
) as stream:
    for text in stream.text_stream:
        # Send each chunk to your client
        pass
    
    # Get the complete message for database storage
    final_message = stream.get_final_message()
```

ကုဒ်အဓိပ္ပာယ်: အပိုင်းလေးတွေကို client ဆီ ပို့နိုင်တယ်။ ပြီးရင် `get_final_message()` နဲ့ အပြည့်ယူပြီး database သိမ်းလို့ရတယ်။

This gives you the best of both worlds: real-time streaming for users and a complete message object for your application logic.
ဒါက နှစ်ခုလုံး ရတယ်။ User အတွက် အချိန်နဲ့တပြေးညီ streaming။ App logic အတွက် message object အပြည့်။

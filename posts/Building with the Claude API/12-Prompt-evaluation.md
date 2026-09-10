# Prompt Evaluation
# Prompt စစ်ဆေးအကဲဖြတ်ခြင်း
Prompt = Claude ဆီ ပို့တဲ့ ညွှန်ကြားစာ။ Evaluation = ကောင်းမကောင်း တိုင်းတာခြင်း။

When working with Claude, writing a good prompt is just the beginning. To build reliable AI applications, you need to understand two critical concepts: prompt engineering and prompt evaluation. Prompt engineering gives you techniques for writing better prompts, while prompt evaluation helps you measure how well those prompts actually work.
Claude နဲ့ အလုပ်လုပ်တဲ့အခါ ကောင်းတဲ့ prompt ရေးတာက အစပဲ။ ယုံကြည်ရတဲ့ AI app တည်ဆောက်ဖို့၊ အရေးကြီး အယူအဆ ၂ ခု နားလည်ရမယ်။ Prompt engineering နဲ့ prompt evaluation။ Prompt engineering က ပိုကောင်းတဲ့ prompt ရေးနည်း ပေးတယ်။ Prompt evaluation က အဲဒီ prompt တွေ တကယ် ဘယ်လောက် ကောင်းလဲ တိုင်းပေးတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623381%2F04_-_001_-_Prompt_Evaluation_00.1748623381094.png

## Prompt Engineering vs Prompt Evaluation
## Prompt Engineering နှင့် Prompt Evaluation

Prompt engineering is your toolkit for crafting effective prompts. It includes techniques like:
Prompt engineering က ထိရောက်တဲ့ prompt ရေးဖို့ သုံးတဲ့ ကိရိယာအစု။ ဥပမာ နည်းတွေ:

- Multishot prompting
- Multishot prompting = ဥပမာ များစွာ ထည့်ပြီး လမ်းညွှန်တာ

- Structuring with XML tags
- XML tag နဲ့ ဖွဲ့စည်းပုံချခြင်း

- Many other best practices
- တခြား ကောင်းမွန်တဲ့ လုပ်နည်းများစွာ

These techniques help Claude understand exactly what you're asking for and how you want it to respond.
ဒီနည်းတွေက သင်ဘာတောင်းလဲ၊ ဘယ်လို ဖြေစေချင်လဲ Claude တိတိကျကျ နားလည်အောင် ကူညီတယ်။

Prompt evaluation takes a different approach. Instead of focusing on how to write prompts, it's about measuring their effectiveness through automated testing. You can:
Prompt evaluation က ချဉ်းကပ်ပုံ မတူဘူး။ Prompt ဘယ်လို ရေးမလဲ မဟုတ်ဘဲ၊ အလိုအလျောက် စမ်းသပ်ပြီး ထိရောက်မှု တိုင်းတာတယ်။ လုပ်လို့ရတာ:

- Test against expected answers
- မျှော်လင့်တဲ့ အဖြေနဲ့ နှိုင်းယှဉ် စမ်းခြင်း

- Compare different versions of the same prompt
- Prompt တူရဲ့ ဗားရှင်း မတူတာတွေ နှိုင်းယှဉ်ခြင်း

- Review outputs for errors
- အဖြေတွေမှာ အမှား ရှိမရှိ စစ်ခြင်း

## Three Paths After Writing a Prompt
## Prompt ရေးပြီးရင် လမ်း ၃ ခု

Once you've drafted a prompt, you typically face three options for what to do next:
Prompt မူကြမ်း ရေးပြီးရင်၊ နောက်ဘာလုပ်မလဲ ဆိုတဲ့ ရွေးစရာ ၃ ခု မကြာခဏ ရှိတယ်။

https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748623382%2F04_-_001_-_Prompt_Evaluation_10.1748623382207.png

Option 1: Test the prompt once and decide it's good enough. This carries a significant risk of breaking in production when users provide unexpected inputs.
ရွေးချယ်မှု ၁: Prompt ကို တစ်ခါပဲ စမ်းပြီး လုံလောက်ပြီလို့ ဆုံးဖြတ်တာ။ Production (တကယ့်အသုံး) မှာ user က မမျှော်လင့်တဲ့ input ပေးရင် ပျက်နိုင်တဲ့ အန္တရာယ် ကြီးတယ်။

Option 2: Test the prompt a few times and tweak it to handle a corner case or two. While better than option 1, users will often provide very unexpected outputs that you haven't considered.
ရွေးချယ်မှု ၂: Prompt ကို ခဏခဏ စမ်းပြီး၊ ထူးခြားဖြစ်ရပ် တစ်ခုနှစ်ခု အတွက် နည်းနည်း ပြင်တာ။ ရွေးချယ်မှု ၁ ထက် ပိုကောင်းတယ်။ ဒါပေမဲ့ user တွေက မစဉ်းစားထားတဲ့ မမျှော်လင့် input တွေ မကြာခဏ ပေးတတ်တယ်။

Option 3: Run the prompt through an evaluation pipeline to score it, then iterate on the prompt based on objective metrics. This approach requires more work and cost, but gives you much more confidence in your prompt's reliability.
ရွေးချယ်မှု ၃: Prompt ကို evaluation pipeline ထဲ ခိုင်းပြီး မှတ်ချက်ယူပါ။ ပြီးရင် ဘက်မလိုက် တိုင်းတာချက် (metric) အရ prompt ကို ထပ်ပြင်ပါ။ ဒီနည်းက အလုပ်ပိုများ၊ ကုန်ကျစရိတ် ပိုများတယ်။ ဒါပေမဲ့ prompt ယုံကြည်ရမှုကို ပိုသေချာစေတယ်။

## Why Most Engineers Fall Into Testing Traps
## Engineer အများစု ဘာကြောင့် စမ်းသပ်မှု ထောင်ချောက်ထဲ ကျလဲ

Options 1 and 2 are common traps that all engineers fall into, myself included. It's natural to write a prompt for a serious application and not test it thoroughly enough. We tend to underestimate how many edge cases real users will encounter.
ရွေးချယ်မှု ၁ နဲ့ ၂ က Engineer အားလုံး ကျတတ်တဲ့ ထောင်ချောက်။ ကျွန်တော်လည်း ပါတယ်။ အရေးကြီး app အတွက် prompt ရေးပြီး၊ လုံလုံလောက်လောက် မစမ်းမိတာ သဘာဝကျတယ်။ တကယ့် user တွေ ကြုံမယ့် edge case (အစွန်းရောက်ဖြစ်ရပ်) ဘယ်လောက်များမလဲ ဆိုတာကို နည်းနည်းပဲ ခန့်မှန်းတတ်တယ်။

The reality is that when you deploy a prompt to production, users will interact with it in ways you never anticipated. What seemed like a solid prompt during your limited testing can quickly break down when faced with the full variety of real-world inputs.
တကယ်က prompt ကို production တင်လိုက်ရင်၊ user တွေက မတွေးထားတဲ့ ပုံစံနဲ့ သုံးကြမယ်။ စမ်းနည်းနည်းနဲ့ ခိုင်မာတယ်ထင်တဲ့ prompt က၊ တကယ့်ကမ္ဘာက input အမျိုးမျိုးနဲ့ ကြုံရင် မြန်မြန် ပျက်နိုင်တယ်။

## The Evaluation-First Approach
## Evaluation ကို အရင်လုပ်တဲ့ ချဉ်းကပ်ပုံ

Option 3 represents a more systematic approach to prompt development. By running your prompt through an evaluation pipeline, you get objective metrics about its performance across a broader range of test cases. This data-driven approach lets you:
ရွေးချယ်မှု ၃ က prompt ဖွံ့ဖြိုးမှုကို ပိုစနစ်ကျအောင် လုပ်တဲ့ နည်း။ Prompt ကို evaluation pipeline ထဲ ခိုင်းရင်၊ စမ်းသပ်မှု ပိုကျယ်တဲ့ အပိုင်းမှာ စွမ်းရည်ကို ဘက်မလိုက် တိုင်းတာချက် ရတယ်။ ဒေတာအခြေခံ ဒီနည်းက ဒီလို လုပ်ခွင့်ပေးတယ်:

- Identify weaknesses before they become production issues
- Production ပြဿနာ မဖြစ်ခင် အားနည်းချက် ရှာခြင်း

- Compare different prompt versions objectively
- Prompt ဗားရှင်း မတူတာတွေကို ဘက်မလိုက် နှိုင်းယှဉ်ခြင်း

- Iterate with confidence based on measurable improvements
- တိုင်းလို့ရတဲ့ တိုးတက်မှုအရ သေချာသေချာ ထပ်ပြင်ခြင်း

- Build more reliable AI applications
- ပိုယုံကြည်ရတဲ့ AI app တည်ဆောက်ခြင်း

While this approach requires more upfront investment in time and testing infrastructure, it pays dividends in the reliability and robustness of your final application. The goal is to catch problems during development rather than after your users encounter them.
ဒီနည်းက အချိန်နဲ့ စမ်းသပ်စနစ်ကို အရင် ပိုရင်းရတယ်။ ဒါပေမဲ့ နောက်ဆုံး app ရဲ့ ယုံကြည်ရမှုနဲ့ ခိုင်မာမှုမှာ ပြန်အကျိုးရှိတယ်။ ပန်းတိုင်က user မကြုံခင်၊ ဖွံ့ဖြိုးနေစဉ်မှာ ပြဿနာ ဖမ်းဖို့။

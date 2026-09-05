<notes>
<critical>
Below are notes from a video course about working with the Claude language model.
ဒီအောက်မှာ Claude language model နဲ့ အလုပ်လုပ်တဲ့ video course မှတ်စုတွေ ရှိပါတယ်။

Use these notes as a resource to answer the user's question.
ဒီမှတ်စုတွေကို သုံးပြီး user ရဲ့ မေးခွန်းကို ဖြေပါ။

Write your answer as a standalone response - do not refer directly to these notes unless specifically requested by the user.
အဖြေကို သီးသန့် စာတစ်ပုဒ်လို ရေးပါ။ user က တောင်းမှသာ ဒီမှတ်စုတွေကို တိုက်ရိုက် ညွှန်းပါ။
</critical>

<note title="Overview of Claude Models">
Overview of Claude Models
Claude Model တွေ အကြောင်း အနှစ်ချုပ်

Claude has three model families optimized for different priorities:
Claude မှာ အဓိက ရည်ရွယ်ချက် မတူတဲ့ model မိသားစု ၃ မျိုး ရှိပါတယ်။

Opus = highest intelligence model for complex, multi-step tasks requiring deep reasoning and planning. Trade-off: higher cost and latency.
Opus = ဉာဏ်အကောင်းဆုံး model။ ခက်ခဲပြီး အဆင့်များတဲ့ အလုပ်၊ နက်နက်ရှိုင်းရှိုင်း စဉ်းစားရတာ၊ အစီအစဉ်ဆွဲရတာတွေအတွက်။ အားနည်းချက်: ပိုက်ဆံ ပိုကုန်ပြီး နှေးတယ်။

Sonnet = balanced model with good intelligence, speed, and cost efficiency. Strong coding abilities and precise code editing. Best for most practical use cases.
Sonnet = ဉာဏ်၊ အမြန်နှုန်း၊ ကုန်ကျစရိတ် သုံးမျိုးလုံး မျှတတဲ့ model။ ကုဒ်ရေးတာ၊ ကုဒ်ပြင်တာ အားကောင်းတယ်။ လက်တွေ့ အလုပ်အများစုအတွက် အကောင်းဆုံး။

Haiku = fastest model optimized for speed and cost efficiency. No reasoning capabilities like Opus/Sonnet. Best for real-time user interactions and high-volume processing.
Haiku = အမြန်ဆုံး model။ မြန်မြန်လုပ်ချင်တာ၊ ပိုက်ဆံ သက်သာချင်တာအတွက်။ Opus/Sonnet လို နက်နက်ရှိုင်းရှိုင်း စဉ်းစားတဲ့ စွမ်းရည် မရှိဘူး။ အချိန်နဲ့တပြေးညီ user နဲ့ စကားပြောတာ၊ အလုပ်အများကြီး လုပ်တာအတွက် ကောင်းတယ်။

Selection framework: Intelligence priority → Opus. Speed priority → Haiku. Balanced requirements → Sonnet.
ရွေးချယ်ပုံ: ဉာဏ်အရေးကြီးရင် → Opus။ မြန်ချင်ရင် → Haiku။ မျှတချင်ရင် → Sonnet။

Common approach = use multiple models in same application based on specific task requirements rather than single model selection.
အများသုံးနည်း = app တစ်ခုထဲမှာ model တစ်ခုတည်း မရွေးဘဲ၊ အလုပ်တစ်ခုချင်းစီအလိုက် model အမျိုးမျိုး သုံးပါ။

All models share core capabilities: text generation, coding, image analysis. Main difference is optimization focus.
Model အားလုံးမှာ အခြေခံ စွမ်းရည်တူတယ်: စာရေးတာ၊ ကုဒ်ရေးတာ၊ ပုံကြည့်တာ။ ကွာတာက ဘယ်အချက်ကို ပိုအာရုံစိုက်လဲ ဆိုတာပဲ။
</note>

<note title="Accessing the API">
Accessing the API
API ကို ဘယ်လို သုံးမလဲ
API = app ကနေ Claude ကို ခေါ်တဲ့ တံခါးပေါက်။

API Access Flow = 5-step process from user input to response display
API သုံးပုံ စီးဆင်းမှု = user ရိုက်တဲ့စာ ကနေ အဖြေပြတဲ့အထိ အဆင့် ၅ ဆင့်။

Step 1: Client sends user text to developer's server (never access Anthropic API directly from client apps to keep API key secret)
အဆင့် ၁: Client (ဖုန်း/ဝက်ဘ်) က user ရဲ့ စာကို developer ရဲ့ server ဆီ ပို့တယ်။ Client app ကနေ Anthropic API ကို တိုက်ရိုက် မခေါ်ပါနဲ့။ API key (လျှို့ဝှက်ကီး) ပေါက်မှာ စိုးလို့။

Step 2: Server makes request to Anthropic API using SDK (Python, TypeScript, JavaScript, Go, Ruby) or plain HTTP. Required parameters = API key + model name + messages list + max_tokens limit
အဆင့် ၂: Server က Anthropic API ဆီ တောင်းဆိုတယ်။ SDK (အဆင်သင့် ကုဒ်အထုပ်) သုံးလို့ရတယ်။ Python, TypeScript, JavaScript, Go, Ruby ရှိတယ်။ သို့မဟုတ် ရိုးရိုး HTTP နဲ့လည်း ရတယ်။ မဖြစ်မနေ ပို့ရမယ့်အချက် = API key + model နာမည် + messages စာရင်း + max_tokens ကန့်သတ်။

Step 3: Text generation process has 4 stages:
အဆင့် ၃: စာထုတ်တဲ့ လုပ်ငန်းမှာ အဆင့် ၄ ဆင့် ရှိတယ်။

- Tokenization = breaking input into tokens (words/word parts/symbols/spaces)
- Tokenization = ထည့်လိုက်တဲ့စာကို token လေးတွေ ခွဲတာ (စကားလုံး / စကားလုံးအစိတ် / သင်္ကေတ / နေရာလွတ်)

- Embedding = converting tokens to number lists representing all possible word meanings
- Embedding = token တွေကို ဂဏန်းစာရင်း ပြောင်းတာ။ အဲဒီဂဏန်းတွေက စကားလုံး အဓိပ္ပာယ် ဖြစ်နိုင်တာတွေကို ကိုယ်စားပြုတယ်။

- Contextualization = adjusting embeddings based on neighboring tokens to determine precise meaning
- Contextualization = ဘေးက token တွေကို ကြည့်ပြီး embedding ကို ချိန်တာ။ ဒီစကားလုံးရဲ့ တိတိကျကျ အဓိပ္ပာယ်ကို ရှာဖို့။

- Generation = output layer produces probabilities for next word, model selects using probability + randomness, adds selected word, repeats process
- Generation = နောက်စကားလုံး ဖြစ်နိုင်ခြေတွေ ထုတ်တယ်။ model က ဖြစ်နိုင်ခြေ + ကျပန်းရွေးချယ်မှု နဲ့ ရွေးတယ်။ ရွေးထားတဲ့ စကားလုံး ထည့်တယ်။ ဒီလို ထပ်လုပ်တယ်။

Step 4: Model stops when max_tokens reached or special end_of_sequence token generated
အဆင့် ၄: max_tokens ပြည့်ရင်၊ သို့မဟုတ် ပြီးဆုံးကြောင်း အထူး token ထွက်လာရင် model ရပ်တယ်။

Step 5: API returns response with generated text + usage counts + stop_reason to server, server sends to client for display
အဆင့် ၅: API က ထွက်လာတဲ့စာ + သုံးသွားတဲ့ အရေအတွက် + ဘာကြောင့်ရပ်လဲ (stop_reason) ကို server ဆီ ပြန်ပို့တယ်။ Server က client ဆီ ပို့ပြီး မျက်နှာပြင်မှာ ပြတယ်။

Token = text chunk (word/part/symbol)
Token = စာအပိုင်းလေး (စကားလုံး / အစိတ်အပိုင်း / သင်္ကေတ)

Embedding = numerical representation of word meanings
Embedding = စကားလုံး အဓိပ္ပာယ်ကို ဂဏန်းနဲ့ ပြထားတာ

Contextualization = meaning refinement using neighboring words
Contextualization = ဘေးက စကားလုံးတွေ သုံးပြီး အဓိပ္ပာယ်ကို ပိုတိကျအောင် ချိန်တာ

Max_tokens = generation length limit
Max_tokens = ဘယ်လောက်အထိ စာထုတ်မလဲ ဆိုတဲ့ ကန့်သတ်

Stop_reason = why model stopped generating
Stop_reason = model ဘာကြောင့် စာထုတ်တာ ရပ်လဲ
</note>

<note title="Making a Request">
Making a Request
Request တစ်ခု ဘယ်လို ပို့မလဲ
Request = API ဆီ ပို့တဲ့ တောင်းဆိုချက်။

Making API Request to Anthropic = Process involving 4 setup steps and understanding message structure
Anthropic ဆီ API request ပို့တာ = ပြင်ဆင်အဆင့် ၄ ဆင့် + message ဖွဲ့စည်းပုံ နားလည်ရတယ်။

Setup Steps:
ပြင်ဆင်အဆင့်များ:

1. Install packages = pip install anthropic python-dotenv in Jupyter notebook
1. Package တပ်ဆင်ပါ = Jupyter notebook ထဲမှာ `pip install anthropic python-dotenv`

2. Store API key = Create .env file with ANTHROPIC_API_KEY="your_key" (ignore in version control)
2. API key သိမ်းပါ = `.env` ဖိုင်လုပ်ပြီး `ANTHROPIC_API_KEY="your_key"` ထည့်ပါ။ Git ထဲ မတင်ပါနဲ့။

3. Load environment variable = Use python-dotenv to securely load API key
3. Environment variable ဖွင့်ပါ = python-dotenv နဲ့ API key ကို လုံလုံခြုံခြုံ ဖတ်ပါ။

4. Create client = Initialize anthropic client and define model variable (claude-3-sonnet)
4. Client ဖန်တီးပါ = anthropic client စတင်ပြီး model နာမည် သတ်မှတ်ပါ (ဥပမာ claude-3-sonnet)။

API Request Structure:
API Request ဖွဲ့စည်းပုံ:

- Function = client.messages.create()
- Function = `client.messages.create()`

- Required arguments = model, max_tokens, messages
- မဖြစ်မနေ ပေးရမယ့်အချက် = model, max_tokens, messages

- Model = Name of Claude model to use
- Model = သုံးမယ့် Claude model နာမည်

- Max_tokens = Safety limit for generation length (not target length)
- Max_tokens = စာဘယ်လောက်အထိ ထုတ်လို့ရလဲ ဆိုတဲ့ လုံခြုံရေးကန့်သတ်။ ပစ်မှတ် အရှည် မဟုတ်ဘူး။

- Messages = List containing conversation exchanges
- Messages = စကားပြောလဲလှယ်မှုတွေ ပါတဲ့ စာရင်း

Message Types:
Message အမျိုးအစားများ:

- User message = {"role": "user", "content": "your text"} (human-authored content)
- User message = `{"role": "user", "content": "your text"}` (လူရေးထားတဲ့ စာ)

- Assistant message = Contains model-generated responses
- Assistant message = model ထုတ်တဲ့ အဖြေတွေ ပါတယ်

Response Access:
အဖြေကို ဘယ်လို ယူမလဲ:

- Full response = Contains metadata and nested structure
- အဖြေအပြည့် = metadata (အပိုအချက်အလက်) နဲ့ အထပ်ထပ် ဖွဲ့စည်းပုံ ပါတယ်

- Text only = message.content[0].text extracts just generated text
- စာသက်သက် = `message.content[0].text` က ထွက်လာတဲ့စာကိုပဲ ထုတ်ယူတယ်

Example request structure: client.messages.create(model=model, max_tokens=1000, messages=[{"role": "user", "content": "What is quantum computing?"}])
ဥပမာ request ဖွဲ့စည်းပုံ: `client.messages.create(model=model, max_tokens=1000, messages=[{"role": "user", "content": "What is quantum computing?"}])`
</note>

<note title="Multi-Turn Conversations">
Multi-Turn Conversations
အလှည့်လိုက် စကားပြောခြင်း
Multi-turn = အပြန်အလှန် အကြိမ်များစွာ စကားပြောတာ။

Multi-Turn Conversations = conversations with multiple back-and-forth exchanges that maintain context.
Multi-Turn Conversations = အပြန်အလှန် စကားများစွာ ပြောပြီး၊ ရှေ့က စကားကို မမေ့ဘဲ ဆက်နားလည်တာ။

Key limitation: Anthropic API stores no messages. Each request is independent with no memory of previous exchanges.
အရေးကြီး ကန့်သတ်: Anthropic API က message တွေ မသိမ်းဘူး။ Request တစ်ခုချင်းစီက သီးသန့်။ ရှေ့က စကားကို မှတ်မထားဘူး။

Solution requires two steps:
ဖြေရှင်းနည်းမှာ အဆင့် ၂ ဆင့် လိုတယ်။

1. Manually maintain message list in code
1. ကုဒ်ထဲမှာ message စာရင်းကို ကိုယ်တိုင် သိမ်းထားပါ

2. Send entire conversation history with every follow-up request
2. နောက်ထပ် မေးတိုင်း စကားပြောမှတ်တမ်း အပြည့် ပို့ပါ

Message structure = list of dictionaries with "role" (user/assistant) and "content" fields.
Message ဖွဲ့စည်းပုံ = dictionary စာရင်း။ တစ်ခုချင်းမှာ `"role"` (user/assistant) နဲ့ `"content"` ရှိတယ်။

Conversation flow:
စကားပြော စီးဆင်းမှု:

- Send initial user message
- ပထမ user message ပို့ပါ

- Receive assistant response
- Assistant အဖြေ လက်ခံပါ

- Append assistant response to message history
- Assistant အဖြေကို မှတ်တမ်းထဲ ထည့်ပါ

- Add new user message to history
- user ရဲ့ စာအသစ်ကို မှတ်တမ်းထဲ ထည့်ပါ

- Send complete history for context-aware follow-up
- မှတ်တမ်းအပြည့် ပို့ပြီး ရှေ့ကအကြောင်းကို သိတဲ့ နောက်ဆက်တွဲ မေးခွန်း လုပ်ပါ

Helper functions needed:
အကူအညီ function တွေ လိုတယ်:

- add_user_message(messages, text) = appends user message to history
- `add_user_message(messages, text)` = user message ကို မှတ်တမ်းထဲ ထည့်တယ်

- add_assistant_message(messages, text) = appends assistant response to history
- `add_assistant_message(messages, text)` = assistant အဖြေကို မှတ်တမ်းထဲ ထည့်တယ်

- chat(messages) = sends message history to API and returns response
- `chat(messages)` = မှတ်တမ်းကို API ဆီ ပို့ပြီး အဖြေ ပြန်ယူတယ်

Without message history = responses lack context and continuity. With complete history = Claude maintains conversation context and provides relevant follow-ups.
မှတ်တမ်း မပါရင် = အဖြေတွေက ရှေ့နောက် မဆက်ဘူး။ မှတ်တမ်းအပြည့် ပါရင် = Claude က စကားပြောအကြောင်းအရာကို မှတ်ပြီး သက်ဆိုင်တဲ့ နောက်ဆက်တွဲ အဖြေ ပေးတယ်။
</note>

<note title="System Prompts">
System Prompts
System Prompt များ
System prompt = Claude ကို ဘယ်လို လူ / ဘယ်လို ပုံစံနဲ့ ဖြေရမလဲ ပြောတဲ့ ညွှန်ကြားချက်။

System Prompts = technique to customize Claude's response style and tone by assigning it a specific role or behavior pattern.
System Prompts = Claude ကို အခန်းကဏ္ဍ သို့မဟုတ် အပြုအမူ ပုံစံ ပေးပြီး၊ အဖြေပုံစံနဲ့ အသံနေအသံထားကို ပြင်တဲ့ နည်း။

Implementation = pass system prompt as plain string to create function using system keyword argument.
လုပ်ပုံ = `create` function ဆီ `system` ဆိုတဲ့ argument နဲ့ ရိုးရိုးစာသား prompt ပို့ပါ။

Purpose = control how Claude responds rather than what it responds. Example: math tutor role makes Claude give hints instead of direct answers.
ရည်ရွယ်ချက် = ဘာဖြေမလဲ မဟုတ်ဘဲ ဘယ်လိုဖြေမလဲ ကို ထိန်းချုပ်တာ။ ဥပမာ: သင်္ချာဆရာ အခန်းကဏ္ဍ ပေးရင် Claude က အဖြေတန်းမပေးဘဲ ညွှန်ကြားချက်ပဲ ပေးတယ်။

Structure = first line typically assigns role ("You are a patient math tutor"), followed by specific behavioral instructions.
ဖွဲ့စည်းပုံ = ပထမစာကြောင်းမှာ အခန်းကဏ္ဍ ပေးတယ် ("You are a patient math tutor")။ နောက်မှာ ဘယ်လို ပြုမူရမလဲ ညွှန်ကြားတယ်။

Key principle = system prompts guide response approach, not content. Same question gets different treatment based on assigned role.
အဓိက စည်းမျဉ်း = system prompt က ဖြေပုံကို လမ်းညွှန်တယ်။ အကြောင်းအရာကို မပြဌာန်းဘူး။ မေးခွန်းတူရင်တောင် အခန်းကဏ္ဍပေါ်မူတည်ပြီး ဖြေပုံ ကွာတယ်။

Technical implementation = create params dictionary, conditionally add system key if prompt provided, pass params to create function with ** unpacking. Handle None case by excluding system parameter entirely.
နည်းပညာအရ လုပ်ပုံ = params dictionary လုပ်ပါ။ prompt ရှိမှ `system` key ထည့်ပါ။ `**` နဲ့ `create` function ဆီ ဖြန့်ပို့ပါ။ prompt မရှိရင် (`None`) `system` parameter ကို လုံးဝ မထည့်ပါနဲ့။

Use case example = Math tutor that gives guidance/hints rather than complete solutions, encouraging student thinking over direct answers.
သုံးပုံ ဥပမာ = သင်္ချာဆရာက အဖြေအပြည့် မပေးဘဲ လမ်းညွှန် / ညွှန်ကြားချက် ပေးတယ်။ ကျောင်းသား ကိုယ်တိုင် စဉ်းစားအောင် လုပ်တယ်။
</note>

<note title="Temperature">
Temperature
Temperature (ကျပန်းဖြစ်မှု)
Temperature = Claude က စကားလုံး ရွေးတဲ့အခါ ဘယ်လောက် ကျပန်း / ဖန်တီးမှု များမလဲ။

Temperature = parameter (0-1) that controls randomness in Claude's text generation by influencing token selection probabilities.
Temperature = ၀ ကနေ ၁ အတွင်း parameter။ Claude စာထုတ်တဲ့အခါ token ရွေးတဲ့ ဖြစ်နိုင်ခြေကို ပြောင်းပြီး၊ ဘယ်လောက် ကျပန်းဖြစ်မလဲ ထိန်းတယ်။

Text generation process: Input text → tokenization → probability assignment to possible next tokens → token selection based on probabilities → repeat.
စာထုတ်ပုံ: ထည့်တဲ့စာ → tokenization → နောက် token ဖြစ်နိုင်ခြေ ပေး → ဖြစ်နိုင်ခြေအရ ရွေး → ထပ်လုပ်။

Temperature effects:
Temperature ရဲ့ အကျိုးသက်ရောက်မှု:

- Temperature 0 = deterministic output, always selects highest probability token
- Temperature 0 = အမြဲတမ်း တူတဲ့ အဖြေ။ ဖြစ်နိုင်ခြေ အမြင့်ဆုံး token ကိုပဲ ရွေးတယ်။

- Higher temperature = increases chance of selecting lower probability tokens, more creative/unexpected outputs
- Temperature မြင့်ရင် = ဖြစ်နိုင်ခြေ နည်းတဲ့ token တွေ ရွေးနိုင်ခြေ တက်တယ်။ ပိုဖန်တီးမှုရှိ / မမျှော်လင့်တဲ့ အဖြေ ရတယ်။

Usage guidelines:
သုံးသင့်ပုံ:

- Low temperature (near 0) = data extraction, factual tasks requiring consistency
- Temperature နိမ့် (၀ နား) = ဒေတာထုတ်ယူတာ၊ အချက်အလက်မှန်ရမယ့် အလုပ်၊ အဖြေ တည်ငြိမ်ချင်တာ

- High temperature (near 1) = creative tasks like brainstorming, writing, jokes, marketing
- Temperature မြင့် (၁ နား) = စိတ်ကူးထုတ်တာ၊ စာရေးတာ၊ ဟာသ၊ ကြော်ငြာ စတဲ့ ဖန်တီးမှုအလုပ်

Implementation: Add temperature parameter to model API calls. Higher values don't guarantee different outputs, just increase probability of variation.
လုပ်ပုံ: API ခေါ်တဲ့အခါ `temperature` parameter ထည့်ပါ။ တန်ဖိုးမြင့်ရုံနဲ့ အဖြေ မတူမယ်လို့ အာမခံ မရဘူး။ ကွာနိုင်ခြေ ပိုများတာပဲ။

Key insight: Temperature directly manipulates the probability distribution of next token selection, making high-probability tokens more/less dominant in the selection process.
အဓိက နားလည်ချက်: Temperature က နောက် token ရွေးတဲ့ ဖြစ်နိုင်ခြေ ဖြန့်ဖြူးမှုကို တိုက်ရိုက် ပြောင်းတယ်။ ဖြစ်နိုင်ခြေမြင့်တဲ့ token တွေ ပိုလွှမ်းမိုးလာတာ / လျော့လာတာ ဖြစ်တယ်။
</note>

<note title="Response Streaming">
Response Streaming
အဖြေကို အပိုင်းလိုက် စီးထုတ်ခြင်း
Streaming = စာအပြည့် မစောင့်ဘဲ၊ ထွက်လာသလို အပိုင်းလိုက် ပြတာ။

Response Streaming = technique to display AI responses chunk-by-chunk as they're generated instead of waiting for complete response.
Response Streaming = AI အဖြေအပြည့် မစောင့်ဘဲ၊ ထုတ်နေစဉ် အပိုင်းလေးတွေ အလိုက် ပြတဲ့ နည်း။

Problem solved: AI responses can take 10-30 seconds. Users expect immediate feedback, not just spinners.
ဖြေရှင်းတဲ့ ပြဿနာ: AI အဖြေက ၁၀-၃၀ စက္ကန့် ကြာနိုင်တယ်။ User တွေက စောင့်နေတဲ့ အကွက်လေးပဲ မဟုတ်ဘဲ၊ ချက်ချင်း တုံ့ပြန်မှု မျှော်တယ်။

How it works:
ဘယ်လို အလုပ်လုပ်လဲ:

1. Server sends user message to Claude
1. Server က user message ကို Claude ဆီ ပို့တယ်

2. Claude immediately sends initial response (no text, just acknowledgment)
2. Claude က ချက်ချင်း ပထမအကြောင်းပြန်တယ် (စာမပါသေး၊ လက်ခံကြောင်းပဲ)

3. Stream of events follows, each containing text chunks
3. နောက်က event တွေ စီးလာတယ်။ တစ်ခုချင်းမှာ စာအပိုင်းလေးတွေ ပါတယ်

4. Server forwards chunks to frontend for real-time display
4. Server က အပိုင်းလေးတွေကို frontend ဆီ ပို့ပြီး အချိန်နဲ့တပြေးညီ ပြတယ်

Event types:
Event အမျိုးအစားများ:

- message_start = initial acknowledgment
- message_start = ပထမဆုံး လက်ခံကြောင်း

- content_block_start = text generation begins
- content_block_start = စာစထုတ်ပြီ

- content_block_delta = contains actual text chunks (most important)
- content_block_delta = တကယ့် စာအပိုင်းလေးတွေ ပါတယ် (အရေးအကြီးဆုံး)

- content_block_stop/message_stop = generation complete
- content_block_stop / message_stop = စာထုတ်တာ ပြီးပြီ

Implementation:
လုပ်ပုံ:

Basic: client.messages.create(stream=True) returns event iterator
အခြေခံ: `client.messages.create(stream=True)` က event တွေကို တစ်ခုချင်း ပြန်ပေးတယ်

Simplified: client.messages.stream() with text_stream property extracts just text
ပိုလွယ်: `client.messages.stream()` ရဲ့ `text_stream` က စာသားပဲ ထုတ်ပေးတယ်

Final message: stream.get_final_message() assembles all chunks for storage
နောက်ဆုံး message: `stream.get_final_message()` က အပိုင်းအားလုံး ပေါင်းပြီး သိမ်းဖို့ အဆင်သင့် လုပ်တယ်

Key benefits: Better UX through immediate response visibility, complete message capture for database storage.
အဓိက အကျိုး: User ချက်ချင်း မြင်ရလို့ သုံးရတာ ပိုကောင်းတယ်။ Message အပြည့်ကို database ထဲ သိမ်းလို့ရတယ်။
</note>

<note title="Controlling Model Output">
Controlling Model Output
Model အဖြေကို ထိန်းချုပ်ခြင်း

Controlling Model Output = Two key techniques beyond prompt modification
Model အဖြေ ထိန်းချုပ်ခြင်း = prompt ပြင်တာအပြင် အဓိက နည်း ၂ ခု ရှိတယ်။

Pre-filling Assistant Messages = Manually adding assistant message at end of conversation to steer response direction
Assistant Message ကြိုဖြည့်ခြင်း = စကားပြောအဆုံးမှာ assistant message ကို ကိုယ်တိုင် ထည့်ပြီး၊ အဖြေသွားမယ့် ဦးတည်ရာကို လှည့်ပေးတာ။

How it works:
ဘယ်လို အလုပ်လုပ်လဲ:

- Assemble messages list with user prompt + manual assistant message
- user prompt + ကိုယ်ထည့်တဲ့ assistant message နဲ့ messages စာရင်း စုပါ

- Claude sees assistant message as already authored content
- Claude က အဲဒီ assistant message ကို ပြီးသား ရေးထားတဲ့စာ လို့ မြင်တယ်

- Claude continues response from exact end of pre-filled text
- Claude က ကြိုဖြည့်ထားတဲ့ စာအဆုံးကနေ တိတိကျကျ ဆက်ရေးတယ်

- Response gets steered toward pre-filled direction
- အဖြေက ကြိုဖြည့်ထားတဲ့ ဦးတည်ရာဆီ လှည့်သွားတယ်

Key point: Claude continues from exact endpoint of pre-fill, not complete sentences. Must stitch together pre-fill + generated response.
အရေးကြီးချက်: Claude က ကြိုဖြည့်စာရဲ့ အဆုံးမှတ်ကနေ ဆက်တယ်။ စာကြောင်းပြည့်အောင် မဆက်ဘူး။ ကြိုဖြည့်စာ + ထွက်လာတဲ့အဖြေ ကို ကိုယ်တိုင် ပေါင်းရမယ်။

Example: Pre-fill "Coffee is better because" → Claude continues with justification for coffee
ဥပမာ: `"Coffee is better because"` ကြိုဖြည့် → Claude က ကော်ဖီ ပိုကောင်းတဲ့ အကြောင်း ဆက်ပြောတယ်

Stop Sequences = Force Claude to halt generation when specific string appears
Stop Sequences = သတ်မှတ်စာသား ပေါ်လာရင် Claude ကို အတင်း ရပ်ခိုင်းတာ

How it works:
ဘယ်လို အလုပ်လုပ်လဲ:

- Provide stop sequence string in chat function
- chat function ထဲမှာ ရပ်ခိုင်းမယ့် စာသား ပေးပါ

- When Claude generates that exact string, response immediately stops
- Claude က အဲဒီစာသား တိတိကျကျ ထုတ်လိုက်ရင် အဖြေ ချက်ချင်း ရပ်တယ်

- Generated stop sequence text not included in final output
- ရပ်ခိုင်းတဲ့ စာသားကို နောက်ဆုံးအဖြေထဲ မထည့်ဘူး

Example: Prompt "count 1 to 10" + stop sequence "five" → Output stops at "four, " (five not included)
ဥပမာ: `"count 1 to 10"` + stop sequence `"five"` → `"four, "` မှာ ရပ်တယ် (`five` မပါ)

Refinement: Stop sequence ", five" → Clean output "one, two, three, four"
ပိုသေချာအောင်: stop sequence `", five"` → သန့်တဲ့အဖြေ `"one, two, three, four"`

Both techniques provide precise control over response direction and length without changing core prompts.
ဒီနည်း ၂ ခုစလုံးက အဓိက prompt ကို မပြောင်းဘဲ၊ အဖြေ ဦးတည်ရာနဲ့ အရှည်ကို တိတိကျကျ ထိန်းလို့ရတယ်။
</note>

<note title="Structured Data">
Structured Data
ဖွဲ့စည်းပုံရှိတဲ့ ဒေတာ
Structured data = JSON, ကုဒ်၊ စာရင်း စသဖြင့် ပုံစံတကျ ဒေတာ။

Structured Data Generation = technique using assistant message prefilling + stop sequences to get raw output without Claude's natural explanatory headers/footers.
Structured Data ထုတ်ခြင်း = assistant message ကြိုဖြည့် + stop sequence သုံးပြီး၊ Claude ရဲ့ ရှင်းလင်းချက် ခေါင်းစဉ်/အဆုံးသတ် မပါဘဲ၊ ကုန်ကြမ်း အဖြေပဲ ရအောင် လုပ်တဲ့ နည်း။

Problem = Claude automatically adds markdown formatting, headers, commentary when generating JSON/code/structured content. Users often want just the raw data for copy/paste functionality.
ပြဿနာ = Claude က JSON / ကုဒ် / ဖွဲ့စည်းပုံရှိတဲ့ အကြောင်းအရာ ထုတ်တဲ့အခါ markdown ပုံစံ၊ ခေါင်းစဉ်၊ ရှင်းလင်းချက်တွေ အလိုအလျောက် ထည့်တယ်။ User တွေက ကူးယူဖို့ ကုန်ကြမ်းဒေတာပဲ လိုတာ များတယ်။

Solution Pattern:
ဖြေရှင်းပုံ:

1. User message = request for structured data
1. User message = ဖွဲ့စည်းပုံရှိတဲ့ ဒေတာ တောင်းတယ်

2. Assistant message prefill = opening delimiter (e.g., "```json")
2. Assistant message ကြိုဖြည့် = စတဲ့ ပိုင်းခြားသင်္ကေတ (ဥပမာ `"```json"`)

3. Stop sequence = closing delimiter (e.g., "```")
3. Stop sequence = ပိတ်တဲ့ ပိုင်းခြားသင်္ကေတ (ဥပမာ `"```"`)

How it works = Claude sees prefilled message, assumes it already started response, generates only the requested content, stops when hitting delimiter.
ဘယ်လို အလုပ်လုပ်လဲ = Claude က ကြိုဖြည့်စာကို မြင်တယ်၊ အဖြေ စပြီးသား လို့ ယူဆတယ်၊ တောင်းထားတဲ့ အကြောင်းအရာပဲ ထုတ်တယ်၊ ပိုင်းခြားသင်္ကေတ တွေ့ရင် ရပ်တယ်။

Result = Raw structured data output with no extra formatting or commentary.
ရလဒ် = ပုံစံအပို / ရှင်းလင်းချက် မပါတဲ့ ကုန်ကြမ်း ဖွဲ့စည်းပုံဒေတာ။

Application = Works for any structured data type (JSON, Python code, lists, etc.), not just JSON. Use whenever you need clean, parseable output without explanatory text.
သုံးနိုင်တာ = JSON သက်သက် မဟုတ်။ Python ကုဒ်၊ စာရင်း စတဲ့ ဖွဲ့စည်းပုံရှိတာ အားလုံးမှာ ရတယ်။ ရှင်းလင်းချက်မပါတဲ့ သန့်တဲ့ အဖြေ လိုတိုင်း သုံးပါ။

Key benefit = Output can be directly used/copied without manual selection or parsing of unwanted text.
အဓိက အကျိုး = မလိုတဲ့စာ ဖယ်စရာမလိုဘဲ၊ အဖြေကို တိုက်ရိုက် သုံးလို့ / ကူးလို့ ရတယ်။
</note>

<note title="Prompt Evaluation">
Prompt Evaluation
Prompt စစ်ဆေးအကဲဖြတ်ခြင်း
Prompt = Claude ဆီ ပို့တဲ့ ညွှန်ကြားစာ။ Evaluation = ကောင်းမကောင်း တိုင်းတာခြင်း။

Prompt Engineering = techniques for writing/editing prompts to help Claude understand requests and desired responses.
Prompt Engineering = Claude က တောင်းဆိုချက်နဲ့ လိုချင်တဲ့ အဖြေကို နားလည်အောင် prompt ရေး/ပြင်တဲ့ နည်းများ။

Prompt Evaluation = automated testing of prompts using objective metrics to measure effectiveness.
Prompt Evaluation = prompt တွေကို အလိုအလျောက် စမ်းပြီး၊ ဘက်မလိုက်တဲ့ မှတ်ချက် (metric) နဲ့ ထိရောက်မှု တိုင်းတာခြင်း။

Three paths after writing a prompt:
Prompt ရေးပြီးရင် လမ်း ၃ ခု ရှိတယ်။

1. Test once/twice, deploy to production (trap)
1. တစ်နှစ်ခါ စမ်းပြီး production (တကယ့်အသုံး) ထဲ တင်လိုက်တာ (ထောင်ချောက်)

2. Test with custom inputs, minor tweaks for corner cases (trap)
2. ကိုယ်လုပ်တဲ့ input နဲ့ စမ်း၊ ထူးခြားဖြစ်ရပ်လေးတွေအတွက် နည်းနည်းပဲ ပြင်တာ (ထောင်ချောက်)

3. Run through evaluation pipeline for objective scoring (recommended)
3. အကဲဖြတ် pipeline ထဲ ဖြတ်ပြီး ဘက်မလိုက် မှတ်ချက်ယူတာ (အကြံပြုချက်)

Key takeaway: Engineers commonly under-test prompts. Use evaluation pipelines to get objective performance scores before iterating and deploying prompts.
အဓိက မှတ်စရာ: Engineer တွေက prompt ကို မလုံလောက်အောင်ပဲ စမ်းတတ်တယ်။ Prompt ပြင်ပြီး မတင်ခင်၊ evaluation pipeline နဲ့ ဘက်မလိုက် စွမ်းရည်မှတ်ချက် ယူပါ။
</note>

<note title="A Typical Eval Workflow">
A Typical Eval Workflow
ပုံမှန် Eval လုပ်ငန်းစဉ်
Eval = prompt ကောင်းမကောင်း စမ်းပြီး မှတ်ချက်ပေးတာ။

Typical Eval Workflow = 6-step iterative process for prompt improvement
ပုံမှန် Eval လုပ်ငန်းစဉ် = prompt ပိုကောင်းအောင် အဆင့် ၆ ဆင့် ထပ်ခါထပ်ခါ လုပ်တာ။

Step 1: Write initial prompt draft - create baseline prompt to optimize
အဆင့် ၁: ပထမ prompt မူကြမ်း ရေးပါ။ ဒီကနေ စပြီး ပိုကောင်းအောင် လုပ်မယ်။

Step 2: Create evaluation dataset - collection of test inputs (can be 3 examples or thousands, hand-written or LLM-generated)
အဆင့် ၂: စမ်းမယ့် dataset လုပ်ပါ။ စမ်းသုံး input တွေ စုပါ။ ဥပမာ ၃ ခုလည်း ရတယ်၊ ထောင်ချီလည်း ရတယ်။ လက်ရေးလည်း ရတယ်၊ LLM က ထုတ်လည်း ရတယ်။

Step 3: Generate prompt variations - interpolate each dataset input into prompt template
အဆင့် ၃: Prompt ပုံစံထဲကို dataset က input တစ်ခုချင်းစီ ထည့်ပြီး prompt အမျိုးမျိုး ဖြစ်အောင် လုပ်ပါ။

Step 4: Get LLM responses - feed each prompt variation to Claude, collect outputs
အဆင့် ၄: Prompt အမျိုးမျိုးကို Claude ဆီ ပို့ပြီး အဖြေတွေ စုပါ။

Step 5: Grade responses - use grader system to score each response (e.g. 1-10 scale), average scores for overall prompt performance
အဆင့် ၅: အဖြေတစ်ခုချင်းကို မှတ်ချက်ပေးပါ (ဥပမာ ၁-၁၀)။ ပျမ်းမျှမှတ်နဲ့ prompt တစ်ခုလုံး ဘယ်လောက်ကောင်းလဲ ကြည့်ပါ။

Step 6: Iterate - modify prompt based on scores, repeat entire process, compare versions
အဆင့် ၆: မှတ်ချက်ကြည့်ပြီး prompt ပြင်ပါ။ လုပ်ငန်းစဉ် အပြည့် ထပ်လုပ်ပါ။ ဗားရှင်းတွေ နှိုင်းယှဉ်ပါ။

Key points: No standard methodology exists. Many open-source/paid tools available. Can start simple with custom implementation. Grading complexity varies. Objective scoring enables systematic prompt improvement through A/B comparison.
အရေးကြီးချက်များ: ပုံသေနည်း တစ်ခုတည်း မရှိဘူး။ အခမဲ့ / အခကြေးငွေ ကိရိယာ များတယ်။ ကိုယ်တိုင် ရိုးရိုးစရေးလို့ရတယ်။ မှတ်ချက်ပေးပုံ ခက်တာ/လွယ်တာ ကွာတယ်။ ဘက်မလိုက် မှတ်ချက်ရှိရင် A/B နှိုင်းယှဉ်ပြီး prompt ကို စနစ်တကျ ပိုကောင်းအောင် လုပ်လို့ရတယ်။
</note>

<note title="Generating Test Datasets">
Generating Test Datasets
စမ်းသပ် Dataset ဖန်တီးခြင်း
Dataset = စမ်းသုံး ဥပမာတွေ စုထားတာ။

Custom prompt evaluation workflow = build prompt + generate test dataset + evaluate performance
ကိုယ်ပိုင် prompt အကဲဖြတ် လုပ်ငန်းစဉ် = prompt ရေး + စမ်းသပ် dataset ထုတ် + စွမ်းရည် တိုင်း

Goal = AWS code assistance prompt that outputs only Python, JSON config, or regex without explanations
ပန်းတိုင် = AWS ကုဒ်အကူအညီ prompt။ ရှင်းလင်းချက် မပါဘဲ Python, JSON config, သို့မဟုတ် regex ပဲ ထုတ်ရမယ်။

Dataset generation approaches = manual assembly or automated with Claude (use faster models like Haiku for generation)
Dataset ထုတ်ပုံ = ကိုယ်တိုင် စုတာ၊ သို့မဟုတ် Claude နဲ့ အလိုအလျောက် ထုတ်တာ (ထုတ်ဖို့ Haiku လို မြန်တဲ့ model သုံးပါ)

Dataset structure = array of JSON objects with task property describing user requests
Dataset ဖွဲ့စည်းပုံ = JSON object စာရင်း။ တစ်ခုချင်းမှာ user တောင်းဆိုချက် ဖော်ပြတဲ့ `task` ရှိတယ်။

Generation process = prompt Claude to create test cases → use pre-filling with assistant message "```json" → set stop sequence "```" → parse response as JSON → save to file
ထုတ်ပုံ လုပ်ငန်းစဉ် = Claude ကို စမ်းသပ်မှုတွေ လုပ်ခိုင်း → assistant message `"```json"` ကြိုဖြည့် → stop sequence `"```"` ထား → အဖြေကို JSON အဖြစ် ဖတ် → ဖိုင်သိမ်း

Key implementation = generate_dataset() function that sends prompt to Claude, gets structured JSON response of test tasks, saves to dataset.json file for later evaluation use
အဓိက လုပ်ပုံ = `generate_dataset()` function က prompt ကို Claude ဆီ ပို့တယ်၊ စမ်းသပ်အလုပ်တွေရဲ့ JSON အဖြေယူတယ်၊ နောက်မှ အကဲဖြတ်ဖို့ `dataset.json` မှာ သိမ်းတယ်။

Test dataset enables systematic evaluation by running prompt against multiple input scenarios to measure performance consistency.
စမ်းသပ် dataset ရှိရင် prompt ကို input အမျိုးမျိုးနဲ့ စမ်းပြီး၊ စွမ်းရည် တည်ငြိမ်မှုကို စနစ်တကျ တိုင်းလို့ရတယ်။
</note>

<note title="Running the Eval">
Running the Eval
Eval ကို ဘယ်လို ခိုင်းမလဲ

Eval execution process = merging test cases with prompts, running through LLM, and grading outputs.
Eval ခိုင်းပုံ = စမ်းသပ်မှုတွေကို prompt နဲ့ ပေါင်း၊ LLM ထဲ ဖြတ်၊ အဖြေတွေ မှတ်ချက်ပေး။

Test case = individual record from dataset (JSON object).
Test case = dataset ထဲက တစ်ခုချင်း မှတ်တမ်း (JSON object)။

Three core functions:
အဓိက function ၃ ခု:

- run_prompt = merges test case with prompt, sends to Claude, returns output
- `run_prompt` = test case ကို prompt နဲ့ ပေါင်း၊ Claude ဆီ ပို့၊ အဖြေ ပြန်ပေး

- run_test_case = calls run_prompt, grades result, returns summary dictionary
- `run_test_case` = `run_prompt` ခေါ်၊ အဖြေ မှတ်ချက်ပေး၊ အနှစ်ချုပ် dictionary ပြန်ပေး

- run_eval = loops through dataset, calls run_test_case for each, assembles results
- `run_eval` = dataset တစ်ခုချင်း လှည့်၊ `run_test_case` ခေါ်၊ ရလဒ်တွေ စု

Basic prompt structure = "Please solve the following task: [test_case_task]" (v1 starting point).
အခြေခံ prompt ဖွဲ့စည်းပုံ = `"Please solve the following task: [test_case_task]"` (v1 စမှတ်)။

Current limitations = no output formatting instructions, hardcoded scoring (score=10), verbose Claude responses.
အခု အားနည်းချက် = အဖြေပုံစံ ညွှန်ကြားချက် မရှိ၊ မှတ်ချက်ကို ကုဒ်ထဲ ပုံသေ ထား (`score=10`)၊ Claude အဖြေတွေ စကားများတယ်။

Runtime = ~31 seconds with Haiku model for full dataset execution.
ကြာချိန် = dataset အပြည့်ကို Haiku နဲ့ ခိုင်းရင် ၃၁ စက္ကန့်ခန့်။

Output format = array of objects containing Claude output, original test case, and score.
အထွက် ပုံစံ = Claude အဖြေ၊ မူရင်း test case၊ မှတ်ချက် ပါတဲ့ object စာရင်း။

Next step = implement proper grading system to replace hardcoded scores.
နောက်အဆင့် = ပုံသေမှတ်ချက်အစား တကယ့် မှတ်ချက်ပေးစနစ် ရေးပါ။

Eval pipeline core = dataset + prompt + LLM + grader, with minimal code complexity.
Eval pipeline အူတိုင် = dataset + prompt + LLM + grader။ ကုဒ် ရှုပ်အောင် မလုပ်ပါနဲ့။
</note>

<note title="Model Based Grading">
Model Based Grading
Model နဲ့ မှတ်ချက်ပေးခြင်း
Grader = အဖြေကောင်းမကောင်း မှတ်ချက်ပေးတဲ့ စနစ်။

Model Based Grading = evaluation system that takes model outputs and assigns objective scores (typically 1-10 scale, 10 = highest quality)
Model Based Grading = model အဖြေတွေယူပြီး ဘက်မလိုက် မှတ်ချက်ပေးတဲ့ စနစ်။ အများအားဖြင့် ၁-၁၀။ ၁၀ = အကောင်းဆုံး။

Three grader types:
Grader အမျိုးအစား ၃ ခု:

- Code graders = programmatic checks (length, word presence, syntax validation, readability scores)
- Code grader = ကုဒ်နဲ့ စစ်တာ (အရှည်၊ စကားလုံး ပါ/မပါ၊ syntax မှန်/မမှန်၊ ဖတ်လွယ်မှု)

- Model graders = additional API call to evaluate original model output, highly flexible for quality/instruction-following assessment
- Model grader = မူရင်းအဖြေကို နောက် API ခေါ်ပြီး အကဲဖြတ်တာ။ အရည်အသွေး / ညွှန်ကြားချက် လိုက်နာမှု စစ်ဖို့ ပျော့ပြောင်းတယ်။

- Human graders = person evaluates responses, most flexible but time-consuming and tedious
- Human grader = လူက အဖြေကြည့်တာ။ အပျော့ပြောင်းဆုံး၊ ဒါပေမဲ့ အချိန်ကုန်ပြီး ပင်ပန်းတယ်။

Key requirements: Must return objective signal (usually numerical score). Define evaluation criteria upfront.
မဖြစ်မနေလိုအပ်ချက်: ဘက်မလိုက် အချက်ပြမှု ပြန်ပေးရမယ် (များသောအားဖြင့် ဂဏန်းမှတ်)။ အကဲဖြတ် စံနှုန်းကို ကြိုသတ်မှတ်ပါ။

Implementation pattern for model graders:
Model grader လုပ်ပုံ:

- Create detailed prompt requesting strengths/weaknesses/reasoning/score (not just score alone to avoid default middling scores)
- အားသာချက် / အားနည်းချက် / အကြောင်းပြချက် / မှတ်ချက် တောင်းတဲ့ အသေးစိတ် prompt ရေးပါ။ မှတ်ချက်ပဲ တောင်းရင် အလယ်အလတ်မှတ်ပဲ ပေးတတ်တယ်။

- Use JSON response format with pre-filled assistant message and stop sequences
- JSON အဖြေပုံစံ သုံးပါ။ assistant message ကြိုဖြည့် + stop sequence သုံးပါ။

- Parse returned JSON for score and reasoning
- ပြန်လာတဲ့ JSON ကနေ မှတ်ချက်နဲ့ အကြောင်းပြချက် ဖတ်ပါ

- Calculate average scores across test cases for final metric
- test case တွေရဲ့ ပျမ်းမျှမှတ်ကို နောက်ဆုံး တိုင်းတာချက်အဖြစ် တွက်ပါ

Model graders offer high flexibility but may be inconsistent. Still provides objective baseline for prompt optimization.
Model grader က ပျော့ပြောင်းတယ်၊ ဒါပေမဲ့ တစ်ခါနဲ့တစ်ခါ မတူနိုင်ဘူး။ ဒါတောင် prompt ပိုကောင်းအောင် လုပ်ဖို့ ဘက်မလိုက် အခြေခံမှတ် ရသေးတယ်။
</note>

<note title="Code Based Grading">
Code Based Grading
ကုဒ်နဲ့ မှတ်ချက်ပေးခြင်း

Code Based Grading = automated validation system for LLM outputs containing code, JSON, or regex
Code Based Grading = LLM က ထုတ်တဲ့ ကုဒ်၊ JSON၊ regex ကို အလိုအလျောက် စစ်တဲ့ စနစ်။

Core Implementation:
အဓိက လုပ်ပုံ:

- validate_json() = attempts JSON parsing, returns 10 if valid, 0 if error
- `validate_json()` = JSON ဖတ်ကြည့်တယ်။ မှန်ရင် ၁၀၊ မှားရင် ၀

- validate_python() = attempts AST parsing, returns 10 if valid, 0 if error
- `validate_python()` = Python AST နဲ့ စစ်တယ်။ မှန်ရင် ၁၀၊ မှားရင် ၀

- validate_regex() = attempts regex compilation, returns 10 if valid, 0 if error
- `validate_regex()` = regex တွဲကြည့်တယ်။ မှန်ရင် ၁၀၊ မှားရင် ၀

Dataset Requirements:
Dataset လိုအပ်ချက်:

- Must include "format" key specifying expected output type (JSON/Python/RegEx)
- မျှော်လင့်တဲ့ အထွက်အမျိုးအစား ပြတဲ့ `"format"` key ပါရမယ် (JSON / Python / RegEx)

- Updated via prompt template modification for automated dataset generation
- အလိုအလျောက် dataset ထုတ်ဖို့ prompt ပုံစံကို ပြင်ပြီး ထည့်ထားတယ်

Prompt Engineering:
Prompt ရေးပုံ:

- Instruct model to respond only with raw code/JSON/regex
- model ကို ကုန်ကြမ်း ကုဒ် / JSON / regex ပဲ ပြန်ခိုင်းပါ

- No comments, explanations, or commentary
- မှတ်ချက်၊ ရှင်းလင်းချက် မထည့်ပါနဲ့

- Use pre-filled Assistant message with ```code``` blocks
- Assistant message ကို code block နဲ့ ကြိုဖြည့်ပါ

- Add stop sequences to extract clean output
- သန့်တဲ့အဖြေရဖို့ stop sequence ထည့်ပါ

Scoring System:
မှတ်ချက်ပေးစနစ်:

- Final score = (model_score + syntax_score) / 2
- နောက်ဆုံးမှတ် = (model_score + syntax_score) / 2

- Combines semantic evaluation with syntax validation
- အဓိပ္ပာယ်အရ ကောင်းမကောင်း + ကုဒ်မှန်မမှန် နှစ်ခု ပေါင်းတယ်

- Enables measurement of both correctness and technical validity
- မှန်ကန်မှုနဲ့ နည်းပညာအရ တရားဝင်မှု နှစ်ခုလုံး တိုင်းလို့ရတယ်

Key Limitation = requires known expected format for proper validator selection
အဓိက ကန့်သတ် = ဘယ် validator သုံးမလဲ သိအောင်၊ မျှော်လင့်တဲ့ ပုံစံကို ကြိုသိရမယ်
</note>

<note title="Prompt Engineering">
Prompt Engineering
Prompt အင်ဂျင်နီယာ

Prompt Engineering = improving prompts to get more reliable, higher-quality outputs from language models.
Prompt Engineering = language model က ပိုယုံကြည်ရ၊ ပိုကောင်းတဲ့ အဖြေထုတ်အောင် prompt တွေ ပိုကောင်းအောင် လုပ်တာ။

Module Structure: Start with initial poor prompt → Apply prompt engineering techniques step-by-step → Evaluate improvements after each technique → Observe performance gains over time.
သင်ခန်းစာ ဖွဲ့စည်းပုံ: အားနည်းတဲ့ ပထမ prompt က စ → နည်းတွေကို အဆင့်ဆင့် သုံး → နည်းတစ်ခုပြီးတိုင်း တိုးတက်မှု တိုင်း → အချိန်ကြာလာတာနဲ့ စွမ်းရည် တက်လာတာ ကြည့်

Example Goal: Generate one-day meal plan for athletes based on height, weight, physical goal, dietary restrictions.
ဥပမာ ပန်းတိုင်: အားကစားသမားအတွက် တစ်ရက်စာ ထမင်းစားအစီအစဉ် ထုတ်ပါ။ အရပ်၊ ကိုယ်အလေးချိန်၊ ကိုယ်ကာယပန်းတိုင်၊ အစားအသောက် ကန့်သတ်တွေအရ။

Technical Setup:
နည်းပညာ ပြင်ဆင်မှု:

- Updated eval pipeline with flexible prompt evaluator class
- ပျော့ပြောင်းတဲ့ prompt evaluator class ပါတဲ့ eval pipeline အသစ်

- Supports concurrency (adjust max_concurrent_tasks based on rate limits)
- တစ်ပြိုင်နက် လုပ်တာ ထောက်ပံ့တယ် (`max_concurrent_tasks` ကို rate limit အရ ချိန်ပါ)

- generate_dataset() method creates test cases with specified inputs
- `generate_dataset()` က သတ်မှတ် input တွေနဲ့ test case တွေ လုပ်တယ်

- run_prompt() function processes each test case individually
- `run_prompt()` က test case တစ်ခုချင်း စီမံတယ်

Key Components:
အဓိက အစိတ်အပိုင်းများ:

- prompt_input_spec = dictionary defining required prompt inputs
- `prompt_input_spec` = prompt ထဲ လိုအပ်တဲ့ input တွေ ပြတဲ့ dictionary

- extra_criteria = additional validation requirements for model grading
- `extra_criteria` = model မှတ်ချက်ပေးဖို့ အပို စစ်ဆေးချက်များ

- output.html = formatted evaluation report showing test case results and scores
- `output.html` = test case ရလဒ်နဲ့ မှတ်ချက်တွေ ပြတဲ့ ပုံစံချ အစီရင်ခံစာ

Process: Write initial prompt → Interpolate test case inputs → Run evaluation → Apply engineering techniques → Re-evaluate → Repeat until satisfactory performance.
လုပ်ငန်းစဉ်: ပထမ prompt ရေး → test case input တွေ ထည့် → အကဲဖြတ် → နည်းတွေ သုံး → ပြန်အကဲဖြတ် → ကျေနပ်တဲ့အထိ ထပ်လုပ်

Initial Results: Expect poor scores (example: 2.32) with basic prompts, especially when using less capable models. Scores improve as techniques are applied.
ပထမရလဒ်: အခြေခံ prompt နဲ့ဆို မှတ်နည်းမယ်လို့ မျှော်ပါ (ဥပမာ ၂.၃၂)။ အထူးသဖြင့် အားနည်းတဲ့ model နဲ့။ နည်းတွေ သုံးလာရင် မှတ် တက်လာတယ်။
</note>

<note title="Being Clear and Direct">
Being Clear and Direct
ရှင်းရှင်းလင်းလင်း၊ တိုက်ရိုက် ပြောပါ

Being Clear and Direct = Use simple, direct language with action verbs in the first line of prompts to specify the exact task.
ရှင်းရှင်းလင်းလင်း၊ တိုက်ရိုက် = prompt ရဲ့ ပထမစာကြောင်းမှာ ရိုးရိုး၊ တိုက်ရိုက် စကား + လုပ်ဆောင်ချက်ကြိယာ သုံးပြီး၊ တိတိကျကျ ဘာလုပ်ရမလဲ ပြောပါ။

First line importance = Most critical part of prompt that sets the foundation for AI response.
ပထမစာကြောင်း အရေးကြီးပုံ = prompt ရဲ့ အရေးအကြီးဆုံး အပိုင်း။ AI အဖြေရဲ့ အခြေခံ ဖြစ်တယ်။

Structure = Action verb + clear task description + output specifications.
ဖွဲ့စည်းပုံ = လုပ်ဆောင်ချက်ကြိယာ + ရှင်းတဲ့ အလုပ်ဖော်ပြချက် + အဖြေ ဘယ်လိုဖြစ်ရမလဲ။

Examples:
ဥပမာများ:

- "Write three paragraphs about how solar panels work"
- "Write three paragraphs about how solar panels work" (ဆိုလာပြား ဘယ်လိုအလုပ်လုပ်လဲ စာပိုဒ် ၃ ပိုဒ် ရေးပါ)

- "Identify three countries that use geothermal energy and for each include generation stats"
- "Identify three countries that use geothermal energy and for each include generation stats" (မြေအောက်အပူစွမ်းအင် သုံးတဲ့ နိုင်ငံ ၃ ခု ရှာ၊ တစ်နိုင်ငံချင်း ထုတ်လုပ်မှု ကိန်းဂဏန်း ထည့်ပါ)

- "Generate a one day meal plan for an athlete that meets their dietary restrictions"
- "Generate a one day meal plan for an athlete that meets their dietary restrictions" (အားကစားသမားအတွက် အစားကန့်သတ်နဲ့ ကိုက်တဲ့ တစ်ရက်စာ ထမင်းစားအစီအစဉ် ထုတ်ပါ)

Key components = Action verb at start + direct task statement + expected output details.
အဓိက အစိတ်အပိုင်း = အစမှာ လုပ်ဆောင်ချက်ကြိယာ + တိုက်ရိုက် အလုပ်ပြောချက် + မျှော်လင့်တဲ့ အဖြေ အသေးစိတ်

Result = Improved prompt performance (example showed score increase from 2.32 to 3.92).
ရလဒ် = Prompt စွမ်းရည် တက်လာတယ် (ဥပမာ မှတ် ၂.၃၂ ကနေ ၃.၉၂)။
</note>

<note title="Being Specific">
Being Specific
တိတိကျကျ ပြောပါ

Being Specific = adding guidelines or steps to direct model output in particular direction
တိတိကျကျ ပြောခြင်း = လမ်းညွှန်ချက် သို့မဟုတ် အဆင့်တွေ ထည့်ပြီး၊ model အဖြေကို လိုရာဦးတည်ရာဆီ ပို့တာ

Two types of guidelines:
လမ်းညွှန်ချက် အမျိုးအစား ၂ ခု:

Type A (Attributes) = list qualities/attributes desired in output (length, structure, format)
အမျိုးအစား A (ဂုဏ်သတ္တိများ) = အဖြေမှာ လိုချင်တဲ့ ဂုဏ်သတ္တိတွေ စာရင်းပြုပါ (အရှည်၊ ဖွဲ့စည်းပုံ၊ ပုံစံ)

Type B (Steps) = provide specific steps for model to follow in reasoning process
အမျိုးအစား B (အဆင့်များ) = model စဉ်းစားတဲ့အခါ လိုက်နာရမယ့် တိကျတဲ့ အဆင့်တွေ ပေးပါ

Type A controls output characteristics. Type B controls how model arrives at answer.
အမျိုးအစား A က အဖြေရဲ့ ပုံသဏ္ဌာန်ကို ထိန်းတယ်။ အမျိုးအစား B က အဖြေရောက်ပုံကို ထိန်းတယ်။

Both techniques often combined in professional prompts.
ပရော်ဖက်ရှင်နယ် prompt တွေမှာ ဒီနည်း ၂ ခုကို မကြာခဏ ပေါင်းသုံးတယ်။

When to use:
ဘယ်တော့ သုံးမလဲ:

- Type A (attributes): recommended for almost all prompts
- အမျိုးအစား A (ဂုဏ်သတ္တိ): prompt နီးပါး အားလုံးမှာ သုံးသင့်တယ်

- Type B (steps): use for complex problems where you want model to consider broader perspective or additional viewpoints it might not naturally consider
- အမျိုးအစား B (အဆင့်): ခက်ခဲတဲ့ ပြဿနာမှာ၊ model က သူ့ဘာသာ မစဉ်းစားနိုင်တဲ့ ပိုကျယ်တဲ့ ရှုထောင့်တွေ ထည့်စဉ်းစားစေချင်ရင် သုံးပါ

Example improvement: meal planning prompt score jumped from 3.92 to 7.86 when guidelines added, demonstrating significant quality improvement through specificity.
တိုးတက်မှု ဥပမာ: ထမင်းစားအစီအစဉ် prompt မှာ လမ်းညွှန်ချက် ထည့်တော့ မှတ် ၃.၉၂ ကနေ ၇.၈၆ တက်သွားတယ်။ တိကျမှုက အရည်အသွေးကို သိသိသာသာ တိုးစေတယ်။
</note>

<note title="Structure with XML Tags">
Structure with XML Tags
XML Tag နဲ့ ဖွဲ့စည်းပုံချခြင်း
XML tag = `<sales_records>` လို ပိုင်းခြားတဲ့ အမှတ်အသား။

XML Tags for Prompt Structure = Using XML tags to organize and delineate different content sections within prompts to improve AI comprehension.
Prompt ဖွဲ့စည်းပုံအတွက် XML Tag = prompt ထဲက အပိုင်းတွေကို XML tag နဲ့ ခွဲခြား စုစည်းပြီး၊ AI ပိုနားလည်အောင် လုပ်တာ။

Purpose = When interpolating large amounts of content into prompts, XML tags help AI models distinguish between different types of information and understand text grouping.
ရည်ရွယ်ချက် = prompt ထဲ အကြောင်းအရာ အများကြီး ထည့်တဲ့အခါ၊ XML tag က ဘယ်စာက ဘယ်အမျိုးအစားလဲ၊ ဘယ်စာတွေ အုပ်စုတူလဲ ဆိုတာ AI ခွဲခြားကူညီတယ်။

Implementation = Wrap content sections in descriptive XML tags like <sales_records></sales_records> or <my_code></my_code> rather than dumping unstructured text.
လုပ်ပုံ = စာတွေကို ပုံစံမရှိ ပုံပုံထည့်မယ့်အစား `<sales_records></sales_records>` သို့မဟုတ် `<my_code></my_code>` လို နာမည်ရှင်းတဲ့ XML tag နဲ့ ပတ်ပါ။

Tag naming = Use descriptive, specific tag names (e.g., "sales_records" better than "data") to provide context about content nature.
Tag နာမည်ပေးပုံ = ရှင်းရှင်းလင်းလင်း၊ တိတိကျကျ နာမည်ပေးပါ။ `"data"` ထက် `"sales_records"` က ပိုကောင်းတယ်။ အကြောင်းအရာ ဘာလဲ ဆိုတာ ပိုသိရတယ်။

Example use case = Debugging prompt with mixed code and documentation becomes clearer when separated into <my_code> and <docs> tags.
သုံးပုံ ဥပမာ = ကုဒ်နဲ့ စာရွက်စာတမ်း ရောနေတဲ့ debug prompt ကို `<my_code>` နဲ့ `<docs>` ခွဲရင် ပိုရှင်းတယ်။

Benefits = Makes prompt structure obvious to AI, reduces confusion about content boundaries, improves output quality even for smaller content blocks.
အကျိုး = Prompt ဖွဲ့စည်းပုံကို AI ရှင်းရှင်းမြင်ရတယ်။ ဘယ်နေရာက စ/ဆုံးလဲ ရှုပ်တာ လျော့တယ်။ အပိုင်းသေးသေးတွေမှာတောင် အဖြေပိုကောင်းတယ်။

Application = Can wrap any interpolated content like <athlete_information> even when content is short, to clarify it's external input requiring consideration.
သုံးနိုင်တာ = `<athlete_information>` လို အပိုင်းတိုတိုကိုတောင် ပတ်လို့ရတယ်။ ဒါက ပြင်ပက ထည့်လာတဲ့ input၊ ထည့်စဉ်းစားရမယ် ဆိုတာ ရှင်းအောင်။
</note>

<note title="Providing Examples">
Providing Examples
ဥပမာ ပေးခြင်း

One-shot/Multi-shot prompting = providing examples in prompts to guide model behavior. One-shot = single example, multi-shot = multiple examples.
One-shot / Multi-shot prompting = prompt ထဲ ဥပမာထည့်ပြီး model အပြုအမူကို လမ်းညွှန်တာ။ One-shot = ဥပမာ ၁ ခု။ Multi-shot = ဥပမာ များစွာ။

Implementation: Structure examples with XML tags containing sample input and ideal output. Always wrap examples clearly to distinguish from actual prompt content.
လုပ်ပုံ: ဥပမာတွေကို XML tag နဲ့ ဖွဲ့ပါ။ နမူနာ input နဲ့ လိုချင်တဲ့ အဖြေ ထည့်ပါ။ တကယ့် prompt စာနဲ့ မရောအောင် ဥပမာကို ရှင်းရှင်း ပတ်ပါ။

Key applications:
အဓိက သုံးစရာများ:

- Corner case handling (sarcasm detection, edge scenarios)
- ထူးခြားဖြစ်ရပ် ကိုင်တွယ်ခြင်း (သရော်စာ ရှာတာ၊ အစွန်းရောက် အခြေအနေ)

- Complex output formatting (JSON structures, specific formats)
- ရှုပ်ထွေးတဲ့ အဖြေပုံစံ (JSON ဖွဲ့စည်းပုံ၊ သတ်မှတ်ပုံစံ)

- Clarifying expected response quality/style
- လိုချင်တဲ့ အဖြေ အရည်အသွေး / ပုံစံ ကို ရှင်းပြခြင်း

Best practices:
ကောင်းမွန်တဲ့ လုပ်နည်းများ:

- Add context for corner cases ("be especially careful with sarcasm")
- ထူးခြားဖြစ်ရပ်အတွက် အကြောင်းအရာ ထည့်ပါ ("sarcasm ကို အထူးသတိထားပါ")

- Include reasoning explaining why output is ideal
- ဒီအဖြေ ဘာကြောင့် ကောင်းလဲ ဆိုတဲ့ အကြောင်းပြချက် ထည့်ပါ

- Use highest-scoring examples from prompt evaluations as templates
- Prompt အကဲဖြတ်မှာ မှတ်အမြင့်ဆုံး ဥပမာတွေကို ပုံစံအဖြစ် သုံးပါ

- Place examples after main instructions/guidelines
- အဓိက ညွှန်ကြားချက် / လမ်းညွှန်တွေ နောက်မှာ ဥပမာ ထားပါ

Effectiveness boost: Combine examples with explanations of what makes them ideal to reinforce desired output characteristics.
ပိုထိရောက်အောင်: ဥပမာနဲ့အတူ ဘာကြောင့် ကောင်းလဲ ရှင်းပြပါ။ လိုချင်တဲ့ အဖြေဂုဏ်သတ္တိ ပိုခိုင်မာလာမယ်။
</note>

<note title="Introducing Tool Use">
Introducing Tool Use
Tool Use မိတ်ဆက်
Tool = Claude က ပြင်ပအချက်အလက် ယူဖို့ သုံးတဲ့ ကိရိယာ။

Tool use = method for Claude to access external information beyond training data.
Tool use = Claude က သင်ကြားထားတဲ့ ဒေတာအပြင် ပြင်ပအချက်အလက် ယူတဲ့ နည်း။

Default limitation: Claude only knows information from training data, lacks current/real-time information.
ပုံမှန် ကန့်သတ်: Claude က သင်ကြားထားတဲ့အချက်ပဲ သိတယ်။ ယခုလက်ရှိ / အချိန်နဲ့တပြေးညီ အချက် မသိဘူး။

Tool use flow:
Tool use စီးဆင်းမှု:

1. Send initial request to Claude + instructions for external data access
1. ပထမ တောင်းဆိုချက် + ပြင်ပဒေတာ ယူပုံ ညွှန်ကြားချက် ကို Claude ဆီ ပို့ပါ

2. Claude evaluates if external data needed, requests specific information
2. Claude က ပြင်ပဒေတာ လိုမလို စဉ်းစားပြီး၊ လိုချင်တဲ့ အချက်ကို တောင်းတယ်

3. Server runs code to fetch requested data from external sources
3. Server က ကုဒ်ခိုင်းပြီး ပြင်ပက အချက်အလက် ယူတယ်

4. Send follow-up request to Claude with retrieved data
4. ယူလာတဲ့ ဒေတာနဲ့ နောက်ဆက်တွဲ တောင်းဆိုချက် ကို Claude ဆီ ပို့ပါ

5. Claude generates final response using original prompt + external data
5. Claude က မူရင်း prompt + ပြင်ပဒေတာ သုံးပြီး နောက်ဆုံးအဖြေ ထုတ်တယ်

Weather example: User asks current weather → Claude requests weather data → Server calls weather API → Claude receives weather data → Claude provides informed weather response.
ရာသီဥတု ဥပမာ: User က ယခုရာသီဥတု မေး → Claude က ရာသီဥတုဒေတာ တောင်း → Server က weather API ခေါ် → Claude က ဒေတာရ → Claude က သိရှိချက်အရ ဖြေတယ်။

Key concept: Tools enable Claude to augment responses with live/current information by orchestrating external data retrieval between Claude's requests.
အဓိက အယူအဆ: Tool တွေက Claude တောင်းတဲ့ကြားမှာ ပြင်ပဒေတာ ယူပေးပြီး၊ ယခုလက်ရှိ အချက်နဲ့ အဖြေကို ဖြည့်ပေးတယ်။
</note>

<note title="Project Overview">
Project Overview
ပရောဂျက် အနှစ်ချုပ်

Goal = Teach Claude to set time-based reminders through tool implementation in Jupyter notebook
ပန်းတိုင် = Jupyter notebook ထဲမှာ tool ရေးပြီး၊ Claude ကို အချိန်အလိုက် သတိပေးချက် ထားတတ်အောင် သင်ပေးပါ

Target interaction = User: "Set reminder for doctor's appointment, week from Thursday" → Claude: "I will remind you at that point in time"
လိုချင်တဲ့ စကားပြောပုံ = User: "ကြာသပတေးနေ့ကနေ တစ်ပတ်ကြာရင် ဆရာဝန်ချိန်းအတွက် သတိပေးပါ" → Claude: "အဲဒီအချိန်မှာ သတိပေးမယ်"

Three core problems requiring tools:
Tool လိုအပ်တဲ့ အဓိက ပြဿနာ ၃ ခု:

1. Time knowledge gap = Claude knows current date but not exact time
1. အချိန်မသိခြင်း = Claude က ယနေ့ရက်စွဲ သိနိုင်တယ်၊ တိတိကျကျ နာရီ မသိဘူး

2. Time calculation errors = Claude sometimes miscalculates time-based addition (e.g., 379 days from January 13th, 1973)
2. အချိန်တွက်မှားခြင်း = Claude က ရက်ပေါင်းတွက်တာ တစ်ခါတလေ မှားတယ် (ဥပမာ ၁၉၇၃ ဇန်နဝါရီ ၁၃ ကနေ ၃၇၉ ရက်)

3. No reminder mechanism = Claude understands reminder concept but lacks implementation capability
3. သတိပေးစနစ် မရှိခြင်း = Claude က သတိပေးချက် ဆိုတာ နားလည်တယ်၊ ဒါပေမဲ့ တကယ် ထားလို့ မရဘူး

Three corresponding tools to build:
တည်ဆောက်ရမယ့် tool ၃ ခု:

1. Current datetime tool = Gets current date + time
1. ယခုရက်စွဲ-အချိန် tool = ယခု ရက်စွဲ + နာရီ ယူတယ်

2. Duration addition tool = Adds time duration to datetime (e.g., current date + 20 days)
2. ကြာချိန်ပေါင်း tool = ရက်စွဲ-အချိန်ပေါ် ကြာချိန် ပေါင်းတယ် (ဥပမာ ယနေ့ + ၂၀ ရက်)

3. Reminder setting tool = Actually sets the reminder
3. သတိပေးချက်ထား tool = တကယ် သတိပေးချက် ထားတယ်

Implementation approach = One tool at a time, building toward multi-tool coordination
လုပ်ပုံ = tool တစ်ခုချင်းစီ တည်ဆောက်ပြီး၊ နောက်မှ tool များစွာ ပူးပေါင်းအောင် လုပ်ပါ
</note>

<note title="Tool Functions">
Tool Functions
Tool Function များ
Function = ခေါ်သုံးလို့ရတဲ့ ကုဒ်အပိုင်း။

Tool Functions = Python functions executed automatically when Claude needs extra information to help users.
Tool Functions = Claude က user ကို ကူညီဖို့ အပိုအချက် လိုတဲ့အခါ အလိုအလျောက် အလုပ်လုပ်တဲ့ Python function များ။

Key characteristics:
အဓိက ဂုဏ်သတ္တိများ:

- Plain Python functions called by Claude when it determines additional data is needed
- Claude က အပိုဒေတာ လိုတယ်လို့ ဆုံးဖြတ်ရင် ခေါ်တဲ့ ရိုးရိုး Python function များ

- Must use descriptive function names and argument names
- Function နာမည်နဲ့ argument နာမည် ရှင်းရှင်းလင်းလင်း ပေးရမယ်

- Should validate inputs and raise errors with meaningful messages
- Input တွေ စစ်ပါ။ မှားရင် အဓိပ္ပာယ်ရှိတဲ့ error message ထုတ်ပါ

- Error messages are visible to Claude, allowing it to retry with corrected parameters
- Error message ကို Claude မြင်တယ်။ ပြင်ပြီး parameter နဲ့ ပြန်ကြိုးစားနိုင်တယ်

Best practices:
ကောင်းမွန်တဲ့ လုပ်နည်းများ:

1. Well-named functions and arguments
1. နာမည်ကောင်းတဲ့ function နဲ့ argument

2. Input validation with immediate error raising for invalid inputs
2. Input စစ်ပြီး၊ မမှန်ရင် ချက်ချင်း error ထုတ်ပါ

3. Meaningful error messages that guide correction
3. ပြင်ပုံ လမ်းညွှန်တဲ့ အဓိပ္ပာယ်ရှိ error message

Example implementation pattern:
ဥပမာ လုပ်ပုံ:

```
def get_current_datetime(date_format="%Y%m%d %H:%M:%S"):
    if not date_format:
        raise ValueError("date format cannot be empty")
    return datetime.now().strftime(date_format)
```

ကုဒ်အဓိပ္ပာယ်: `date_format` ဗလာဆို error ထုတ်တယ်။ ရှိရင် ယခုအချိန်ကို အဲဒီပုံစံနဲ့ ပြန်ပေးတယ်။

Tool function workflow: Claude identifies need for information → calls tool function → receives result or error → may retry with corrections if error occurred.
Tool function စီးဆင်းမှု: Claude က အချက်လိုတယ်လို့ သိ → tool function ခေါ် → ရလဒ် သို့မဟုတ် error ရ → error ဆို ပြင်ပြီး ပြန်ကြိုးစားနိုင်တယ်။

Purpose: Extend Claude's capabilities beyond its training data by providing access to real-time information like current datetime, weather, etc.
ရည်ရွယ်ချက်: ယခုအချိန်၊ ရာသီဥတု စတဲ့ အချိန်နဲ့တပြေးညီ အချက် ပေးပြီး၊ Claude ရဲ့ စွမ်းရည်ကို သင်ကြားဒေတာအပြင် တိုးချဲ့တာ။
</note>

<note title="Tool Schemas">
Tool Schemas
Tool Schema များ
Schema = tool က ဘာလဲ၊ ဘာထည့်ရမလဲ ပြတဲ့ ဖော်ပြချက်စာရွက်။

Tool Schemas = JSON schema specifications that describe tool functions and their parameters for language models
Tool Schemas = language model အတွက် tool function နဲ့ parameter တွေကို ဖော်ပြတဲ့ JSON schema သတ်မှတ်ချက်များ

JSON Schema = data validation specification (not ML-specific) used to validate JSON data, adopted by ML community for tool calling
JSON Schema = JSON ဒေတာ မှန်မမှန် စစ်တဲ့ သတ်မှတ်ချက် (ML သီးသန့် မဟုတ်)။ ML အသိုင်းအဝိုင်းက tool ခေါ်ဖို့ သုံးလာတယ်။

Tool Schema Structure:
Tool Schema ဖွဲ့စည်းပုံ:

- name: tool identifier
- name: tool ရဲ့ နာမည် / အမှတ်အသား

- description: 3-4 sentences explaining what tool does, when to use, what data it returns
- description: tool ဘာလုပ်လဲ၊ ဘယ်တော့သုံးလဲ၊ ဘာဒေတာ ပြန်ပေးလဲ ပြတဲ့ စာကြောင်း ၃-၄ ကြောင်း

- input_schema: actual JSON schema describing function arguments with types and descriptions
- input_schema: function argument တွေရဲ့ အမျိုးအစားနဲ့ ဖော်ပြချက် ပါတဲ့ တကယ့် JSON schema

Schema Generation Trick:
Schema ထုတ်တဲ့ လှည့်ကွက်:

1. Take tool function to Claude.ai
1. Tool function ကို Claude.ai ဆီ ယူသွားပါ

2. Prompt: "write valid JSON schema spec for tool calling for this function, follow best practices in attached documentation"
2. Prompt: "ဒီ function အတွက် tool calling သုံးတဲ့ မှန်ကန်တဲ့ JSON schema ရေးပါ၊ တွဲပို့စာရွက်ထဲက ကောင်းမွန်တဲ့နည်းတွေ လိုက်နာပါ"

3. Attach Anthropic API documentation tool use page
3. Anthropic API ရဲ့ tool use စာမျက်နှာ တွဲပို့ပါ

4. Copy generated schema
4. ထွက်လာတဲ့ schema ကို ကူးယူပါ

Implementation Pattern:
လုပ်ပုံ ပုံစံ:

- Name functions descriptively
- Function နာမည် ရှင်းရှင်းပေးပါ

- Name schemas as [function_name]_schema
- Schema နာမည်ကို `[function_name]_schema` လို့ ပေးပါ

- Import ToolParam from anthropic.types
- `anthropic.types` ကနေ `ToolParam` ကို import လုပ်ပါ

- Wrap schema dictionary with ToolParam() to prevent type errors
- type error မဖြစ်အောင် schema dictionary ကို `ToolParam()` နဲ့ ပတ်ပါ

Purpose = inform Claude about available tools, required arguments, and usage context through standardized JSON validation format
ရည်ရွယ်ချက် = ရနိုင်တဲ့ tool၊ လိုအပ်တဲ့ argument၊ ဘယ်အခြေအနေမှာ သုံးရမလဲ ဆိုတာကို စံ JSON ပုံစံနဲ့ Claude ကို ပြောပြတာ
</note>

<note title="Handling Message Blocks">
Handling Message Blocks
Message Block များ ကိုင်တွယ်ခြင်း
Block = message ထဲက အပိုင်းတစ်ခု (စာ၊ tool ခေါ်တာ စသဖြင့်)။

Tool-Enabled Claude Requests
Tool ပါတဲ့ Claude တောင်းဆိုချက်များ

Step 3: Making requests to Claude with tools = include tool schema in request alongside user message using `tools` keyword argument containing JSON schema specs.
အဆင့် ၃: Tool ပါအောင် Claude ဆီ တောင်းဆိုခြင်း = user message နဲ့အတူ `tools` argument ထဲမှာ JSON schema တွေ ထည့်ပါ။

Multi-Block Messages
Block များစွာ ပါတဲ့ Message

Content structure change = messages now contain multiple blocks instead of just text blocks.
အကြောင်းအရာ ဖွဲ့စည်းပုံ ပြောင်းခြင်း = message ထဲမှာ စာ block ပဲ မဟုတ်တော့ဘူး။ block အမျိုးမျိုး ပါတယ်။

Tool response format = assistant message with:
Tool အဖြေ ပုံစံ = assistant message ထဲမှာ:

- Text block = user-facing explanation
- Text block = user မြင်ရမယ့် ရှင်းလင်းချက်

- Tool use block = contains function name + arguments for tool execution
- Tool use block = အလုပ်လုပ်မယ့် function နာမည် + argument တွေ ပါတယ်

Message History Management
Message မှတ်တမ်း စီမံခြင်း

Critical requirement = manually maintain conversation history since Claude stores nothing.
အရေးကြီး လိုအပ်ချက် = Claude က ဘာမှ မသိမ်းလို့၊ စကားပြောမှတ်တမ်းကို ကိုယ်တိုင် ထိန်းရမယ်။

Multi-block handling = append entire response.content (all blocks) to messages list, not just text.
Block များစွာ ကိုင်တွယ်ပုံ = စာသက်သက် မဟုတ်ဘဲ `response.content` အားလုံး (block အကုန်) ကို messages စာရင်းထဲ ထည့်ပါ။

Helper function updates needed = add_user_message and add_assistant_message functions must support multiple blocks instead of single text blocks only.
Helper function တွေ ပြင်ရမယ် = `add_user_message` နဲ့ `add_assistant_message` က စာတစ်ခုတည်း မဟုတ်၊ block များစွာ လက်ခံရမယ်။

Conversation flow = user message → assistant response with tool use block → execute tool → respond back to Claude with full history.
စကားပြော စီးဆင်းမှု = user message → tool use block ပါတဲ့ assistant အဖြေ → tool အလုပ်လုပ် → မှတ်တမ်းအပြည့်နဲ့ Claude ဆီ ပြန်ပို့
</note>

<note title="Sending Tool Results">
Sending Tool Results
Tool ရလဒ် ပြန်ပို့ခြင်း

Tool Results = Results from executed tool functions sent back to Claude in follow-up requests.
Tool Results = အလုပ်လုပ်ပြီးတဲ့ tool function ရလဒ်တွေကို နောက်ဆက်တွဲ တောင်းဆိုချက်နဲ့ Claude ဆီ ပြန်ပို့တာ။

Process: Execute tool function requested by Claude → Create tool result block → Send follow-up request with full conversation history.
လုပ်ငန်းစဉ်: Claude တောင်းတဲ့ tool function အလုပ်လုပ် → tool result block လုပ် → စကားပြောမှတ်တမ်းအပြည့်နဲ့ နောက်ဆက်တွဲ ပို့

Tool Result Block Structure:
Tool Result Block ဖွဲ့စည်းပုံ:

- tool_use_id = Matches ID from original tool use block to pair requests with results
- tool_use_id = မူရင်း tool use block ရဲ့ ID နဲ့ ကိုက်အောင် ထားပြီး၊ တောင်းဆိုချက်နဲ့ ရလဒ် ချိတ်တယ်

- content = Tool function output converted to string (usually JSON)
- content = Tool function အထွက်ကို စာသား ပြောင်းထားတာ (များသောအားဖြင့် JSON)

- is_error = Boolean flag for function execution errors (default false)
- is_error = function မှားခဲ့လား ပြတဲ့ true/false (ပုံမှန် false)

Tool Use ID Purpose = Links multiple tool requests to correct results when Claude makes simultaneous tool calls. Each tool use gets unique ID, tool results must reference matching IDs.
Tool Use ID ရည်ရွယ်ချက် = Claude က tool များစွာ တစ်ပြိုင်နက် ခေါ်ရင်၊ ဘယ်ရလဒ်က ဘယ်တောင်းဆိုချက်လဲ ချိတ်ပေးတယ်။ Tool use တစ်ခုချင်းမှာ ID သီးသန့် ရှိတယ်။ Tool result က ကိုက်တဲ့ ID ကို ညွှန်းရမယ်။

Follow-up Request Requirements:
နောက်ဆက်တွဲ တောင်းဆိုချက် လိုအပ်ချက်:

- Include complete message history (original user message + assistant tool use message + new user message with tool result)
- message မှတ်တမ်းအပြည့် ထည့်ပါ (မူရင်း user message + assistant tool use message + tool result ပါတဲ့ user message အသစ်)

- Must include original tool schemas even if not using tools again
- tool ထပ်မသုံးတောင် မူရင်း tool schema တွေ ထည့်ရမယ်

- Tool result block goes in user message, not assistant message
- Tool result block က user message ထဲမှာ ထားရတယ်။ assistant message ထဲ မဟုတ်။

Conversation Flow: User request → Claude assistant response (text + tool use blocks) → Server executes tool → User message with tool result block → Claude final response with integrated results.
စကားပြော စီးဆင်းမှု: User တောင်းဆို → Claude assistant အဖြေ (စာ + tool use block) → Server က tool အလုပ်လုပ် → tool result block ပါတဲ့ user message → Claude က ရလဒ်ပေါင်းပြီး နောက်ဆုံးအဖြေ
</note>

<note title="Multi-Turn Conversations with Tools">
Multi-Turn Conversations with Tools
Tool ပါတဲ့ အလှည့်လိုက် စကားပြောခြင်း

Multi-Turn Tool Conversations = conversations where Claude uses multiple tools sequentially to answer a single user query.
Multi-Turn Tool Conversations = user မေးခွန်း တစ်ခုအတွက် Claude က tool များစွာကို အစဉ်လိုက် သုံးတဲ့ စကားပြော။

Tool Chaining Process = user asks question → Claude requests first tool → tool executed → result returned → Claude requests second tool → tool executed → result returned → Claude provides final answer.
Tool ချိတ်ဆက် လုပ်ငန်းစဉ် = user မေး → Claude က ပထမ tool တောင်း → tool အလုပ်လုပ် → ရလဒ်ပြန် → Claude က ဒုတိယ tool တောင်း → tool အလုပ်လုပ် → ရလဒ်ပြန် → Claude က နောက်ဆုံးအဖြေ ပေး

Example Flow = user asks "what day is 103 days from today" → Claude calls get_current_datetime → Claude calls add_duration_to_datetime → Claude provides answer.
ဥပမာ စီးဆင်းမှု = user က "ဒီနေ့ကနေ ၁၀၃ ရက်ကြာရင် ဘယ်နေ့လဲ" မေး → Claude က `get_current_datetime` ခေါ် → Claude က `add_duration_to_datetime` ခေါ် → Claude က အဖြေပေး

Implementation Pattern = while loop that continues calling Claude until no more tool requests, checking each response for tool_use blocks.
လုပ်ပုံ ပုံစံ = `while` loop နဲ့ Claude ကို ဆက်ခေါ်တယ်။ tool တောင်းတာ မရှိတော့မှ ရပ်တယ်။ အဖြေတိုင်းမှာ `tool_use` block ရှိမရှိ စစ်တယ်။

run_conversation Function = takes initial messages, loops through Claude calls, executes requested tools, adds results to conversation, continues until final response.
`run_conversation` Function = ပထမ messages ယူတယ်၊ Claude ခေါ်တာ လှည့်လုပ်တယ်၊ တောင်းတဲ့ tool တွေ အလုပ်လုပ်တယ်၊ ရလဒ်တွေ စကားပြောထဲ ထည့်တယ်၊ နောက်ဆုံးအဖြေ ရတဲ့အထိ ဆက်လုပ်တယ်။

Required Refactors:
ပြင်ရမယ့်အချက်များ:

- add_user_message/add_assistant_message = updated to handle multiple message blocks instead of just plain text
- `add_user_message` / `add_assistant_message` = ရိုးရိုးစာသက်သက် မဟုတ်၊ message block များစွာ ကိုင်တွယ်အောင် ပြင်ပါ

- chat function = accepts tools parameter, returns entire message instead of just first text block
- `chat` function = `tools` parameter လက်ခံပါ။ ပထမ စာ block ပဲ မဟုတ်၊ message အပြည့် ပြန်ပေးပါ

- text_from_message helper = extracts all text blocks from a message with multiple content blocks
- `text_from_message` helper = content block များစွာထဲက စာ block အားလုံး ထုတ်ယူတယ်

Key Insight = can't predict how many tools user queries will require, so system must handle arbitrary chains of tool calls automatically.
အဓိက နားလည်ချက် = user မေးခွန်းက tool ဘယ်နှစ်ခု လိုမလဲ ကြိုမသိနိုင်လို့၊ tool ခေါ်တာ ဘယ်လောက်ပဲ ရှည်ရှည် အလိုအလျောက် ကိုင်တွယ်နိုင်ရမယ်။
</note>

<note title="Implementing Multiple Turns">
Implementing Multiple Turns
အလှည့်များစွာ အကောင်အထည်ဖော်ခြင်း

Multiple Turns Implementation = continuously calling Claude until it stops requesting tools
အလှည့်များစွာ အကောင်အထည်ဖော်ခြင်း = Claude က tool ထပ်မတောင်းတော့တဲ့အထိ ဆက်ခေါ်နေတာ

Stop Reason Field = indicates why Claude stopped generating text
Stop Reason Field = Claude ဘာကြောင့် စာထုတ်တာ ရပ်လဲ ပြတယ်

- stop_reason = "tool_use" means Claude wants to call a tool
- `stop_reason = "tool_use"` ဆိုရင် Claude က tool ခေါ်ချင်တယ်

- Other values exist but tool_use is most commonly checked
- တန်ဖိုး တခြားလည်း ရှိတယ်။ အများဆုံး စစ်တာက `tool_use`

run_conversation Function = main loop that:
`run_conversation` Function = အဓိက loop။ လုပ်တာက:

1. Calls Claude with messages + available tools
1. messages + ရနိုင်တဲ့ tool တွေနဲ့ Claude ခေါ်တယ်

2. Adds assistant response to conversation history
2. assistant အဖြေကို စကားပြောမှတ်တမ်းထဲ ထည့်တယ်

3. Checks stop_reason - if not "tool_use", breaks loop
3. `stop_reason` စစ်တယ်။ `"tool_use"` မဟုတ်ရင် loop ရပ်တယ်

4. If tool_use, calls run_tools function
4. `tool_use` ဆိုရင် `run_tools` function ခေါ်တယ်

5. Adds tool results as user message
5. Tool ရလဒ်တွေကို user message အဖြစ် ထည့်တယ်

6. Repeats until no more tool requests
6. tool တောင်းတာ မရှိတော့တဲ့အထိ ထပ်လုပ်တယ်

run_tools Function = processes multiple tool use blocks:
`run_tools` Function = tool use block များစွာကို စီမံတယ်:

1. Filters message.content for blocks with type="tool_use"
1. `message.content` ထဲက `type="tool_use"` ဖြစ်တဲ့ block တွေ စစ်ထုတ်တယ်

2. Iterates through each tool request
2. tool တောင်းဆိုချက် တစ်ခုချင်း လှည့်လုပ်တယ်

3. Runs appropriate tool function via run_tool helper
3. `run_tool` helper နဲ့ သင့်တဲ့ tool function ခိုင်းတယ်

4. Creates tool_result blocks with: type="tool_result", tool_use_id=original_id, content=JSON_encoded_output, is_error=boolean
4. `tool_result` block တွေ လုပ်တယ်: `type="tool_result"`, `tool_use_id=original_id`, `content=JSON_encoded_output`, `is_error=boolean`

5. Returns list of all tool result blocks
5. tool result block အားလုံးရဲ့ စာရင်း ပြန်ပေးတယ်

run_tool Function = dispatcher that:
`run_tool` Function = လမ်းညွှန်သူ။ လုပ်တာက:

- Takes tool_name and tool_input
- `tool_name` နဲ့ `tool_input` ယူတယ်

- Uses if statements to match tool names to functions
- `if` နဲ့ tool နာမည်ကို function နဲ့ တွဲတယ်

- Executes appropriate tool function
- သင့်တဲ့ tool function အလုပ်လုပ်တယ်

- Scalable for adding multiple tools
- tool အသစ်များစွာ ထပ်ထည့်လို့ရအောင် ချဲ့လို့ရတယ်

Error Handling = try/except blocks around tool execution:
Error ကိုင်တွယ်ခြင်း = tool အလုပ်လုပ်တဲ့နေရာမှာ `try/except` သုံးပါ:

- Success: is_error=false, content=tool_output
- အောင်မြင်: `is_error=false`, `content=tool_output`

- Failure: is_error=true, content=error_message
- ကျရှုံး: `is_error=true`, `content=error_message`

Key Architecture Points:
အဓိက ဗိသုကာ အချက်များ:

- Assistant messages can contain multiple blocks (text + multiple tool_use)
- Assistant message ထဲမှာ block များစွာ ပါနိုင်တယ် (စာ + tool_use များစွာ)

- Each tool_use block gets separate tool_result response
- `tool_use` block တစ်ခုချင်းမှာ `tool_result` သီးသန့် ရှိရမယ်

- Tool results sent back as user message containing all results
- Tool ရလဒ်အားလုံးကို user message တစ်ခုထဲ ပေါင်းပြီး ပြန်ပို့တယ်

- Process repeats until Claude provides final text-only response
- Claude က စာသက်သက် နောက်ဆုံးအဖြေ ပေးတဲ့အထိ ထပ်လုပ်တယ်
</note>

<note title="Using Multiple Tools">
Using Multiple Tools
Tool များစွာ သုံးခြင်း

Multiple Tools Implementation = Adding additional tools to an existing tool system after initial framework setup.
Tool များစွာ အကောင်အထည်ဖော်ခြင်း = အခြေခံ framework ပြီးသွားရင်၊ ရှိပြီးသား tool စနစ်ထဲ tool အသစ်တွေ ထပ်ထည့်တာ။

Process = 3 steps: (1) Add tool schemas to RunConversation function's tools list, (2) Add conditional cases in RunTool function to handle new tool names, (3) Implement actual tool functions.
လုပ်ငန်းစဉ် = အဆင့် ၃ ဆင့်: (၁) `RunConversation` ရဲ့ tools စာရင်းထဲ schema ထည့်၊ (၂) `RunTool` ထဲ tool နာမည်အသစ်အတွက် `if` ထည့်၊ (၃) တကယ့် tool function တွေ ရေး

Key Components:
အဓိက အစိတ်အပိုင်းများ:

- RunConversation function = Contains tools list that makes Claude aware of available tools
- `RunConversation` function = Claude ကို ရနိုင်တဲ့ tool တွေ သိအောင် tools စာရင်း ပါတယ်

- RunTool function = Routes tool calls to appropriate functions based on tool name
- `RunTool` function = tool နာမည်အရ သင့်တဲ့ function ဆီ ပို့တယ်

- Tool schemas = Define tool structure for the AI model
- Tool schemas = AI model အတွက် tool ဖွဲ့စည်းပုံ သတ်မှတ်တယ်

- Tool functions = Actual implementation code
- Tool functions = တကယ့် အလုပ်လုပ်တဲ့ ကုဒ်

Example Tools Added:
ထည့်လိုက်တဲ့ ဥပမာ Tool များ:

- AddDurationToDateTime = Calculates date/time with duration offset
- `AddDurationToDateTime` = ရက်စွဲ/အချိန်ပေါ် ကြာချိန် ပေါင်းတွက်တယ်

- SetReminder = Creates reminder (mock implementation that prints confirmation)
- `SetReminder` = သတိပေးချက် လုပ်တယ် (အတုအယောင်၊ အတည်ပြုစာ ပုံနှိပ်ပြတာ)

Tool Chaining = AI can use multiple tools sequentially in single conversation (e.g., calculate date first, then set reminder with result).
Tool ချိတ်ဆက်ခြင်း = AI က စကားပြောတစ်ခုထဲမှာ tool များစွာ အစဉ်လိုက် သုံးနိုင်တယ် (ဥပမာ ရက်စွဲ အရင်တွက်၊ ပြီးမှ အဲဒီရလဒ်နဲ့ သတိပေးချက် ထား)။

Message Structure = Assistant responses can contain multiple blocks: text blocks + tool use blocks in same message.
Message ဖွဲ့စည်းပုံ = Assistant အဖြေထဲမှာ block များစွာ ပါနိုင်တယ်: စာ block + tool use block တွေ message တစ်ခုထဲမှာ။

Scalability = After initial framework setup, adding new tools becomes simple pattern of schema + routing + implementation.
ချဲ့ထွင်နိုင်မှု = အခြေခံ framework ပြီးရင်၊ tool အသစ်ထည့်တာက schema + လမ်းညွှန် + အကောင်အထည်ဖော် ဆိုတဲ့ ရိုးရိုးပုံစံ ဖြစ်သွားတယ်။
</note>

<note title="The Batch Tool">
The Batch Tool
Batch Tool
Batch = အလုပ်များစွာကို တစ်ပြိုင်နက် / တစ်စုတည်း လုပ်တာ။

Batch Tool = tool that enables Claude to run multiple tools in parallel within a single Assistant message instead of making separate sequential requests.
Batch Tool = Assistant message တစ်ခုထဲမှာ tool များစွာကို တစ်ပြိုင်နက် ခိုင်းတဲ့ tool။ တစ်ခုချင်း အစဉ်လိုက် မတောင်းတော့ဘူး။

Problem: Claude can technically send multiple tool use blocks in one message but rarely does so in practice, leading to unnecessary sequential tool calls.
ပြဿနာ: Claude က message တစ်ခုထဲ tool use block များစွာ ပို့လို့ရတယ်။ ဒါပေမဲ့ လက်တွေ့မှာ နည်းနည်းပဲ လုပ်တယ်။ ဒါကြောင့် မလိုအပ်ဘဲ အစဉ်လိုက် tool ခေါ်တာ ဖြစ်တယ်။

Solution: Create batch tool schema that takes list of invocations (each containing tool name + arguments). Instead of calling tools directly, Claude calls batch tool with array of desired tool executions.
ဖြေရှင်းချက်: invocation စာရင်း ယူတဲ့ batch tool schema လုပ်ပါ (တစ်ခုချင်းမှာ tool နာမည် + argument)။ Tool တွေ တိုက်ရိုက် မခေါ်ဘဲ၊ Claude က လုပ်ချင်တဲ့ tool တွေကို စာရင်းနဲ့ batch tool ခေါ်တယ်။

Implementation:
လုပ်ပုံ:

- Add batch tool to schema with invocations parameter
- `invocations` parameter ပါတဲ့ batch tool ကို schema ထဲ ထည့်ပါ

- Create run_batch function that iterates through invocations list
- `invocations` စာရင်းကို လှည့်လုပ်တဲ့ `run_batch` function ရေးပါ

- Extract tool name and JSON-parsed arguments from each invocation
- invocation တစ်ခုချင်းက tool နာမည်နဲ့ JSON ဖတ်ထားတဲ့ argument တွေ ထုတ်ပါ

- Call run_tool function for each requested tool
- တောင်းထားတဲ့ tool တစ်ခုချင်းအတွက် `run_tool` ခေါ်ပါ

- Return batch_output list containing results from all tool executions
- tool အားလုံးရဲ့ ရလဒ် ပါတဲ့ `batch_output` စာရင်း ပြန်ပေးပါ

Mechanism: Tricks Claude into parallel tool execution by providing higher-level abstraction that manually handles what multiple tool use blocks would accomplish automatically.
ယန္တရား: tool use block များစွာက အလိုအလျောက် လုပ်မယ့်အလုပ်ကို၊ အပေါ်အဆင့် abstraction က ကိုယ်တိုင် ကိုင်တွယ်ပေးပြီး၊ Claude ကို တစ်ပြိုင်နက် tool အလုပ်လုပ်အောင် လှည့်စားတယ်။

Result: Single request-response cycle instead of multiple sequential rounds for parallel-executable tasks.
ရလဒ်: တစ်ပြိုင်နက် လုပ်လို့ရတဲ့ အလုပ်တွေအတွက် အလှည့်များစွာ မလိုတော့ဘူး။ တောင်းဆို-အဖြေ တစ်ပတ်ပဲ။
</note>

<note title="Tools for Structured Data">
Tools for Structured Data
ဖွဲ့စည်းပုံရှိတဲ့ ဒေတာအတွက် Tool များ

Tools for Structured Data = alternative method to extract structured JSON from data sources using Claude's tool system instead of message pre-fill and stop sequences.
ဖွဲ့စည်းပုံရှိတဲ့ ဒေတာအတွက် Tool = message ကြိုဖြည့် + stop sequence အစား၊ Claude ရဲ့ tool စနစ်နဲ့ ဖွဲ့စည်းပုံရှိ JSON ထုတ်တဲ့ တခြားနည်း။

Key differences from prompt-based extraction:
Prompt နဲ့ ထုတ်တာနဲ့ ကွာခြားချက်:

- More reliable output
- အဖြေ ပိုယုံကြည်ရတယ်

- More complex setup
- ပြင်ဆင်မှု ပိုရှုပ်တယ်

- Requires JSON schema specification
- JSON schema သတ်မှတ်ချက် လိုတယ်

Core Process:
အဓိက လုပ်ငန်းစဉ်:

1. Define JSON schema for tool where inputs = desired data structure
1. လိုချင်တဲ့ ဒေတာဖွဲ့စည်းပုံကို tool ရဲ့ input အဖြစ် JSON schema သတ်မှတ်ပါ

2. Send prompt + schema to Claude
2. prompt + schema ကို Claude ဆီ ပို့ပါ

3. Claude calls tool with structured arguments matching schema
3. Claude က schema နဲ့ ကိုက်တဲ့ ဖွဲ့စည်းပုံရှိ argument တွေနဲ့ tool ခေါ်တယ်

4. Extract JSON from tool use block (no tool result needed)
4. tool use block ကနေ JSON ထုတ်ယူပါ (tool result မလိုဘူး)

Critical requirement = Force tool calling using tool_choice parameter:
အရေးကြီး လိုအပ်ချက် = `tool_choice` parameter နဲ့ tool ခေါ်ခိုင်းပါ:

- tool_choice = {"type": "tool", "name": "your_tool_name"}
- `tool_choice = {"type": "tool", "name": "your_tool_name"}`

- Ensures Claude always calls specified tool
- Claude က သတ်မှတ် tool ကို အမြဲ ခေါ်အောင် လုပ်တယ်

Implementation steps:
အကောင်အထည်ဖော် အဆင့်များ:

1. Create schema definition for extraction tool
1. ထုတ်ယူမယ့် tool အတွက် schema သတ်မှတ်ပါ

2. Update chat function to accept tool_choice parameter
2. `chat` function က `tool_choice` လက်ခံအောင် ပြင်ပါ

3. Pass tool_choice to client.messages.create()
3. `tool_choice` ကို `client.messages.create()` ဆီ ပို့ပါ

4. Access structured data from response.content[0].input
4. ဖွဲ့စည်းပုံရှိဒေတာကို `response.content[0].input` က ယူပါ

Use cases = When reliability more important than simplicity. Prompt-based methods better for quick/simple extractions, tools better for complex/reliable extractions.
သုံးသင့်ချိန် = ရိုးရှင်းမှုထက် ယုံကြည်ရမှု ပိုအရေးကြီးရင်။ မြန်မြန် / ရိုးရိုး ထုတ်ချင်ရင် prompt နည်း ပိုကောင်းတယ်။ ရှုပ်ထွေး / ယုံကြည်ရအောင် ထုတ်ချင်ရင် tool ပိုကောင်းတယ်။
</note>

<transcript title="Fine Grained Tool Calling">
Fine Grained Tool Calling
အသေးစိတ် Tool ခေါ်ခြင်း

Tool Streaming = streaming API responses while using tools with Claude
Tool Streaming = Claude နဲ့ tool သုံးနေစဉ် API အဖြေကို အပိုင်းလိုက် စီးထုတ်တာ

Key Components:
အဓိက အစိတ်အပိုင်းများ:

- Standard streaming returns content_block_delta events
- ပုံမှန် streaming က `content_block_delta` event တွေ ပြန်ပေးတယ်

- Tool streaming adds input_json_delta events with partial_json (chunk) and snapshot (cumulative sum)
- Tool streaming က `input_json_delta` event ထပ်ထည့်တယ်။ `partial_json` (အပိုင်း) နဲ့ `snapshot` (စုစုပေါင်း) ပါတယ်

- Implementation requires handling additional event type in streaming pipeline
- လုပ်ပုံမှာ streaming pipeline ထဲ event အမျိုးအစားအသစ် ကိုင်တွယ်ရမယ်

Fine-Grained Tool Calling = feature that disables JSON validation for faster streaming
Fine-Grained Tool Calling = JSON စစ်ဆေးတာ ပိတ်ပြီး streaming ပိုမြန်အောင် လုပ်တဲ့ လုပ်ဆောင်ချက်

Default Behavior:
ပုံမှန် အပြုအမူ:

- Claude generates JSON chunks for tool arguments
- Claude က tool argument တွေအတွက် JSON အပိုင်းလေးတွေ ထုတ်တယ်

- API buffers chunks until complete top-level key-value pair is generated
- အပေါ်ဆုံး key-value တစ်စုံ ပြည့်တဲ့အထိ API က အပိုင်းတွေ ယာယီ သိမ်းထားတယ်

- Validates JSON against schema before sending chunks to server
- server ဆီ မပို့ခင် JSON ကို schema နဲ့ စစ်တယ်

- Results in delays followed by burst of chunks arriving simultaneously
- နှောင့်နှေးပြီးမှ အပိုင်းတွေ တစ်ပြိုင်နက် လာတတ်တယ်

Fine-Grained Mode (fine_grained: true):
Fine-Grained Mode (`fine_grained: true`):

- Disables API-side JSON validation
- API ဘက်က JSON စစ်တာ ပိတ်တယ်

- Sends chunks immediately as generated
- ထုတ်တာနဲ့ အပိုင်းတွေ ချက်ချင်း ပို့တယ်

- Provides traditional streaming experience
- ပုံမှန် streaming အတွေ့အကြုံ ရတယ်

- Requires client-side error handling for invalid JSON
- မမှန်တဲ့ JSON အတွက် client ဘက်မှာ error ကိုင်တွယ်ရမယ်

Trade-offs:
အပေးအယူများ:

- Default = slower but validated JSON
- ပုံမှန် = ပိုနှေးတယ်၊ ဒါပေမဲ့ JSON စစ်ပြီးသား

- Fine-grained = faster streaming but potential invalid JSON (like "undefined" instead of null)
- Fine-grained = streaming ပိုမြန်တယ်၊ ဒါပေမဲ့ JSON မှားနိုင်တယ် (`null` အစား `"undefined"` လို)

- Invalid JSON in default mode gets wrapped as string rather than proper object structure
- ပုံမှန် mode မှာ မမှန်တဲ့ JSON ကို object မဟုတ်ဘဲ စာသားအဖြစ် ပတ်ထားတယ်

Use Cases:
သုံးသင့်ချိန်:

- Fine-grained useful for immediate UI updates or early processing of tool arguments
- Fine-grained က UI ချက်ချင်း ပြင်ချင်တာ၊ tool argument ကို စောစော စီမံချင်တာအတွက် ကောင်းတယ်

- Default sufficient when validation delays acceptable
- စစ်ဆေးတာ နည်းနည်းကြာလည်း ရရင် ပုံမှန် mode လုံလောက်တယ်
</transcript>

<note title="The Text Edit Tool">
The Text Edit Tool
စာပြင် Tool

Text Editor Tool = built-in Claude tool for file/text operations (read, write, create, replace, undo files/directories)
Text Editor Tool = ဖိုင်/စာ လုပ်ငန်းအတွက် Claude ထဲ ပါပြီးသား tool (ဖတ်၊ ရေး၊ ဖန်တီး၊ အစားထိုး၊ ပြန်ဖြည်၊ ဖိုင်/ဖိုလ်ဒါ)

Key characteristics:
အဓိက ဂုဏ်သတ္တိများ:

- Only JSON schema built into Claude, implementation must be custom-coded
- Claude ထဲ ပါတာက JSON schema ပဲ။ တကယ် လုပ်တဲ့ကုဒ်ကို ကိုယ်တိုင် ရေးရမယ်

- Schema stub sent to Claude gets auto-expanded to full schema
- Claude ဆီ schema အတို ပို့ရင် အလိုအလျောက် schema အပြည့် ဖြစ်သွားတယ်

- Schema type string varies by Claude model version (3.5 vs 3.7 have different dates)
- Schema type စာသားက Claude model ဗားရှင်းအလိုက် ကွာတယ် (3.5 နဲ့ 3.7 ရက်စွဲ မတူ)

- Enables Claude to act as software engineer out-of-the-box
- Claude ကို ဆော့ဖ်ဝဲ အင်ဂျင်နီယာလို အဆင်သင့် အလုပ်လုပ်ခိုင်းလို့ရတယ်

Required implementation:
ရေးရမယ့်အရာ:

- Custom class/functions to handle Claude's tool use requests
- Claude ရဲ့ tool use တောင်းဆိုချက် ကိုင်တွယ်တဲ့ ကိုယ်ပိုင် class/function

- Functions for: view files, string replace, create files, etc.
- ဖိုင်ကြည့်၊ စာသားအစားထိုး၊ ဖိုင်ဖန်တီး စတဲ့ function များ

- Actual file system operations not provided by Claude
- တကယ့် ဖိုင်စနစ် လုပ်ငန်းကို Claude က မပေးဘူး

Workflow:
လုပ်ငန်းစဉ်:

1. Send minimal schema stub to Claude (name + type with version-specific date)
1. schema အတိုကို Claude ဆီ ပို့ပါ (နာမည် + ဗားရှင်းရက်စွဲပါတဲ့ type)

2. Claude expands to full schema internally
2. Claude က အတွင်းမှာ schema အပြည့် ချဲ့တယ်

3. Claude sends tool use requests
3. Claude က tool use တောင်းဆိုချက် ပို့တယ်

4. Custom implementation executes actual file operations
4. ကိုယ်ရေးကုဒ်က တကယ့် ဖိုင်လုပ်ငန်း အလုပ်လုပ်တယ်

5. Results sent back to Claude
5. ရလဒ်ကို Claude ဆီ ပြန်ပို့တယ်

Use cases:
သုံးစရာများ:

- Replicate AI code editor functionality
- AI ကုဒ်အယ်ဒီတာ လုပ်ဆောင်ချက် အတုယူခြင်း

- File system operations where native editors unavailable
- ပုံမှန် အယ်ဒီတာ မရှိတဲ့နေရာမှာ ဖိုင်စနစ် လုပ်ငန်း

- Automated code generation/refactoring
- ကုဒ် အလိုအလျောက် ထုတ်ခြင်း / ပြန်စီခြင်း

- Multi-file project manipulation
- ဖိုင်များစွာ ပါတဲ့ ပရောဂျက် ကိုင်တွယ်ခြင်း

Benefits = approximates fancy code editor capabilities through API calls rather than GUI interaction.
အကျိုး = GUI နှိပ်တာမဟုတ်ဘဲ API ခေါ်ပြီး၊ ခေတ်မီ ကုဒ်အယ်ဒီတာနဲ့ နီးစပ်တဲ့ စွမ်းရည် ရတယ်။
</note>

<note title="The Web Search Tool">
The Web Search Tool
ဝက်ဘ်ရှာ Tool

Web Search Tool = built-in Claude tool for searching web to find up-to-date/specialized information for user questions
Web Search Tool = user မေးခွန်းအတွက် နောက်ဆုံးပေါ် / အထူးပြု အချက်အလက် ရှာဖို့ Claude ထဲ ပါပြီးသား ဝက်ဘ်ရှာ tool

Implementation = no custom code needed, Claude handles search execution automatically
လုပ်ပုံ = ကိုယ်ပိုင်ကုဒ် မလိုဘူး။ Claude က ရှာတာကို အလိုအလျောက် လုပ်တယ်

Schema Requirements:
Schema လိုအပ်ချက်:

- type: "web_search_20250305"
- type: `"web_search_20250305"`

- name: "web_search"
- name: `"web_search"`

- max_uses: number (limits total searches, default 5)
- max_uses: ဂဏန်း (ရှာခွင့် အကြိမ်ကန့်သတ်၊ ပုံမှန် ၅)

- allowed_domains: optional list to restrict search to specific domains
- allowed_domains: သတ်မှတ် domain တွေမှာပဲ ရှာခိုင်းတဲ့ စာရင်း (ထည့်ချင်မှ ထည့်)

Response Structure:
အဖြေ ဖွဲ့စည်းပုံ:

- Text blocks = Claude's explanatory text
- Text blocks = Claude ရဲ့ ရှင်းလင်းချက် စာ

- Tool use blocks = search queries Claude executed
- Tool use blocks = Claude ရှာခဲ့တဲ့ ရှာဖွေစာများ

- Web search result blocks = found pages (title, URL)
- Web search result blocks = တွေ့တဲ့ စာမျက်နှာများ (ခေါင်းစဉ်၊ URL)

- Citation blocks = specific text supporting Claude's statements
- Citation blocks = Claude ပြောချက်ကို ထောက်ခံတဲ့ တိကျတဲ့ စာသား

Key Features:
အဓိက လုပ်ဆောင်ချက်များ:

- Multiple searches possible per request (up to max_uses limit)
- တောင်းဆိုချက် တစ်ခုမှာ ရှာတာ များစွာ လုပ်နိုင်တယ် (`max_uses` အထိ)

- Domain restriction available for quality control
- အရည်အသွေး ထိန်းဖို့ domain ကန့်သတ်လို့ရတယ်

- Citation system links statements to source material
- Citation စနစ်က ပြောချက်တွေကို မူရင်းအရင်းအမြစ်နဲ့ ချိတ်တယ်

UI Rendering Pattern:
UI ပြပုံ:

- Display text blocks as normal text
- Text block တွေကို ပုံမှန်စာလို ပြပါ

- Show search results as reference list
- ရှာတွေ့ရလဒ်တွေကို ကိုးကားစာရင်းလို ပြပါ

- Highlight citations with source attribution (domain, title, URL, quoted text)
- Citation တွေကို အရင်းအမြစ်နဲ့ တွဲပြီး မီးမောင်းထိုးပါ (domain, ခေါင်းစဉ်, URL, ကူးယူစာ)

Use Case Example: Restricting to NIH.gov for medical/exercise advice ensures scientifically-backed information vs generic web content.
သုံးပုံ ဥပမာ: ဆေး/လေ့ကျင့်ခန်း အကြံကို NIH.gov မှာပဲ ရှာခိုင်းရင်၊ ဝက်ဘ်ပေါ် ရိုးရိုးစာထက် သိပ္ပံအခြေခံ အချက် ရတယ်။
</note>

<note title="Introducing Retrieval Augmented Generation">
Introducing Retrieval Augmented Generation
RAG မိတ်ဆက်
RAG = စာရွက်ကြီးထဲက သက်ဆိုင်တဲ့အပိုင်း ရှာပြီး၊ အဲဒီအပိုင်းနဲ့ AI ကို ဖြေခိုင်းတဲ့ နည်း။

RAG = Retrieval Augmented Generation technique for querying large documents using language models.
RAG = Retrieval Augmented Generation။ စာရွက်ကြီးတွေကို language model နဲ့ မေးတဲ့ နည်း။

Problem: How to extract specific information from large documents (100-1000+ pages) using Claude without hitting context limits.
ပြဿနာ: စာမျက်နှာ ၁၀၀-၁၀၀၀+ ရှိတဲ့ စာရွက်ကြီးထဲက တိကျတဲ့ အချက်ကို၊ context ကန့်သတ် မထိအောင် Claude နဲ့ ဘယ်လို ထုတ်မလဲ။

Option 1 (Direct approach): Place entire document text directly into prompt.
ရွေးချယ်မှု ၁ (တိုက်ရိုက်နည်း): စာရွက်စာသား အပြည့်ကို prompt ထဲ တိုက်ရိုက် ထည့်ပါ။

- Limitations: Hard token limits, decreased effectiveness with longer prompts, higher costs, slower processing
- အားနည်းချက်: token ကန့်သတ် ခိုင်မာတယ်၊ prompt ရှည်ရင် ထိရောက်မှု ကျတယ်၊ ကုန်ကျစရိတ် ပိုများတယ်၊ ပိုနှေးတယ်

Option 2 (RAG approach): Two-step process
ရွေးချယ်မှု ၂ (RAG နည်း): အဆင့် ၂ ဆင့်

- Step 1: Break document into small chunks
- အဆင့် ၁: စာရွက်ကို အပိုင်းသေးသေး ခွဲပါ

- Step 2: For user questions, find most relevant chunks and include only those in prompt
- အဆင့် ၂: user မေးခွန်းအတွက် အသက်ဆိုင်ဆုံး အပိုင်းတွေ ရှာပြီး၊ အဲဒါတွေပဲ prompt ထဲ ထည့်ပါ

RAG benefits: Model focuses on relevant content, scales to large/multiple documents, smaller prompts, lower costs, faster processing
RAG အကျိုး: Model က သက်ဆိုင်တဲ့ အကြောင်းအရာပဲ အာရုံစိုက်တယ်။ စာရွက်ကြီး / များစွာအထိ ချဲ့လို့ရတယ်။ prompt ပိုတိုတယ်။ ကုန်ကျစရိတ် လျော့တယ်။ ပိုမြန်တယ်။

RAG downsides: More complexity, requires preprocessing, needs search mechanism to find relevant chunks, no guarantee chunks contain complete context, multiple chunking strategies possible (equal portions vs header-based)
RAG အားနည်းချက်: ပိုရှုပ်တယ်။ ကြိုပြင်ဆင်ရတယ်။ သက်ဆိုင်တဲ့ အပိုင်းရှာတဲ့ စနစ် လိုတယ်။ အပိုင်းထဲ အကြောင်းအရာ ပြည့်မယ်လို့ အာမခံ မရဘူး။ ခွဲပုံ နည်းများစွာ ရှိတယ် (အရှည်တူခွဲ vs ခေါင်းစဉ်အလိုက်)

Key challenge: Defining relevance and optimal chunking strategy for specific use cases.
အဓိက စိန်ခေါ်မှု: ဒီအလုပ်အတွက် ဘာကို သက်ဆိုင်တယ်လို့ ပြောမလဲ၊ ဘယ်လို ခွဲရင် အကောင်းဆုံးလဲ သတ်မှတ်ရတာ။

RAG trades simplicity for scalability and efficiency but requires careful implementation and evaluation.
RAG က ရိုးရှင်းမှုကို စွန့်ပြီး၊ ချဲ့ထွင်နိုင်မှုနဲ့ ထိရောက်မှု ယူတယ်။ ဒါပေမဲ့ သေချာ အကောင်အထည်ဖော်၊ သေချာ အကဲဖြတ်ရမယ်။
</note>

<note title="Text Chunking Strategies">
Text Chunking Strategies
စာသား ခွဲခြမ်းနည်းများ
Chunk = စာရွက်ကို ခွဲထားတဲ့ အပိုင်းသေးသေး။

Text Chunking Strategies = process of dividing documents into smaller pieces for RAG pipelines
စာသား ခွဲခြမ်းနည်းများ = RAG pipeline အတွက် စာရွက်တွေကို အပိုင်းသေးသေး ခွဲတဲ့ လုပ်ငန်း

Core Problem: Chunking quality directly impacts RAG performance. Poor chunking leads to irrelevant context retrieval (e.g., medical "bug" text retrieved for software engineering query about bugs).
အဓိက ပြဿနာ: ခွဲပုံ အရည်အသွေးက RAG စွမ်းရည်ကို တိုက်ရိုက် သက်ရောက်တယ်။ မကောင်းရင် မသက်ဆိုင်တဲ့ အပိုင်း ရလာတယ် (ဥပမာ ဆော့ဖ်ဝဲ bug မေးတာမှာ ဆေးပညာ "bug" စာ ရလာတာ)။

Three Main Strategies:
အဓိက နည်း ၃ ခု:

1. Size-Based Chunking = dividing text into equal-length strings
1. အရွယ်အစားအလိုက် ခွဲခြင်း = စာကို အရှည်တူ အပိုင်းတွေ ခွဲတာ

- Pros: Easy to implement, most common in production
- အားသာချက်: လုပ်ရလွယ်တယ်၊ production မှာ အသုံးအများဆုံး

- Cons: Cut-off words, lacks context
- အားနည်းချက်: စကားလုံး ပြတ်တတ်တယ်၊ အကြောင်းအရာ မပြည့်ဘူး

- Solution: Overlap strategy = include characters from neighboring chunks to preserve context
- ဖြေရှင်းချက်: ထပ်နေအောင် ခွဲခြင်း = ဘေးက အပိုင်းက စာလုံးတွေ ပါအောင် ထည့်ပြီး အကြောင်းအရာ မပျောက်အောင်

- Trade-off: Creates text duplication but improves chunk meaning
- အပေးအယူ: စာ ထပ်နေတယ်၊ ဒါပေမဲ့ အပိုင်းရဲ့ အဓိပ္ပာယ် ပိုကောင်းတယ်

2. Structure-Based Chunking = dividing based on document structure (headers, paragraphs, sections)
2. ဖွဲ့စည်းပုံအလိုက် ခွဲခြင်း = ခေါင်းစဉ်၊ စာပိုဒ်၊ အခန်းတွေအရ ခွဲတာ

- Best for structured documents (markdown, HTML)
- ဖွဲ့စည်းပုံရှိတဲ့ စာရွက်အတွက် အကောင်းဆုံး (markdown, HTML)

- Limitation: Requires guaranteed document formatting
- ကန့်သတ်: စာရွက် ပုံစံ ရှိမယ်လို့ အာမခံရမယ်

- Example: Split on markdown headers (##) to create section-based chunks
- ဥပမာ: markdown ခေါင်းစဉ် (`##`) မှာ ခွဲပြီး အခန်းအလိုက် အပိုင်းလုပ်ပါ

3. Semantic-Based Chunking = using NLP to group related sentences/sections
3. အဓိပ္ပာယ်အလိုက် ခွဲခြင်း = NLP သုံးပြီး ဆက်စပ်တဲ့ စာကြောင်း / အခန်းတွေ အုပ်စုဖွဲ့တာ

- Most advanced technique
- အခေတ်အမီဆုံး နည်း

- Groups consecutive sentences based on semantic similarity
- ဆက်တိုက်စာကြောင်းတွေကို အဓိပ္ပာယ် တူမှုအရ အုပ်စုဖွဲ့တယ်

- Complex implementation
- အကောင်အထည်ဖော်ရ ရှုပ်တယ်

Key Implementation Notes:
အကောင်အထည်ဖော် မှတ်စုများ:

- Chunk by character = most reliable fallback, works with any document type
- စာလုံးအရေအတွက်နဲ့ ခွဲ = အယုံကြည်ရဆုံး အရန်နည်း။ စာရွက်အမျိုးအစား အားလုံးမှာ ရတယ်

- Chunk by sentence = good middle ground if sentence detection works reliably
- စာကြောင်းအလိုက် ခွဲ = စာကြောင်းခွဲတာ ယုံကြည်ရရင် ကောင်းတဲ့ အလယ်အလတ်

- Chunk by section = optimal results but requires structured input
- အခန်းအလိုက် ခွဲ = ရလဒ်အကောင်းဆုံး၊ ဒါပေမဲ့ ဖွဲ့စည်းပုံရှိတဲ့ input လိုတယ်

- Strategy choice depends on document type guarantees and use case requirements
- ဘယ်နည်းရွေးမလဲ ဆိုတာ စာရွက်အမျိုးအစား သေချာမှုနဲ့ အလုပ်လိုအပ်ချက်ပေါ် မူတည်တယ်

Rule: No universal best chunking method - depends on document structure guarantees and specific use case.
စည်းမျဉ်း: ကမ္ဘာလုံးဆိုင်ရာ အကောင်းဆုံး ခွဲနည်း မရှိဘူး။ စာရွက်ဖွဲ့စည်းပုံ သေချာမှုနဲ့ တိကျတဲ့ အသုံးပြုမှုပေါ် မူတည်တယ်။
</note>

<note title="Text Embeddings">
Text Embeddings
စာသား Embedding များ
Embedding = စာသား အဓိပ္ပာယ်ကို ဂဏန်းစာရင်းနဲ့ ပြတာ။

Text Embeddings = numerical representation of text meaning generated by embedding models
Text Embeddings = embedding model က ထုတ်တဲ့ စာသားအဓိပ္ပာယ်ရဲ့ ဂဏန်း ကိုယ်စားပြုမှု

Embedding Model = takes text input, outputs long list of numbers (range -1 to +1)
Embedding Model = စာသားထည့်ရင် ဂဏန်းရှည်စာရင်း ထုတ်တယ် (အပိုင်းအခြား -1 ကနေ +1)

Embedding Numbers = scores representing unknown qualities/features of input text. Each number theoretically scores different aspects (happiness, topic relevance, etc.) but actual meaning is unknown to users.
Embedding ဂဏန်းများ = ထည့်လိုက်တဲ့စာရဲ့ မသိရတဲ့ ဂုဏ်သတ္တိ / လက္ခဏာတွေကို မှတ်ချက်ပေးထားတာ။ ဂဏန်းတစ်ခုချင်းက သီအိုရီအရ ကွာခြားတဲ့ ရှုထောင့် (ပျော်ရွှင်မှု၊ ခေါင်းစဉ် သက်ဆိုင်မှု စသဖြင့်) ကို တိုင်းတယ်။ ဒါပေမဲ့ တကယ့်အဓိပ္ပာယ်ကို user မသိရဘူး။

Semantic Search = uses text embeddings to find text chunks related to user questions in RAG pipelines. Solves the search problem of matching user queries to relevant document chunks.
Semantic Search = RAG pipeline ထဲမှာ user မေးခွန်းနဲ့ သက်ဆိုင်တဲ့ စာအပိုင်းတွေကို embedding နဲ့ ရှာတာ။ User မေးခွန်းနဲ့ စာရွက်အပိုင်း တွဲတဲ့ ရှာဖွေပြဿနာကို ဖြေရှင်းတယ်။

RAG Pipeline Process = extract text chunks → user submits query → find related chunks using semantic search → add relevant chunks as context to prompt
RAG Pipeline လုပ်ငန်းစဉ် = စာအပိုင်းတွေ ထုတ် → user မေးခွန်းပို့ → semantic search နဲ့ သက်ဆိုင်တဲ့ အပိုင်းရှာ → သက်ဆိုင်တဲ့ အပိုင်းတွေကို prompt ထဲ context အဖြစ် ထည့်

Implementation = Anthropic recommends Voyage AI for embedding generation. Requires separate account/API key. Free to start, easy integration via SDK.
လုပ်ပုံ = Anthropic က embedding ထုတ်ဖို့ Voyage AI ကို အကြံပေးတယ်။ account / API key သီးသန့် လိုတယ်။ စသုံးရ အခမဲ့။ SDK နဲ့ ပေါင်းရ လွယ်တယ်။

Key Insight = Embeddings enable semantic similarity matching rather than keyword matching, allowing better understanding of text relationships for retrieval tasks.
အဓိက နားလည်ချက်: Embedding က စကားလုံးတူတာ ရှာတာမဟုတ်ဘဲ၊ အဓိပ္ပာယ်တူတာ ရှာတယ်။ ဒါကြောင့် ပြန်လည်ထုတ်ယူတဲ့ အလုပ်မှာ စာသား ဆက်စပ်မှုကို ပိုနားလည်တယ်။
</note>

<note title="The Full RAG Flow">
The Full RAG Flow
RAG စီးဆင်းမှု အပြည့်

RAG Flow = 7-step process combining text chunking, embeddings, and vector search to retrieve relevant context for LLM queries.
RAG Flow = စာသားခွဲခြင်း၊ embedding၊ vector ရှာဖွေခြင်း ပေါင်းပြီး၊ LLM မေးခွန်းအတွက် သက်ဆိုင်တဲ့ context ယူတဲ့ အဆင့် ၇ ဆင့်။

Step 1: Text Chunking = Split source documents into separate text pieces
အဆင့် ၁: စာသားခွဲခြင်း = မူရင်းစာရွက်တွေကို စာအပိုင်းတွေ ခွဲပါ

Step 2: Generate Embeddings = Convert text chunks into numerical vectors using embedding models
အဆင့် ၂: Embedding ထုတ်ခြင်း = စာအပိုင်းတွေကို embedding model နဲ့ ဂဏန်း vector ပြောင်းပါ

Step 3: Normalization = Scale vector magnitudes to 1.0 (handled automatically by embedding APIs)
အဆင့် ၃: Normalization = vector အရှည်ကို 1.0 ဖြစ်အောင် ချိန်ပါ (embedding API တွေက အလိုအလျောက် လုပ်တယ်)

Step 4: Vector Database Storage = Store embeddings in specialized database optimized for numerical vector operations
အဆင့် ၄: Vector Database သိမ်းခြင်း = ဂဏန်း vector လုပ်ငန်းအတွက် ပြုလုပ်ထားတဲ့ database ထဲ embedding တွေ သိမ်းပါ

Step 5: Query Processing = Convert user question into embedding using same model
အဆင့် ၅: မေးခွန်း စီမံခြင်း = user မေးခွန်းကို တူညီတဲ့ model နဲ့ embedding ပြောင်းပါ

Step 6: Similarity Search = Find most similar stored embeddings using cosine similarity calculation
အဆင့် ၆: တူညီမှု ရှာဖွေခြင်း = cosine similarity တွက်ပြီး၊ သိမ်းထားတဲ့ embedding ထဲက အတူဆုံးတွေ ရှာပါ

Step 7: Prompt Assembly = Combine user question with retrieved relevant text chunks, send to LLM
အဆင့် ၇: Prompt စုစည်းခြင်း = user မေးခွန်း + ရှာတွေ့တဲ့ စာအပိုင်းတွေ ပေါင်းပြီး LLM ဆီ ပို့ပါ

Key Math Concepts:
အဓိက သင်္ချာ အယူအဆများ:

- Cosine Similarity = cosine of angle between vectors, returns values -1 to 1, closer to 1 means more similar
- Cosine Similarity = vector နှစ်ခုကြား ထောင့်ရဲ့ cosine။ တန်ဖိုး -1 ကနေ 1။ 1 နဲ့ နီးရင် ပိုတူတယ်

- Cosine Distance = 1 minus cosine similarity, values closer to 0 mean higher similarity
- Cosine Distance = 1 နုတ် cosine similarity။ 0 နဲ့ နီးရင် ပိုတူတယ်

- Vector Database = performs similarity calculations to find closest matching embeddings
- Vector Database = အနီးစပ်ဆုံး embedding ရှာဖို့ တူညီမှု တွက်ချက်တယ်

Process Flow: Pre-processing (steps 1-4) → User Query → Real-time retrieval (steps 5-7) → LLM Response
လုပ်ငန်းစဉ် စီးဆင်းမှု: ကြိုပြင်ဆင်ခြင်း (အဆင့် ၁-၄) → User မေးခွန်း → အချိန်နဲ့တပြေးညီ ရှာယူခြင်း (အဆင့် ၅-၇) → LLM အဖြေ
</note>

<note title="Implementing the Rag Flow">
Implementing the Rag Flow
RAG Flow အကောင်အထည်ဖော်ခြင်း

RAG Flow Implementation = practical walkthrough of 5-step retrieval-augmented generation process
RAG Flow အကောင်အထည်ဖော်ခြင်း = ရှာယူပြီး ဖြည့်စွက် ထုတ်တဲ့ လုပ်ငန်းကို အဆင့် ၅ ဆင့်နဲ့ လက်တွေ့ လျှောက်ပြတာ

Step 1: Text Chunking = split document into sections using chunk_by_section function on report.MD file
အဆင့် ၁: စာသားခွဲခြင်း = `report.MD` ဖိုင်ကို `chunk_by_section` function နဲ့ အခန်းတွေ ခွဲပါ

Step 2: Embedding Generation = create vector representations for each chunk using generate_embedding function (supports single string or list of strings input)
အဆင့် ၂: Embedding ထုတ်ခြင်း = `generate_embedding` function နဲ့ အပိုင်းတစ်ခုချင်း vector လုပ်ပါ (စာသားတစ်ခု သို့မဟုတ် စာသားစာရင်း လက်ခံတယ်)

Step 3: Vector Store Population = create vector index instance, loop through chunk-embedding pairs using zip(), store each pair with store.add_vector(embedding, {content: chunk}). Store original text with embeddings for meaningful retrieval results.
အဆင့် ၃: Vector Store ဖြည့်ခြင်း = vector index instance လုပ်ပါ။ `zip()` နဲ့ chunk-embedding စုံတွေ လှည့်ပါ။ `store.add_vector(embedding, {content: chunk})` နဲ့ သိမ်းပါ။ ရှာတွေ့ရင် အဓိပ္ပာယ်ရှိအောင် မူရင်းစာသားကို embedding နဲ့အတူ သိမ်းပါ။

Step 4: Query Processing = user asks question "what did software engineering department do last year", generate embedding for user query
အဆင့် ၄: မေးခွန်း စီမံခြင်း = user က "software engineering ဌာန မနှစ်က ဘာလုပ်ခဲ့လဲ" မေးတယ်။ user မေးခွန်းအတွက် embedding ထုတ်ပါ

Step 5: Similarity Search = use store.search(user_embedding, 2) to find 2 most relevant chunks, returns results with cosine distances (0.71 for section two, 0.72 for methodology section)
အဆင့် ၅: တူညီမှု ရှာဖွေခြင်း = `store.search(user_embedding, 2)` နဲ့ အသက်ဆိုင်ဆုံး အပိုင်း ၂ ခု ရှာပါ။ cosine distance ပါတဲ့ ရလဒ် ပြန်ပေးတယ် (အခန်း ၂ က ၀.၇၁၊ methodology အခန်းက ၀.၇၂)

Key Components:
အဓိက အစိတ်အပိုင်းများ:

- Vector Index Class = custom vector database implementation
- Vector Index Class = ကိုယ်ပိုင် vector database အကောင်အထည်ဖော်မှု

- Cosine Distance = similarity metric between query and stored embeddings
- Cosine Distance = မေးခွန်း embedding နဲ့ သိမ်းထားတဲ့ embedding ကြား တူညီမှု တိုင်းတာချက်

- Metadata Storage = storing original text content alongside embeddings enables meaningful retrieval
- Metadata သိမ်းခြင်း = မူရင်းစာသားကို embedding ဘေးမှာ သိမ်းရင် ရှာတွေ့တာ အဓိပ္ပာယ်ရှိတယ်

Workflow complete but has limitations requiring further improvements.
လုပ်ငန်းစဉ် ပြီးပြီ။ ဒါပေမဲ့ ကန့်သတ်တွေ ရှိသေးလို့ ထပ်တိုးတက်အောင် လုပ်ရမယ်။
</note>

<note title="BM25 Lexical Search">
BM25 Lexical Search
BM25 စကားလုံး ရှာဖွေခြင်း
Lexical search = စကားလုံး တူတာကို ရှာတာ (အဓိပ္ပာယ် တူတာ မဟုတ်)။

BM25 = Best Match 25, a lexical search algorithm commonly used in RAG pipelines to complement semantic search.
BM25 = Best Match 25။ စကားလုံး ရှာတဲ့ algorithm။ RAG pipeline မှာ semantic search ကို ဖြည့်ဖို့ မကြာခဏ သုံးတယ်။

Problem with semantic search alone = Can miss exact term matches, returning irrelevant results even when specific terms appear frequently in certain documents.
Semantic search သက်သက်ရဲ့ ပြဿနာ = စကားလုံး တိတိကျကျ တူတာ လွတ်နိုင်တယ်။ တချို့စာရွက်မှာ အဲဒီစကားလုံး မကြာခဏ ပါနေတောင် မသက်ဆိုင်တဲ့ ရလဒ် ရနိုင်တယ်။

Hybrid search approach = Combines semantic search (embeddings/vector database) with lexical search (BM25) in parallel, then merges results for better balance.
Hybrid ရှာဖွေနည်း = semantic search (embedding / vector database) နဲ့ lexical search (BM25) ကို တစ်ပြိုင်နက် လုပ်ပြီး၊ ရလဒ် ပေါင်းကာ ပိုမျှတအောင် လုပ်တာ။

BM25 algorithm steps:
BM25 algorithm အဆင့်များ:

1. Tokenize user query into separate terms (remove punctuation, split on spaces)
1. user မေးခွန်းကို စကားလုံးတွေ ခွဲပါ (ပုဒ်ဖြတ်ဖြုတ်၊ နေရာလွတ်မှာ ခွဲ)

2. Count frequency of each term across all text chunks/documents
2. စာအပိုင်း / စာရွက် အားလုံးမှာ စကားလုံးတစ်လုံးချင်း ဘယ်နှစ်ခါ ပါလဲ ရေတွက်ပါ

3. Assign relative importance to terms based on usage frequency (rare terms = higher importance, common terms like "a" = lower importance)
3. သုံးနှုန်းအရ အရေးပါမှု ပေးပါ (ရှားတဲ့စကားလုံး = ပိုအရေးကြီး၊ `"a"` လို အသုံးများတာ = အရေးနည်း)

4. Rank text chunks by how often they contain higher-weighted terms
4. အလေးပိုတဲ့ စကားလုံး များများပါတဲ့ စာအပိုင်းကို အပေါ်တင်ပါ

Key insight = Frequently used terms across corpus are less important for search relevance than rare, specific terms.
အဓိက နားလည်ချက်: စာစုတစ်ခုလုံးမှာ မကြာခဏ သုံးတဲ့ စကားလုံးထက်၊ ရှားပြီး တိကျတဲ့ စကားလုံးက ရှာဖွေမှုအတွက် ပိုအရေးကြီးတယ်။

BM25 advantages = Better at finding exact term matches, prioritizes documents containing rare/specific search terms, complements semantic search weaknesses.
BM25 အားသာချက် = စကားလုံး တိတိကျကျ တူတာ ရှာတာ ပိုကောင်းတယ်။ ရှား/တိကျတဲ့ ရှာဖွေစကားလုံး ပါတဲ့ စာရွက်ကို ဦးစားပေးတယ်။ Semantic search ရဲ့ အားနည်းချက်ကို ဖြည့်တယ်။

Implementation = Both semantic and lexical search systems use similar APIs (add_document, search functions) making them easy to combine.
လုပ်ပုံ = Semantic နဲ့ lexical ရှာဖွေစနစ် နှစ်ခုလုံး API တူတူ သုံးတယ် (`add_document`, `search`)။ ဒါကြောင့် ပေါင်းရ လွယ်တယ်။

Next step = Merge results from both search systems to get benefits of semantic understanding plus exact term matching.
နောက်အဆင့် = ရှာဖွေစနစ် နှစ်ခုရဲ့ ရလဒ် ပေါင်းပါ။ အဓိပ္ပာယ်နားလည်မှု + စကားလုံးတိကျမှု နှစ်ခုလုံး ရမယ်။
</note>

<note title="A Multi-Index Rag Pipeline">
A Multi-Index Rag Pipeline
Index များစွာ ပါတဲ့ RAG Pipeline
Index = ရှာလွယ်အောင် စီထားတဲ့ ဒေတာအညွှန်း။

Multi-Index RAG Pipeline = system combining semantic search (vector index) and lexical search (BM25 index) for improved retrieval accuracy.
Multi-Index RAG Pipeline = ရှာယူမှန်ကန်မှု ပိုကောင်းအောင် semantic search (vector index) နဲ့ lexical search (BM25 index) ပေါင်းတဲ့ စနစ်။

Key Components:
အဓိက အစိတ်အပိုင်းများ:

- Vector Index = semantic similarity search using embeddings
- Vector Index = embedding သုံးပြီး အဓိပ္ပာယ်တူတာ ရှာတယ်

- BM25 Index = lexical/keyword-based search
- BM25 Index = စကားလုံး / keyword အခြေခံ ရှာဖွေခြင်း

- Retriever Class = wrapper that forwards queries to both indexes and merges results
- Retriever Class = မေးခွန်းကို index နှစ်ခုလုံးဆီ ပို့ပြီး ရလဒ် ပေါင်းတဲ့ အပတ်အကာ

Reciprocal Rank Fusion = technique for merging search results from different indexes. Formula: RRF_score = sum of (1/(rank + 1)) across all search methods for each document. Documents ranked by highest combined score.
Reciprocal Rank Fusion = index မတူတဲ့ ရှာဖွေရလဒ်တွေ ပေါင်းတဲ့ နည်း။ ဖော်မြူလာ: `RRF_score = sum of (1/(rank + 1))`။ ရှာနည်းအားလုံးမှာ စာရွက်တစ်ခုချင်းအတွက် ပေါင်းတယ်။ ပေါင်းမှတ် အမြင့်ဆုံးကို အပေါ်တင်တယ်။

Example: Vector search returns [doc2, doc7, doc6], BM25 returns [doc6, doc2, doc7]. After RRF calculation, final ranking becomes [doc2, doc6, doc7] because doc2 ranked high in both methods.
ဥပမာ: Vector ရှာလို့ `[doc2, doc7, doc6]` ရတယ်။ BM25 က `[doc6, doc2, doc7]` ရတယ်။ RRF တွက်ပြီးရင် နောက်ဆုံး အစဉ် `[doc2, doc6, doc7]` ဖြစ်တယ်။ ဘာလို့လဲဆိုတော့ doc2 က နည်းနှစ်ခုလုံးမှာ အဆင့်မြင့်လို့။

Benefits:
အကျိုးများ:

- Improved search accuracy by combining different search paradigms
- ရှာဖွေပုံ မတူတာတွေ ပေါင်းလို့ ရှာမှန်ကန်မှု တက်တယ်

- Modular design with standardized API (search() and add_document() methods)
- စံ API ရှိတဲ့ အပိုင်းလိုက် ဒီဇိုင်း (`search()` နဲ့ `add_document()`)

- Easy to extend with additional search indexes
- ရှာဖွေ index အသစ် ထပ်ထည့်ရ လွယ်တယ်

- Better handling of edge cases where single method fails
- နည်းတစ်ခုတည်း ကျရှုံးတဲ့ ထူးခြားဖြစ်ရပ်ကို ပိုကောင်းအောင် ကိုင်တွယ်တယ်

Implementation pattern allows multiple search methodologies to work together while maintaining separate, isolated index classes.
လုပ်ပုံ ပုံစံက ရှာနည်းများစွာ ပူးပေါင်းခွင့်ပေးတယ်။ Index class တွေကတော့ သီးသန့် ခွဲထားဆဲ။
</note>

<note title="Reranking Results">
Reranking Results
ရလဒ်တွေ ပြန်အစီအစဉ်ချခြင်း
Rerank = ရှာပြီးသား ရလဒ်တွေကို ပြန်စီတာ။

Reranking = post-processing step that uses LLM to reorder search results by relevance after initial retrieval.
Reranking = ပထမ ရှာပြီးရင်၊ LLM နဲ့ ရလဒ်တွေကို သက်ဆိုင်မှုအလိုက် ပြန်စီတဲ့ နောက်ဆက်တွဲ အဆင့်။

Process: Run vector + BM25 search → merge results → pass to LLM with prompt asking to rank documents by relevance → get reordered results.
လုပ်ငန်းစဉ်: vector + BM25 ရှာ → ရလဒ်ပေါင်း → LLM ဆီ ပို့ပြီး သက်ဆိုင်မှုအလိုက် စီခိုင်း → ပြန်စီထားတဲ့ ရလဒ် ရ

Implementation details: Use document IDs instead of full text for efficiency. LLM receives user query + candidate documents + instruction to return most relevant docs in decreasing order. Assistant message pre-fill + stop sequence ensures structured JSON output.
လုပ်ပုံ အသေးစိတ်: မြန်အောင် စာအပြည့် မပို့ဘဲ document ID သုံးပါ။ LLM က user မေးခွန်း + ကိုယ်စားလှယ် စာရွက်တွေ + အသက်ဆိုင်ဆုံးကို အစဉ်ကျ ပြန်ခိုင်းတဲ့ ညွှန်ကြားချက် ရတယ်။ Assistant message ကြိုဖြည့် + stop sequence က ဖွဲ့စည်းပုံရှိ JSON အဖြေ ရအောင် လုပ်တယ်။

Tradeoffs: Increases search accuracy by leveraging LLM's understanding of semantic relevance. Increases latency due to additional LLM call. Particularly effective when initial retrieval methods miss nuanced query intent (e.g., "ENG team" vs "engineering team").
အပေးအယူ: LLM ရဲ့ အဓိပ္ပာယ်နားလည်မှုကြောင့် ရှာမှန်ကန်မှု တက်တယ်။ LLM ထပ်ခေါ်လို့ နှောင့်နှေးမှု တက်တယ်။ ပထမ ရှာနည်းက မေးခွန်းရဲ့ သိမ်မွေ့တဲ့ ရည်ရွယ်ချက် လွတ်တဲ့အခါ အထူးထိရောက်တယ် (ဥပမာ `"ENG team"` နဲ့ `"engineering team"`)။

Example improvement: Query "What did engineering team do with incident 2023?" correctly prioritized software engineering section over cybersecurity section after reranking, despite hybrid search initially ranking it lower.
တိုးတက်မှု ဥပမာ: `"What did engineering team do with incident 2023?"` မေးခွန်းမှာ၊ hybrid ရှာစဉ်က software engineering အခန်းကို အောက်မှာ ထားခဲ့ပေမဲ့၊ rerank ပြီးရင် cybersecurity အခန်းထက် မှန်မှန် ဦးစားပေးသွားတယ်။
</note>

<note title="Contextual Retrieval">
Contextual Retrieval
အကြောင်းအရာပါအောင် ရှာယူခြင်း

Contextual Retrieval = technique to improve RAG pipeline accuracy by adding context to document chunks before embedding.
Contextual Retrieval = embedding မလုပ်ခင် စာအပိုင်းတွေမှာ context ထည့်ပြီး၊ RAG pipeline မှန်ကန်မှု တိုးတဲ့ နည်း။

Problem: When documents are split into chunks, individual chunks lose context from the original document, reducing retrieval accuracy.
ပြဿနာ: စာရွက်ကို အပိုင်းခွဲလိုက်ရင်၊ အပိုင်းတစ်ခုချင်းက မူရင်းစာရွက်ရဲ့ အကြောင်းအရာ ဆုံးရှုံးတယ်။ ရှာယူမှန်ကန်မှု ကျတယ်။

Solution: Pre-processing step that adds contextual information to each chunk before inserting into retriever database.
ဖြေရှင်းချက်: retriever database ထဲ မထည့်ခင်၊ အပိုင်းတစ်ခုချင်းကို အကြောင်းအရာအချက် ထည့်တဲ့ ကြိုပြင်ဆင် အဆင့်။

Process:
လုပ်ငန်းစဉ်:

1. Take individual chunk + original source document
1. အပိုင်းတစ်ခု + မူရင်းစာရွက် ယူပါ

2. Send to LLM (Claude) with prompt asking to generate situating context
2. ဒီအပိုင်းက စာရွက်ထဲ ဘယ်မှာ / ဘာအကြောင်းလဲ ဆိုတဲ့ context ရေးခိုင်းပြီး LLM (Claude) ဆီ ပို့ပါ

3. LLM generates brief context explaining chunk's relationship to larger document
3. LLM က ဒီအပိုင်းနဲ့ စာရွက်ကြီး ဆက်စပ်ပုံ ရှင်းတဲ့ context အတို ထုတ်တယ်

4. Join generated context with original chunk = "contextualized chunk"
4. ထွက်လာတဲ့ context ကို မူရင်းအပိုင်းနဲ့ ပေါင်း = "contextualized chunk"

5. Use contextualized chunk as input to vector/BM25 indexes
5. အဲဒီ contextualized chunk ကို vector / BM25 index ထဲ ထည့်ပါ

Large Document Handling: If source document too large for single prompt, use selective context strategy:
စာရွက်ကြီး ကိုင်တွယ်ပုံ: မူရင်းစာရွက်က prompt တစ်ခုထဲ မဝင်ရင်၊ ရွေးချယ် context နည်း သုံးပါ:

- Include starter chunks (1-3) from document beginning for summary/abstract
- အနှစ်ချုပ်ရဖို့ စာရွက်အစက အပိုင်း ၁-၃ ခု ထည့်ပါ

- Include chunks immediately before target chunk for local context
- ဒေသခံ context အတွက် ပစ်မှတ်အပိုင်း မတိုင်ခင်က အပိုင်းတွေ ထည့်ပါ

- Skip middle chunks that provide less relevant context
- သက်ဆိုင်မှုနည်းတဲ့ အလယ်အပိုင်းတွေ ကျော်ပါ

Implementation: add_context function takes text chunk + source text, generates context via LLM, concatenates context with original chunk, returns contextualized version.
လုပ်ပုံ: `add_context` function က စာအပိုင်း + မူရင်းစာ ယူတယ်၊ LLM နဲ့ context ထုတ်တယ်၊ မူရင်းအပိုင်းနဲ့ ပေါင်းတယ်၊ contextualized ဗားရှင်း ပြန်ပေးတယ်။

Benefit: Chunks retain ties to larger document structure and cross-references, improving retrieval accuracy for complex documents with interconnected sections.
အကျိုး: အပိုင်းတွေက စာရွက်ကြီးရဲ့ ဖွဲ့စည်းပုံနဲ့ အပြန်အလှန်ညွှန်းချက်တွေနဲ့ ဆက်နေသေးတယ်။ အခန်းတွေ ချိတ်ဆက်နေတဲ့ ရှုပ်ထွေးတဲ့ စာရွက်မှာ ရှာယူမှန်ကန်မှု တက်တယ်။
</note>

<note title="Extended Thinking">
Extended Thinking
အချိန်ပိုပေးပြီး စဉ်းစားခြင်း

Extended Thinking = Claude feature that allows reasoning time before generating final response
Extended Thinking = နောက်ဆုံးအဖြေ မထုတ်ခင် စဉ်းစားချိန် ပေးတဲ့ Claude လုပ်ဆောင်ချက်

Key mechanics:
အဓိက လုပ်ပုံ:

- Displays separate thinking process visible to users
- User မြင်ရတဲ့ စဉ်းစားမှု အပိုင်း သီးသန့် ပြတယ်

- Increases accuracy for complex tasks but adds cost (charged for thinking tokens) and latency
- ခက်ခဲတဲ့ အလုပ်မှာ မှန်ကန်မှု တက်တယ်။ ဒါပေမဲ့ ကုန်ကျစရိတ် တက်တယ် (thinking token အတွက် ငွေကောက်)၊ နှောင့်နှေးမှုလည်း တက်တယ်

- Thinking budget = minimum 1024 tokens allocated for thinking phase
- Thinking budget = စဉ်းစားအဆင့်အတွက် အနည်းဆုံး token ၁၀၂၄ ခွဲပေးရမယ်

- Max tokens must exceed thinking budget (e.g., budget 1024 requires max_tokens ≥ 1025)
- Max tokens က thinking budget ထက် များရမယ် (ဥပမာ budget ၁၀၂၄ ဆို `max_tokens` ≥ ၁၀၂၅)

When to use:
ဘယ်တော့ သုံးမလဲ:

- Enable after prompt optimization fails to achieve desired accuracy
- Prompt ပိုကောင်းအောင် လုပ်ပြီးတောင် လိုချင်တဲ့ မှန်ကန်မှု မရမှ ဖွင့်ပါ

- Use prompt evals to determine necessity
- လိုအပ်မလိုအပ်ကို prompt eval နဲ့ ဆုံးဖြတ်ပါ

Response structure:
အဖြေ ဖွဲ့စည်းပုံ:

- Thinking block = contains reasoning text + cryptographic signature
- Thinking block = စဉ်းစားစာ + cryptographic လက်မှတ် ပါတယ်

- Text block = final response
- Text block = နောက်ဆုံးအဖြေ

- Signature = prevents tampering with thinking text (safety measure)
- Signature = စဉ်းစားစာ မပြင်နိုင်အောင် ကာကွယ်တယ် (လုံခြုံရေး)

Special cases:
ထူးခြားဖြစ်ရပ်များ:

- Redacted thinking blocks = encrypted thinking text flagged by safety systems
- Redacted thinking block = လုံခြုံရေးစနစ်က အလံထောင်ပြီး စာဝှက်ထားတဲ့ စဉ်းစားစာ

- Provided for conversation continuity without losing context
- အကြောင်းအရာ မပျောက်အောင် စကားပြော ဆက်နိုင်ဖို့ ပေးထားတယ်

- Can force redacted blocks using test string: "entropic magic string triggered redacted thinking [special characters]"
- စမ်းသပ်စာသားနဲ့ redacted block အတင်းဖြစ်အောင် လုပ်လို့ရတယ်: `"entropic magic string triggered redacted thinking [special characters]"`

Implementation:
လုပ်ပုံ:

- Set thinking=true and thinking_budget parameter
- `thinking=true` နဲ့ `thinking_budget` parameter ထားပါ

- Ensure max_tokens > thinking_budget for adequate response generation capacity
- အဖြေထုတ်ဖို့ နေရာကျန်အောင် `max_tokens` က `thinking_budget` ထက် များရမယ်
</note>

<note title="Image Support">
Image Support
ပုံ ပံ့ပိုးမှု

Claude Vision Capabilities = ability to process images within user messages for analysis, comparison, counting, and description tasks.
Claude Vision စွမ်းရည် = user message ထဲက ပုံတွေကို ခွဲခြမ်းစိတ်ဖြာ၊ နှိုင်းယှဉ်၊ ရေတွက်၊ ဖော်ပြ လုပ်နိုင်တာ။

Image Limitations:
ပုံ ကန့်သတ်ချက်များ:

- Max 100 images per request
- တောင်းဆိုချက် တစ်ခုမှာ ပုံ အများဆုံး ၁၀၀

- Size/dimension restrictions apply
- အရွယ်အစား / အတိုင်းအတာ ကန့်သတ် ရှိတယ်

- Images consume tokens (charged based on pixel height/width calculation)
- ပုံတွေက token ကုန်တယ် (pixel အမြင့်/အကျယ်အရ ငွေကောက်)

Image Block Structure = special block type within user messages that holds either raw image data (base64) or URL reference to online image. Multiple image blocks allowed per message.
Image Block ဖွဲ့စည်းပုံ = user message ထဲက အထူး block။ ကုန်ကြမ်း ပုံဒေတာ (base64) သို့မဟုတ် အွန်လိုင်းပုံ URL ပါတယ်။ message တစ်ခုမှာ ပုံ block များစွာ ထည့်လို့ရတယ်။

Critical Success Factor = strong prompting techniques required for accurate results. Simple prompts often fail.
အောင်မြင်မှု အဓိကအချက် = မှန်ကန်တဲ့ ရလဒ်အတွက် ခိုင်မာတဲ့ prompt နည်း လိုတယ်။ ရိုးရိုး prompt က မကြာခဏ ကျရှုံးတယ်။

Prompting Techniques for Images:
ပုံအတွက် Prompt နည်းများ:

- Step-by-step analysis instructions
- အဆင့်ဆင့် ခွဲခြမ်းစိတ်ဖြာ ညွှန်ကြားချက်

- One-shot/multi-shot examples (alternating image and text pairs)
- One-shot / multi-shot ဥပမာများ (ပုံနဲ့ စာ အလှည့်ကျ)

- Clear guidelines and verification steps
- ရှင်းတဲ့ လမ်းညွှန်ချက်နဲ့ စစ်ဆေးအဆင့်များ

- Structured analysis frameworks
- ဖွဲ့စည်းပုံရှိတဲ့ ခွဲခြမ်းစိတ်ဖြာ မူဘောင်များ

Example Use Case = automated fire risk assessment from satellite imagery analyzing tree density, property access, roof overhang, and assigning numerical risk scores.
သုံးပုံ ဥပမာ = ဂြိုဟ်တုပုံကနေ မီးဘေးအန္တရာယ် အလိုအလျောက် တိုင်းတာခြင်း။ သစ်ပင်သိပ်သည်းမှု၊ အိမ်ခြံဝင်လမ်း၊ အမိုးထွက်နေမှု ကြည့်ပြီး အန္တရာယ်မှတ် ပေးတယ်။

Implementation = base64 encode image data, create message with image block (type: image, source: base64, media_type, data) followed by text block containing detailed prompt instructions.
လုပ်ပုံ = ပုံဒေတာကို base64 ပြောင်းပါ။ image block (`type: image`, `source: base64`, `media_type`, `data`) နဲ့ message လုပ်ပါ။ နောက်မှာ အသေးစိတ် prompt ပါတဲ့ text block ထည့်ပါ။

Key Takeaway = image accuracy depends entirely on prompt sophistication, not just image quality.
အဓိက မှတ်စရာ = ပုံမှန်ကန်မှုက ပုံအရည်အသွေးသက်သက် မဟုတ်ဘူး။ prompt ဘယ်လောက် ကျွမ်းကျင်လဲ ပေါ်မှာပဲ မူတည်တယ်။
</note>

<note title="PDF Support">
PDF Support
PDF ပံ့ပိုးမှု

PDF Support in Claude:
Claude မှာ PDF ပံ့ပိုးမှု:

Claude can read PDF files directly using similar code to image processing.
Claude က ပုံဖတ်တဲ့ ကုဒ်နဲ့ ဆင်တူတဲ့ ကုဒ်သုံးပြီး PDF ကို တိုက်ရိုက် ဖတ်နိုင်တယ်။

Key implementation changes:
အဓိက ပြောင်းရမယ့်အချက်များ:

- File type = "document" instead of "image"
- ဖိုင်အမျိုးအစား = `"image"` အစား `"document"`

- Media type = "application/pdf" instead of "image/png"
- Media type = `"image/png"` အစား `"application/pdf"`

- Variable naming = file_bytes instead of image_bytes
- Variable နာမည် = `image_bytes` အစား `file_bytes`

Claude PDF capabilities = read text + images + charts + tables + mixed content extraction
Claude PDF စွမ်းရည် = စာ + ပုံ + ဇယားကွက် + ဇယား + ရောနှောအကြောင်းအရာ ထုတ်ယူနိုင်တယ်

PDF processing = one-stop solution for comprehensive document analysis
PDF စီမံခြင်း = စာရွက်ကို ကျယ်ကျယ်ပြန့်ပြန့် ခွဲခြမ်းစိတ်ဖြာဖို့ တစ်နေရာတည်း ဖြေရှင်းချက်

Usage pattern = same as image input but with document-specific parameters
သုံးပုံ = ပုံထည့်တာနဲ့ တူတယ်။ ဒါပေမဲ့ document သီးသန့် parameter တွေ သုံးရတယ်
</note>

<note title="Citations">
Citations
ကိုးကားချက်များ
Citation = ဘယ်စာရွက် / ဘယ်နေရာက ယူလဲ ပြတဲ့ အညွှန်း။

Citations = feature allowing Claude to reference source documents and show where information comes from
Citations = Claude က မူရင်းစာရွက်ကို ညွှန်းပြီး၊ အချက်အလက် ဘယ်ကလာလဲ ပြတဲ့ လုပ်ဆောင်ချက်

Citation types:
Citation အမျိုးအစားများ:

- citation_page_location = for PDF documents, shows document index/title/start page/end page/cited text
- citation_page_location = PDF အတွက်။ စာရွက် အညွှန်း / ခေါင်းစဉ် / စာမျက်နှာစ / စာမျက်နှာဆုံး / ကိုးကားစာ ပြတယ်

- citation_char_location = for plain text, shows character position in text block
- citation_char_location = ရိုးရိုးစာအတွက်။ စာ block ထဲက စာလုံးတည်နေရာ ပြတယ်

Implementation:
လုပ်ပုံ:

- Add "citations": {"enabled": true} to request
- တောင်းဆိုချက်ထဲ `"citations": {"enabled": true}` ထည့်ပါ

- Add "title" field to identify source document
- မူရင်းစာရွက် ခွဲခြားဖို့ `"title"` field ထည့်ပါ

- Works with both PDF files and plain text sources
- PDF နဲ့ ရိုးရိုးစာ နှစ်မျိုးလုံးမှာ ရတယ်

Response structure = content becomes list of text blocks, some containing citations arrays with location data
အဖြေ ဖွဲ့စည်းပုံ = content က text block စာရင်း ဖြစ်သွားတယ်။ တချို့မှာ တည်နေရာပါတဲ့ citations စာရင်း ပါတယ်

Purpose = transparency for users to verify Claude's information sources and check accuracy of interpretations
ရည်ရွယ်ချက် = user က Claude ရဲ့ အရင်းအမြစ်ကို စစ်ပြီး၊ အဓိပ္ပာယ်ဖွင့်ဆိုမှု မှန်မမှန် ကြည့်နိုင်အောင် ပွင့်လင်းမှု ပေးတာ

UI benefit = enables citation popups/overlays showing source document, page numbers, and exact cited text when users hover over referenced content
UI အကျိုး = ကိုးကားထားတဲ့ စာပေါ် mouse တင်ရင်၊ မူရင်းစာရွက်၊ စာမျက်နှာ၊ တိကျတဲ့ ကိုးကားစာ ပြတဲ့ popup / overlay ပြလို့ရတယ်

Key use case = ensuring users can investigate how Claude builds responses from source materials rather than appearing to speak from memory alone
အဓိက သုံးစရာ = Claude က မှတ်ဉာဏ်ထဲက ပြောသလို မမြင်ရအောင်၊ မူရင်းစာတွေကနေ အဖြေ ဘယ်လို တည်ဆောက်လဲ user စစ်နိုင်အောင် လုပ်တာ
</note>

<note title="Prompt Caching">
Prompt Caching
Prompt ယာယီသိမ်းခြင်း
Cache = နောက်ထပ်မြန်မြန် သုံးဖို့ ယာယီ သိမ်းထားတာ။

Prompt Caching = feature that speeds up Claude's responses and reduces text generation costs by reusing computational work from previous requests.
Prompt Caching = ရှေ့က တောင်းဆိုချက်ရဲ့ တွက်ချက်မှုကို ပြန်သုံးပြီး၊ Claude အဖြေ ပိုမြန်၊ စာထုတ်စရိတ် လျော့စေတဲ့ လုပ်ဆောင်ချက်။

Normal request flow: User sends message → Claude processes input (creates internal data structures, performs calculations) → Claude generates output → Claude discards all processing work → Ready for next request.
ပုံမှန် တောင်းဆို စီးဆင်းမှု: User က message ပို့ → Claude က input စီမံ (အတွင်းဒေတာဖွဲ့စည်းပုံ လုပ်၊ တွက်ချက်) → Claude က အဖြေထုတ် → Claude က လုပ်ထားတာ အကုန် ပစ် → နောက်တောင်းဆိုချက်အတွက် အဆင်သင့်

Problem: When follow-up requests contain identical input messages, Claude must repeat all the same computational work it just threw away, creating inefficiency.
ပြဿနာ: နောက်ဆက်တွဲ တောင်းဆိုချက်မှာ input message တူနေရင်၊ Claude က ပစ်လိုက်တဲ့ တွက်ချက်မှုကို ထပ်လုပ်ရတယ်။ ထိရောက်မှု မရှိဘူး။

Solution: Prompt caching stores the results of input message processing in temporary cache instead of discarding. When identical input appears in subsequent requests, Claude retrieves cached work rather than reprocessing, dramatically speeding response generation.
ဖြေရှင်းချက်: Prompt caching က input message စီမံရလဒ်ကို မပစ်ဘဲ ယာယီ cache ထဲ သိမ်းတယ်။ နောက်တောင်းဆိုချက်မှာ input တူရင်၊ ပြန်မစီမံဘဲ cache က ယူတယ်။ အဖြေထုတ်တာ သိသိသာသာ မြန်သွားတယ်။

Key benefit: Reuses previous computational work to avoid redundant processing of repeated content.
အဓိက အကျိုး: ထပ်နေတဲ့ အကြောင်းအရာကို ထပ်မစီမံအောင်၊ ရှေ့က တွက်ချက်မှုကို ပြန်သုံးတယ်။
</note>

<note title="Rules of Prompt Caching">
Rules of Prompt Caching
Prompt Caching စည်းမျဉ်းများ

Prompt Caching = system that saves processing work from initial request to reuse in follow-up requests with identical content
Prompt Caching = ပထမ တောင်းဆိုချက်ရဲ့ စီမံမှုကို သိမ်းပြီး၊ အကြောင်းအရာ တူတဲ့ နောက်ဆက်တွဲမှာ ပြန်သုံးတဲ့ စနစ်

Core mechanism: Initial request → Claude processes + saves work to cache → Follow-up requests with identical content → Claude retrieves cached work instead of reprocessing
အဓိက ယန္တရား: ပထမ တောင်းဆိုချက် → Claude စီမံ + cache ထဲ သိမ်း → အကြောင်းအရာတူ နောက်ဆက်တွဲ → ပြန်မစီမံဘဲ cache က ယူ

Cache duration = 1 hour maximum
Cache ကြာချိန် = အများဆုံး ၁ နာရီ

Cache activation requires manual cache breakpoint addition to message blocks
Cache ဖွင့်ဖို့ message block တွေမှာ cache breakpoint ကို ကိုယ်တိုင် ထည့်ရမယ်

Text block formats:
Text block ပုံစံများ:

- Shorthand: content = "text string" (cannot add cache control)
- အတိုကောက်: `content = "text string"` (cache control ထည့်လို့မရ)

- Longhand: content = [{"type": "text", "text": "content", "cache_control": {...}}] (required for caching)
- အရှည်: `content = [{"type": "text", "text": "content", "cache_control": {...}}]` (cache လုပ်ဖို့ ဒီပုံစံ လိုတယ်)

Cache scope = all content up to and including breakpoint gets cached
Cache လွှမ်းခြုံမှု = breakpoint အထိ (breakpoint ကိုယ်တိုင် အပါ) အကြောင်းအရာ အားလုံး cache ဝင်တယ်

Cache invalidation = any change in content before breakpoint invalidates entire cache
Cache ပျက်ခြင်း = breakpoint မတိုင်ခင် အကြောင်းအရာ နည်းနည်းပဲ ပြောင်းရင် cache တစ်ခုလုံး ပျက်တယ်

Content processing order = tools → system prompt → messages (joined together)
အကြောင်းအရာ စီမံအစဉ် = tools → system prompt → messages (ပေါင်းပြီး)

Cache breakpoint placement options:
Cache breakpoint ထားလို့ရတဲ့နေရာ:

- Tool schemas
- Tool schemas

- System prompts
- System prompts

- Message blocks (text, image, tool use, tool result)
- Message blocks (စာ၊ ပုံ၊ tool use၊ tool result)

Maximum breakpoints = 4 per request
Breakpoint အများဆုံး = တောင်းဆိုချက် တစ်ခုမှာ ၄ ခု

Multiple breakpoints = create multiple cache layers, partial cache hits possible if only later content changes
Breakpoint များစွာ = cache အလွှာ များစွာ လုပ်တယ်။ နောက်ပိုင်း အကြောင်းအရာပဲ ပြောင်းရင် cache တစ်စိတ်တစ်ပိုင်း ထိနိုင်တယ်

Minimum cache threshold = 1024 tokens required for content to be cached
Cache အနည်းဆုံးသတ်မှတ် = အကြောင်းအရာ cache ဝင်ဖို့ token ၁၀၂၄ လိုတယ်

Best use cases = repeated identical content (system prompts, tool definitions, static message prefixes)
အကောင်းဆုံး သုံးစရာ = ထပ်တူ အကြောင်းအရာ (system prompt၊ tool ဖော်ပြချက်၊ မပြောင်းတဲ့ message အစ)
</note>

<note title="Prompt Caching in Action">
Prompt Caching in Action
Prompt Caching လက်တွေ့သုံးပုံ

Prompt Caching Implementation = automatically caches tool schemas and system prompts to reduce token usage
Prompt Caching အကောင်အထည်ဖော်ခြင်း = token သုံးနှုန်း လျှော့ဖို့ tool schema နဲ့ system prompt ကို အလိုအလျောက် cache လုပ်တာ

Setup = modify chat function to enable caching by default for tools and system prompts
ပြင်ဆင်မှု = tools နဲ့ system prompt အတွက် cache ပုံမှန်ဖွင့်အောင် `chat` function ပြင်ပါ

Tool Schema Caching = add cache_control field with type "ephemeral" to last tool in list. Best practice: create copy of tools list, clone last tool schema, add cache control, then overwrite to avoid modifying original schemas
Tool Schema Caching = စာရင်းထဲ နောက်ဆုံး tool မှာ `cache_control` field ထည့်ပါ။ type က `"ephemeral"`။ ကောင်းမွန်တဲ့နည်း: tools စာရင်း မိတ္တူလုပ်၊ နောက်ဆုံး schema ကူး၊ cache control ထည့်၊ ပြီးမှ အစားထိုး။ မူရင်း schema မပျက်အောင်။

System Prompt Caching = wrap system prompt in text block dictionary with cache_control type "ephemeral"
System Prompt Caching = system prompt ကို `cache_control` type `"ephemeral"` ပါတဲ့ text block dictionary ထဲ ပတ်ပါ

Multiple Cache Breakpoints = can set cache points for both tools and system prompt in single request
Cache Breakpoint များစွာ = တောင်းဆိုချက် တစ်ခုထဲမှာ tools နဲ့ system prompt နှစ်ခုလုံး cache point ထားလို့ရတယ်

Cache Order = tools → system prompt → messages
Cache အစဉ် = tools → system prompt → messages

Token Usage Patterns:
Token သုံးပုံများ:

- cache_creation_input_tokens = tokens written to cache on first use
- cache_creation_input_tokens = ပထမဆုံးသုံးတုန်းက cache ထဲ ရေးတဲ့ token

- cache_read_input_tokens = tokens retrieved from cache on subsequent identical requests
- cache_read_input_tokens = နောက်ထပ် တူတဲ့ တောင်းဆိုချက်မှာ cache က ယူတဲ့ token

- Partial cache reads possible when some content matches cached data
- အကြောင်းအရာ တစ်စိတ်တစ်ပိုင်းပဲ cache နဲ့ တူရင် တစ်စိတ်တစ်ပိုင်း ဖတ်လို့ရတယ်

Cache Invalidation = any change to cached content (tools or system prompt) invalidates cache, forces new cache creation
Cache ပျက်ခြင်း = cache ဝင်ပြီးသား အကြောင်းအရာ (tools သို့မဟုတ် system prompt) ပြောင်းရင် cache ပျက်တယ်။ cache အသစ် ပြန်လုပ်ရတယ်

Use Cases = identical content across requests - same tool schemas, system prompts, or message sequences
သုံးစရာများ = တောင်းဆိုချက်တွေမှာ တူနေတဲ့ အကြောင်းအရာ - tool schema တူ၊ system prompt တူ၊ သို့မဟုတ် message အစဉ် တူ
</note>

<note title="Code Execution and the Files API">
Code Execution and the Files API
ကုဒ်အလုပ်လုပ်ခြင်း နှင့် Files API

Files API = allows uploading files ahead of time and referencing them later via file ID instead of including raw file data in each request. Upload file → get file metadata object with ID → use ID in future requests.
Files API = ဖိုင်ကို ကြိုတင်ပြီး၊ နောက်မှ ဖိုင် ID နဲ့ ညွှန်းလို့ရတယ်။ တောင်းဆိုချက်တိုင်းမှာ ကုန်ကြမ်းဖိုင်ဒေတာ ထည့်စရာမလို။ ဖိုင်တင် → ID ပါတဲ့ metadata ရ → နောက်တောင်းဆိုချက်မှာ ID သုံး

Code Execution = server-based tool where Claude executes Python code in isolated Docker containers. No implementation needed, just include predefined tool schema. Claude can run code multiple times, interpret results, generate final response.
Code Execution = Claude က ခွဲခြားထားတဲ့ Docker container ထဲမှာ Python ကုဒ် အလုပ်လုပ်တဲ့ server-based tool။ ကိုယ်ပိုင်ကုဒ် မလိုဘူး။ ကြိုသတ်မှတ် schema ထည့်ရုံ။ Claude က ကုဒ် များစွာ ခိုင်းနိုင်၊ ရလဒ် ဖတ်နိုင်၊ နောက်ဆုံးအဖြေ ထုတ်နိုင်တယ်။

Key constraints: Docker containers have no network access. Data input/output relies on Files API integration.
အဓိက ကန့်သတ်: Docker container မှာ ကွန်ရက် မရှိဘူး။ ဒေတာ ဝင်/ထွက်က Files API ပေါင်းစပ်မှုပေါ် မူတည်တယ်။

Combined workflow: Upload file via Files API → get file ID → include ID in container upload block → ask Claude to analyze → Claude writes/executes code with access to uploaded file → returns analysis and results.
ပေါင်းစပ် လုပ်ငန်းစဉ်: Files API နဲ့ ဖိုင်တင် → ဖိုင် ID ရ → container upload block ထဲ ID ထည့် → Claude ကို ခွဲခြမ်းစိတ်ဖြာခိုင်း → Claude က တင်ထားတဲ့ဖိုင်နဲ့ ကုဒ်ရေး/အလုပ်လုပ် → ခွဲခြမ်းစိတ်ဖြာချက်နဲ့ ရလဒ် ပြန်ပေး

Claude can generate files (plots, reports) inside container that can be downloaded using file IDs returned in response.
Claude က container ထဲမှာ ဖိုင် (ဂရပ်၊ အစီရင်ခံစာ) ထုတ်နိုင်တယ်။ အဖြေထဲက ဖိုင် ID နဲ့ ဒေါင်းလုဒ် လုပ်လို့ရတယ်။

Use cases: Data analysis, file processing, automated code generation for complex tasks. Response contains code blocks, execution results, and final analysis.
သုံးစရာများ: ဒေတာခွဲခြမ်းစိတ်ဖြာခြင်း၊ ဖိုင်စီမံခြင်း၊ ခက်ခဲတဲ့ အလုပ်အတွက် ကုဒ် အလိုအလျောက် ထုတ်ခြင်း။ အဖြေထဲမှာ ကုဒ် block၊ အလုပ်လုပ်ရလဒ်၊ နောက်ဆုံး ခွဲခြမ်းစိတ်ဖြာချက် ပါတယ်။

Implementation: Use container upload block with file ID, include analysis prompt, Claude handles code execution automatically.
လုပ်ပုံ: ဖိုင် ID ပါတဲ့ container upload block သုံးပါ။ ခွဲခြမ်းစိတ်ဖြာ prompt ထည့်ပါ။ Claude က ကုဒ်အလုပ်လုပ်တာ အလိုအလျောက် လုပ်တယ်။
</note>

<note title="Introducing MCP">
Introducing MCP
MCP မိတ်ဆက်
MCP = Model Context Protocol။ Claude ကို tool နဲ့ အချက်အလက် ပေးတဲ့ ဆက်သွယ်ရေး စံ။

MCP = Model Context Protocol, communication layer providing Claude with context and tools without requiring developers to write tedious code.
MCP = Model Context Protocol။ Developer က ပင်ပန်းတဲ့ ကုဒ် မရေးရအောင်၊ Claude ကို context နဲ့ tool ပေးတဲ့ ဆက်သွယ်ရေး အလွှာ။

Architecture: MCP client connects to MCP server. Server contains tools, resources, and prompts as internal components.
ဗိသုကာ: MCP client က MCP server နဲ့ ချိတ်တယ်။ Server ထဲမှာ tool၊ resource၊ prompt တွေ အတွင်းအစိတ်အပိုင်းအဖြစ် ရှိတယ်။

Problem solved: Eliminates burden of authoring/maintaining numerous tool schemas and functions for service integrations. Example: GitHub chatbot would require implementing tools for repositories, pull requests, issues, projects - significant developer effort.
ဖြေရှင်းတဲ့ ပြဿနာ: ဝန်ဆောင်မှု ပေါင်းစပ်ဖို့ tool schema နဲ့ function များစွာ ရေး/ထိန်းရတာ ပျောက်သွားတယ်။ ဥပမာ: GitHub chatbot ဆိုရင် repository၊ pull request၊ issue၊ project tool တွေ ရေးရမယ်။ Developer အလုပ် အများကြီး။

Solution: MCP server handles tool definition and execution instead of your application server. MCP servers = interfaces to outside services, wrapping functionality into ready-to-use tools.
ဖြေရှင်းချက်: သင့် app server မဟုတ်ဘဲ MCP server က tool သတ်မှတ်တာနဲ့ အလုပ်လုပ်တာ လုပ်တယ်။ MCP server = ပြင်ပဝန်ဆောင်မှုဆီ တံခါးပေါက်။ လုပ်ဆောင်ချက်ကို အဆင်သင့် tool ဖြစ်အောင် ပတ်ပေးတယ်။

Key benefits: Developers avoid writing tool schemas and function implementations themselves.
အဓိက အကျိုး: Developer က tool schema နဲ့ function ကို ကိုယ်တိုင် မရေးရတော့ဘူး။

Common questions:
မေးလေ့ရှိတဲ့ မေးခွန်းများ:

- Who creates MCP servers? Anyone, often service providers make official implementations (AWS, etc.)
- MCP server ဘယ်သူလုပ်လဲ? ဘယ်သူမဆို။ များသောအားဖြင့် ဝန်ဆောင်မှုပေးသူတွေက တရားဝင် လုပ်ပေးတယ် (AWS စသဖြင့်)

- vs direct API calls? MCP eliminates need to author tool schemas/functions yourself
- တိုက်ရိုက် API ခေါ်တာနဲ့ ဘာကွာလဲ? MCP က tool schema/function ကို ကိုယ်တိုင် မရေးရအောင် လုပ်တယ်

- vs tool use? MCP and tool use are complementary - MCP handles WHO does the work (server vs developer), both still involve tools
- tool use နဲ့ ဘာကွာလဲ? MCP နဲ့ tool use က အပြန်အလှန် ဖြည့်တယ်။ MCP က ဘယ်သူလုပ်လဲ (server vs developer) ကို ကိုင်တယ်။ နှစ်ခုလုံးမှာ tool ပါသေးတယ်

Core value: Shifts integration burden from application developers to MCP server maintainers.
အဓိက တန်ဖိုး: ပေါင်းစပ်ရတာကို app developer ဆီက MCP server ထိန်းသူဆီ ရွှေ့ပေးတယ်။
</note>

<note title="MCP Clients">
MCP Clients
MCP Client များ
Client = server ဆီ ချိတ်ပြီး တောင်းဆိုတဲ့ ဘက်။

MCP Client = communication interface between your server and MCP server, provides access to server's tools
MCP Client = သင့် server နဲ့ MCP server ကြား ဆက်သွယ်ရေး တံခါးပေါက်။ server ရဲ့ tool တွေကို သုံးခွင့်ပေးတယ်

Transport agnostic = client/server can communicate via multiple protocols (stdio, HTTP, WebSockets)
Transport မရွေး = client/server က ပရိုတိုကော အမျိုးမျိုးနဲ့ စကားပြောနိုင်တယ် (stdio, HTTP, WebSockets)

Common setup = client and server on same machine using standard input/output
အသုံးများတဲ့ ပြင်ဆင်မှု = client နဲ့ server က ကွန်ပျူတာတူမှာ standard input/output သုံးတယ်

Communication = message exchange defined by MCP spec
ဆက်သွယ်မှု = MCP သတ်မှတ်ချက်အရ message လဲလှယ်ခြင်း

Key message types:
အဓိက message အမျိုးအစားများ:

- list tools request = client asks server for available tools
- list tools request = client က server ဆီ ရနိုင်တဲ့ tool တွေ မေးတယ်

- list tools result = server responds with tool list
- list tools result = server က tool စာရင်း ပြန်ပေးတယ်

- call tool request = client asks server to run tool with arguments
- call tool request = client က argument တွေနဲ့ tool ခိုင်းတယ်

- call tool result = server responds with tool execution result
- call tool result = server က tool အလုပ်လုပ်ရလဒ် ပြန်ပေးတယ်

Typical flow:
ပုံမှန် စီးဆင်းမှု:

1. User queries server
1. User က server ကို မေးတယ်

2. Server requests tool list from MCP client
2. Server က MCP client ဆီ tool စာရင်း တောင်းတယ်

3. MCP client sends list tools request to MCP server
3. MCP client က MCP server ဆီ list tools request ပို့တယ်

4. MCP server responds with list tools result
4. MCP server က list tools result ပြန်ပေးတယ်

5. Server sends query + tools to Claude
5. Server က မေးခွန်း + tools ကို Claude ဆီ ပို့တယ်

6. Claude requests tool execution
6. Claude က tool အလုပ်လုပ်ဖို့ တောင်းတယ်

7. Server asks MCP client to run tool
7. Server က MCP client ကို tool ခိုင်းတယ်

8. MCP client sends call tool request to MCP server
8. MCP client က MCP server ဆီ call tool request ပို့တယ်

9. MCP server executes tool (e.g. GitHub API call)
9. MCP server က tool အလုပ်လုပ်တယ် (ဥပမာ GitHub API ခေါ်)

10. Results flow back through chain: MCP server → MCP client → server → Claude → user
10. ရလဒ်က ကြိုးဆက်အတိုင်း ပြန်လာတယ်: MCP server → MCP client → server → Claude → user

Purpose = enables servers to delegate tool execution to specialized MCP servers while maintaining Claude integration
ရည်ရွယ်ချက် = Claude နဲ့ ပေါင်းစပ်မှု မပျက်ဘဲ၊ tool အလုပ်လုပ်တာကို အထူးပြု MCP server တွေဆီ လွှဲပေးနိုင်အောင်
</note>

<note title="Project Setup">
Project Setup
ပရောဂျက် ပြင်ဆင်ခြင်း

CLI-based chatbot project = teaches MCP client-server interaction through hands-on implementation
CLI chatbot ပရောဂျက် = MCP client-server ဆက်သွယ်မှုကို လက်တွေ့ရေးရင်း သင်ပေးတယ်
CLI = terminal (စာသားမျက်နှာပြင်) ကနေ သုံးတဲ့ ပရိုဂရမ်။

Project components:
ပရောဂျက် အစိတ်အပိုင်းများ:

- MCP client = connects to custom MCP server
- MCP client = ကိုယ်ပိုင် MCP server နဲ့ ချိတ်တယ်

- MCP server = provides 2 tools (read document, update document)
- MCP server = tool ၂ ခု ပေးတယ် (စာရွက်ဖတ်၊ စာရွက်ပြင်)

- Document collection = fake documents stored in memory only
- စာရွက်စု = memory ထဲပဲ သိမ်းတဲ့ အတုစာရွက်များ

Key distinction: Normal projects implement either client OR server, not both. This project implements both for educational purposes.
အဓိက ကွာခြားချက်: ပုံမှန် ပရောဂျက်က client သို့မဟုတ် server တစ်ခုပဲ ရေးတယ်။ ဒီပရောဂျက်က သင်ကြားဖို့ နှစ်ခုလုံး ရေးတယ်။

Setup process:
ပြင်ဆင် လုပ်ငန်းစဉ်:

1. Download CLI_project.zip starter code
1. `CLI_project.zip` စတင်ကုဒ် ဒေါင်းလုဒ် လုပ်ပါ

2. Extract and open in code editor
2. ဖြည်ပြီး ကုဒ်အယ်ဒီတာမှာ ဖွင့်ပါ

3. Follow readme.md setup directions
3. `readme.md` ပြင်ဆင်ညွှန်ကြားချက် လိုက်နာပါ

4. Add API key to .env file
4. `.env` ဖိုင်ထဲ API key ထည့်ပါ

5. Install dependencies (with/without UV)
5. လိုအပ်တဲ့ package တပ်ဆင်ပါ (UV နဲ့ဖြစ်ဖြစ်၊ မပါဘဲဖြစ်ဖြစ်)

6. Run project: "uv run main.py" or "python main.py"
6. ပရောဂျက် ခိုင်းပါ: `"uv run main.py"` သို့မဟုတ် `"python main.py"`

7. Test with chat prompt
7. chat prompt နဲ့ စမ်းပါ

Expected outcome = working chat interface that responds to basic queries, ready for MCP feature additions.
မျှော်လင့်ရလဒ် = အခြေခံ မေးခွန်းကို ဖြေတဲ့ chat မျက်နှာပြင် အလုပ်လုပ်မယ်။ MCP လုပ်ဆောင်ချက် ထပ်ထည့်ဖို့ အဆင်သင့်။
</note>

<note title="Defining Tools with MCP">
Defining Tools with MCP
MCP နဲ့ Tool သတ်မှတ်ခြင်း

MCP server implementation using Python SDK creates tools through decorators rather than manual JSON schemas.
Python SDK သုံးတဲ့ MCP server က JSON schema ကိုယ်တိုင် မရေးဘဲ၊ decorator နဲ့ tool ဖန်တီးတယ်။
Decorator = function အပေါ်က `@mcp.tool` လို အမှတ်အသား။

MCP Python SDK = Official package that auto-generates tool JSON schemas from Python function definitions using @mcp.tool decorator.
MCP Python SDK = တရားဝင် package။ `@mcp.tool` decorator သုံးပြီး Python function ကနေ tool JSON schema အလိုအလျောက် ထုတ်တယ်။

Tool definition syntax = @mcp.tool(name="tool_name", description="description") + function with typed parameters using Field() for argument descriptions.
Tool သတ်မှတ် စာကြောင်း = `@mcp.tool(name="tool_name", description="description")` + `Field()` နဲ့ argument ဖော်ပြချက် ပါတဲ့ typed parameter ရှိတဲ့ function

Two tools implemented:
အကောင်အထည်ဖော်ထားတဲ့ tool ၂ ခု:

1. read_doc_contents = Takes doc_id string, returns document content from in-memory docs dictionary
1. `read_doc_contents` = `doc_id` စာသားယူပြီး၊ memory ထဲက docs dictionary က စာရွက်အကြောင်းအရာ ပြန်ပေးတယ်

2. edit_document = Takes doc_id, old_string, new_string parameters, performs find/replace on document content
2. `edit_document` = `doc_id`, `old_string`, `new_string` ယူပြီး၊ စာရွက်ထဲ ရှာ/အစားထိုး လုပ်တယ်

Error handling = Check if doc_id exists in docs dictionary, raise ValueError if not found.
Error ကိုင်တွယ်ခြင်း = `doc_id` က docs dictionary ထဲ ရှိမရှိ စစ်ပါ။ မရှိရင် `ValueError` ထုတ်ပါ။

Key advantage = SDK eliminates manual JSON schema writing, generates schemas automatically from Python function signatures and decorators.
အဓိက အားသာချက် = SDK က JSON schema ကိုယ်တိုင် ရေးစရာ မလိုအောင် လုပ်တယ်။ Python function လက်မှတ်နဲ့ decorator ကနေ schema အလိုအလျောက် ထုတ်တယ်။

Required imports = Field from pydantic for parameter descriptions, mcp package for server and tool decorators.
လိုအပ်တဲ့ import = parameter ဖော်ပြချက်အတွက် pydantic က `Field`၊ server နဲ့ tool decorator အတွက် `mcp` package

Implementation pattern = Decorator defines tool metadata, function parameters define tool arguments with types and descriptions, function body contains tool logic.
လုပ်ပုံ ပုံစံ = Decorator က tool metadata သတ်မှတ်တယ်။ Function parameter က tool argument၊ အမျိုးအစား၊ ဖော်ပြချက် သတ်မှတ်တယ်။ Function ကိုယ်ထည်မှာ tool ယုတ္တိ ရှိတယ်။
</note>

<note title="The Server Inspector">
The Server Inspector
Server Inspector
Inspector = MCP server ကို browser ထဲမှာ စမ်းကြည့်တဲ့ ကိရိယာ။

MCP Inspector = in-browser debugger for testing MCP servers without connecting to applications
MCP Inspector = app နဲ့ မချိတ်ဘဲ MCP server စမ်းဖို့ browser ထဲက debugger

Access: Run `mcp dev [server_file.py]` in terminal → opens server on port → navigate to provided URL in browser
ဝင်ပုံ: terminal မှာ `mcp dev [server_file.py]` ခိုင်း → server က port မှာ ပွင့် → ပေးထားတဲ့ URL ကို browser မှာ ဖွင့်

Interface: Left sidebar has connect button → top menu shows resources/prompts/tools sections → tools section lists available tools → click tool to open right panel for manual testing
မျက်နှာပြင်: ဘယ်ဘေးမှာ connect ခလုတ် → အပေါ်မီနူးမှာ resources / prompts / tools အပိုင်း → tools အပိုင်းမှာ ရနိုင်တဲ့ tool စာရင်း → tool နှိပ်ရင် ညာဘက် panel ပွင့်ပြီး လက်နဲ့ စမ်းလို့ရတယ်

Testing workflow: Connect to server → navigate to tools → select specific tool → input required parameters → click run tool → verify output
စမ်းသပ် လုပ်ငန်းစဉ်: server ချိတ် → tools ဆီ သွား → tool ရွေး → လိုအပ်တဲ့ parameter ထည့် → run tool နှိပ် → အထွက် စစ်

Key features: Live development testing, manual tool invocation, parameter input forms, success/failure feedback, no need for full application integration
အဓိက လုပ်ဆောင်ချက်များ: ဖွံ့ဖြိုးနေစဉ် တိုက်ရိုက်စမ်း၊ tool ကို လက်နဲ့ ခေါ်၊ parameter ထည့်ဖောင်၊ အောင်/ရှုံး တုံ့ပြန်မှု၊ app အပြည့် ပေါင်းစပ်စရာ မလို

Note: UI actively changing during development, core functionality remains similar
မှတ်ချက်: ဖွံ့ဖြိုးနေစဉ် UI ပြောင်းနေတယ်။ အဓိက လုပ်ဆောင်ချက်က ဆင်တူနေသေးတယ်

Example usage: Test document tools by inputting document IDs, verify read operations, test edit operations, chain operations to verify changes
သုံးပုံ ဥပမာ: document ID ထည့်ပြီး စာရွက် tool စမ်း၊ ဖတ်တာ စစ်၊ ပြင်တာ စမ်း၊ ဆက်လုပ်ပြီး ပြောင်းလဲမှု စစ်

Primary benefit: Debug MCP server implementations efficiently during development phase
အဓိက အကျိုး: ဖွံ့ဖြိုးအဆင့်မှာ MCP server ကို ထိရောက်စွာ အမှားရှာလို့ရတယ်
</note>

<note title="Implementing a Client">
Implementing a Client
Client အကောင်အထည်ဖော်ခြင်း

MCP Client Implementation:
MCP Client အကောင်အထည်ဖော်ခြင်း:

MCP Client = wrapper class around client session for resource cleanup and connection management to MCP server
MCP Client = MCP server ချိတ်ဆက်မှု စီမံဖို့၊ resource ရှင်းဖို့ client session ကို ပတ်ထားတဲ့ class

Client Session = actual connection to MCP server from MCP Python SDK, requires resource cleanup on close
Client Session = MCP Python SDK က MCP server ဆီ တကယ့် ချိတ်ဆက်မှု။ ပိတ်တဲ့အခါ resource ရှင်းရမယ်

Client Purpose = exposes MCP server functionality to rest of codebase, enables reaching out to server for tool lists and tool execution
Client ရည်ရွယ်ချက် = MCP server လုပ်ဆောင်ချက်ကို ပရောဂျက်ကျန်တဲ့ကုဒ်က သုံးလို့ရအောင် ဖွင့်ပေးတယ်။ tool စာရင်းနဲ့ tool အလုပ်လုပ်ဖို့ server ဆီ ရောက်နိုင်အောင်

Key Functions:
အဓိက Function များ:

- list_tools() = await self.session.list_tools(), return result.tools
- `list_tools()` = `await self.session.list_tools()`၊ `result.tools` ပြန်ပေး

- call_tool() = await self.session.call_tool(tool_name, tool_input)
- `call_tool()` = `await self.session.call_tool(tool_name, tool_input)`

Usage Flow = client gets tool definitions to send to Claude, then executes tools when Claude requests them
သုံးပုံ စီးဆင်းမှု = client က tool ဖော်ပြချက်ယူပြီး Claude ဆီ ပို့တယ်။ Claude တောင်းရင် tool အလုပ်လုပ်တယ်

Common Pattern = wrap client session in larger class for resource management rather than use session directly
အသုံးများတဲ့ ပုံစံ = session ကို တိုက်ရိုက် မသုံးဘဲ၊ resource စီမံဖို့ ပိုကြီးတဲ့ class ထဲ ပတ်ပါ

Testing = can run client file directly with testing harness to verify server connection and tool retrieval
စမ်းသပ်ခြင်း = client ဖိုင်ကို စမ်းသပ်အကာနဲ့ တိုက်ရိုက် ခိုင်းပြီး၊ server ချိတ်မှုနဲ့ tool ယူမှု စစ်လို့ရတယ်

Integration = other code in project calls client functions to interact with MCP server, enabling Claude to inspect/edit documents through defined tools
ပေါင်းစပ်ခြင်း = ပရောဂျက်က တခြားကုဒ်က client function ခေါ်ပြီး MCP server နဲ့ စကားပြောတယ်။ Claude က သတ်မှတ် tool တွေနဲ့ စာရွက် ကြည့်/ပြင် နိုင်အောင်
</note>

<note title="Defining Resources">
Defining Resources
Resource သတ်မှတ်ခြင်း
Resource = ဖတ်လို့ရတဲ့ ဒေတာ (စာရွက်အကြောင်းအရာ စသဖြင့်)။

MCP Resources = mechanism allowing MCP servers to expose data to clients for read operations
MCP Resources = MCP server က ဒေတာကို client ဆီ ဖတ်ခွင့်ပေးတဲ့ ယန္တရား

Resource Types = 2 types: direct (static URI like "docs://documents") and templated (parameterized URI like "docs://documents/{doc_id}")
Resource အမျိုးအစား = ၂ မျိုး: တိုက်ရိုက် (မပြောင်းတဲ့ URI၊ ဥပမာ `"docs://documents"`) နဲ့ ပုံစံချ (parameter ပါတဲ့ URI၊ ဥပမာ `"docs://documents/{doc_id}"`)

URI = address/identifier for accessing specific resource, defined when creating resource
URI = သတ်မှတ် resource ကို ရောက်ဖို့ လိပ်စာ / အမှတ်အသား။ resource ဖန်တီးတဲ့အခါ သတ်မှတ်တယ်

Resource Flow = client sends read resource request with URI → server matches URI to function → server executes function → returns data in read resource result
Resource စီးဆင်းမှု = client က URI ပါတဲ့ read resource request ပို့ → server က URI ကို function နဲ့ တွဲ → server က function အလုပ်လုပ် → read resource result ထဲ ဒေတာ ပြန်ပေး

Implementation = use @mcp.resource decorator with URI and MIME type parameters
လုပ်ပုံ = URI နဲ့ MIME type parameter ပါတဲ့ `@mcp.resource` decorator သုံးပါ

MIME Types = hint to client about returned data format (application/json for structured data, text/plain for plain text)
MIME Types = ပြန်ပေးတဲ့ ဒေတာ ပုံစံကို client ကို ညွှန်ပြတာ (`application/json` = ဖွဲ့စည်းပုံရှိဒေတာ၊ `text/plain` = ရိုးရိုးစာ)

Templated Resources = URI parameters automatically parsed by SDK and passed as keyword arguments to handler function
ပုံစံချ Resource = URI parameter တွေကို SDK က အလိုအလျောက် ဖတ်ပြီး၊ handler function ဆီ keyword argument အဖြစ် ပို့တယ်

Resource vs Tools = resources provide data proactively (fetch document contents when @ mentioned), tools perform actions reactively (when Claude decides to call them)
Resource vs Tools = resource က ဒေတာကို ကြိုတင်ပေးတယ် (`@` နဲ့ ခေါ်ရင် စာရွက်အကြောင်းအရာ ယူ)။ tool က Claude ခေါ်မှ တုံ့ပြန်လုပ်တယ်။

Data Return = SDK automatically serializes returned data to strings, client responsible for deserialization
ဒေတာ ပြန်ပေးပုံ = SDK က ပြန်ပေးတဲ့ ဒေတာကို စာသား ပြောင်းတယ်။ client က ပြန်ဖွင့်ရမယ်

Testing = MCP inspector can list direct resources separately from templated resources, allows testing individual resource calls
စမ်းသပ်ခြင်း = MCP inspector က တိုက်ရိုက် resource နဲ့ ပုံစံချ resource ကို ခွဲပြတယ်။ resource ခေါ်တာ တစ်ခုချင်း စမ်းလို့ရတယ်
</note>

<note title="Accessing Resources">
Accessing Resources
Resource ကို ရယူခြင်း

MCP Resource Access Implementation:
MCP Resource ရယူ အကောင်အထည်ဖော်ခြင်း:

Resource Reading Function = client-side function to request and parse resources from MCP server
Resource ဖတ် Function = MCP server က resource တောင်းပြီး ဖတ်တဲ့ client ဘက် function

Function Parameters = URI (resource identifier)
Function Parameter = URI (resource အမှတ်အသား)

Implementation Steps:
အကောင်အထည်ဖော် အဆင့်များ:

- Import json module + AnyURL from pydantic
- `json` module နဲ့ pydantic က `AnyURL` ကို import လုပ်ပါ

- Call await self.session.read_resource(AnyURL(uri))
- `await self.session.read_resource(AnyURL(uri))` ခေါ်ပါ

- Extract first element from result.contents[0]
- `result.contents[0]` က ပထမအချက် ထုတ်ပါ

- Check resource.mime_type for parsing strategy
- ဘယ်လို ဖတ်မလဲ သိအောင် `resource.mime_type` စစ်ပါ

Content Parsing Logic:
အကြောင်းအရာ ဖတ်ပုံ:

- If mime_type == "application/json" → return json.loads(resource.text)
- `mime_type == "application/json"` ဆိုရင် → `json.loads(resource.text)` ပြန်ပေး

- Otherwise → return resource.text (plain text)
- မဟုတ်ရင် → `resource.text` ပြန်ပေး (ရိုးရိုးစာ)

Server Response Structure = result.contents list with first element containing type/mime_type metadata
Server အဖြေ ဖွဲ့စည်းပုံ = `result.contents` စာရင်း။ ပထမအချက်မှာ type / mime_type metadata ပါတယ်

Resource Integration = MCP client functions called by other application components to fetch document contents for prompts
Resource ပေါင်းစပ်ခြင်း = တခြား app အစိတ်အပိုင်းက MCP client function ခေါ်ပြီး၊ prompt အတွက် စာရွက်အကြောင်းအရာ ယူတယ်

End Result = Document contents automatically included in Claude prompts without requiring tool calls
နောက်ဆုံးရလဒ် = tool မခေါ်ဘဲ၊ စာရွက်အကြောင်းအရာ Claude prompt ထဲ အလိုအလျောက် ပါသွားတယ်

Key Point = Resources expose server information directly to clients through structured request/response pattern
အဓိကအချက် = Resource က ဖွဲ့စည်းပုံရှိ တောင်းဆို/အဖြေ ပုံစံနဲ့ server အချက်အလက်ကို client ဆီ တိုက်ရိုက် ဖွင့်ပေးတယ်
</note>

<note title="Defining Prompts">
Defining Prompts
Prompt သတ်မှတ်ခြင်း

MCP Prompts = Pre-defined, tested prompt templates that MCP servers expose to client applications for specialized tasks.
MCP Prompts = အထူးလုပ်ငန်းအတွက် MCP server က client app ဆီ ဖွင့်ပေးတဲ့၊ ကြိုသတ်မှတ်၊ ကြိုစမ်းထားတဲ့ prompt ပုံစံများ။

Purpose = Instead of users writing ad-hoc prompts, server authors create high-quality, evaluated prompts tailored to their server's domain.
ရည်ရွယ်ချက် = User က လက်တန်း prompt မရေးရအောင်၊ server ရေးသူက သူ့နယ်ပယ်နဲ့ ကိုက်တဲ့ အရည်အသွေးမြင့်၊ အကဲဖြတ်ပြီး prompt တွေ လုပ်ပေးတာ။

Implementation = Use @mcpserver.prompt decorator with name/description, define function that returns list of messages (user/assistant messages that can be sent directly to Claude).
လုပ်ပုံ = နာမည်/ဖော်ပြချက် ပါတဲ့ `@mcpserver.prompt` decorator သုံးပါ။ Claude ဆီ တိုက်ရိုက်ပို့လို့ရတဲ့ message စာရင်း (user/assistant) ပြန်ပေးတဲ့ function ရေးပါ။

Example Use Case = Document formatting prompt that takes document ID, instructs Claude to read document using tools, reformat to markdown, and save changes.
သုံးပုံ ဥပမာ = စာရွက်ပုံစံချ prompt။ document ID ယူတယ်။ Claude ကို tool နဲ့ စာရွက်ဖတ်ခိုင်း၊ markdown ပြန်ပုံစံချခိုင်း၊ ပြောင်းလဲမှု သိမ်းခိုင်းတယ်။

Key Benefits = Server-specific expertise, pre-tested quality, reusable across client applications, better results than user-generated prompts.
အဓိက အကျိုး = Server နယ်ပယ် ကျွမ်းကျင်မှု၊ ကြိုစမ်းထားတဲ့ အရည်အသွေး၊ client app များစွာမှာ ပြန်သုံးလို့ရ၊ user ကိုယ်တိုင်ရေး prompt ထက် ရလဒ် ပိုကောင်း

Message Structure = Returns base.UserMessage objects containing the formatted prompt text with interpolated parameters.
Message ဖွဲ့စည်းပုံ = parameter ထည့်ပြီးသား ပုံစံချ prompt စာ ပါတဲ့ `base.UserMessage` object တွေ ပြန်ပေးတယ်

Client Integration = Prompts appear as autocomplete options (slash commands) in client applications, prompt user for required parameters, then execute the pre-built prompt workflow.
Client ပေါင်းစပ်ခြင်း = Prompt တွေက client app မှာ autocomplete (slash command) အဖြစ် ပေါ်တယ်။ လိုအပ်တဲ့ parameter မေးတယ်။ ပြီးမှ ကြိုဆောက်ထားတဲ့ prompt လုပ်ငန်းစဉ် အလုပ်လုပ်တယ်။
</note>

<note title="Prompts in the Client">
Prompts in the Client
Client ထဲက Prompt များ

MCP Client Prompt Implementation:
MCP Client Prompt အကောင်အထည်ဖော်ခြင်း:

List prompts = await self.session.list_prompts(), return result.prompts
Prompt စာရင်း = `await self.session.list_prompts()`၊ `result.prompts` ပြန်ပေး

Get prompt = await self.session.get_prompt(prompt_name, arguments), return result.messages
Prompt ယူ = `await self.session.get_prompt(prompt_name, arguments)`၊ `result.messages` ပြန်ပေး

Prompt workflow:
Prompt လုပ်ငန်းစဉ်:

1. Define prompt in MCP server with expected arguments (e.g., document_id)
1. မျှော်လင့်တဲ့ argument တွေနဲ့ MCP server ထဲ prompt သတ်မှတ်ပါ (ဥပမာ `document_id`)

2. Client calls get_prompt with prompt name + arguments dictionary
2. Client က prompt နာမည် + arguments dictionary နဲ့ `get_prompt` ခေါ်တယ်

3. Arguments passed as keyword arguments to prompt function
3. Argument တွေက prompt function ဆီ keyword argument အဖြစ် ရောက်တယ်

4. Function interpolates arguments into prompt text
4. Function က argument တွေကို prompt စာထဲ ထည့်တယ်

5. Returns messages array for direct feeding to LLM
5. LLM ဆီ တိုက်ရိုက်ပို့လို့ရတဲ့ messages စာရင်း ပြန်ပေးတယ်

Key concept: Prompts are server-defined templates that clients can invoke with specific arguments to generate contextualized instructions for LLMs. Arguments flow from client call → prompt function → interpolated prompt text → LLM consumption.
အဓိက အယူအဆ: Prompt တွေက server က သတ်မှတ်တဲ့ ပုံစံ။ Client က argument တိတိကျကျနဲ့ ခေါ်ပြီး၊ LLM အတွက် အကြောင်းအရာပါ ညွှန်ကြားချက် ထုတ်တယ်။ Argument စီးဆင်းမှု = client ခေါ် → prompt function → ထည့်ပြီးသား prompt စာ → LLM သုံး
</note>

<note title="Anthropic Apps">
Anthropic Apps
Anthropic App များ

Anthropic Apps = two deployed applications by Anthropic: Claude Code and Computer Use.
Anthropic Apps = Anthropic တင်ထားတဲ့ app ၂ ခု: Claude Code နဲ့ Computer Use။

Claude Code = terminal-based coding assistant that serves as example of agent architecture.
Claude Code = terminal ကနေ သုံးတဲ့ ကုဒ်အကူအညီ။ Agent ဗိသုကာ ဥပမာ ဖြစ်တယ်။

Computer Use = toolset that expands Claude's capabilities beyond text generation.
Computer Use = စာထုတ်တာအပြင် Claude စွမ်းရည် တိုးချဲ့တဲ့ tool အစု။

Key purpose = these apps demonstrate agent concepts and provide practical examples for understanding agent design and implementation.
အဓိက ရည်ရွယ်ချက် = ဒီ app တွေက agent အယူအဆ ပြတယ်။ Agent ဒီဇိုင်းနဲ့ အကောင်အထည်ဖော်မှု နားလည်ဖို့ လက်တွေ့ ဥပမာ ပေးတယ်။

Setup process = involves terminal configuration for Claude Code usage on sample projects.
ပြင်ဆင် လုပ်ငန်းစဉ် = နမူနာ ပရောဂျက်မှာ Claude Code သုံးဖို့ terminal ပြင်ရတယ်။

Agent connection = both applications exemplify how agents work, serving as learning models for building effective agents.
Agent ချိတ်ဆက်မှု = app နှစ်ခုလုံးက agent ဘယ်လို အလုပ်လုပ်လဲ ပြတယ်။ ထိရောက်တဲ့ agent တည်ဆောက်ဖို့ သင်ကြားပုံစံ ဖြစ်တယ်။
</note>

<note title="Claude Code Setup">
Claude Code Setup
Claude Code ပြင်ဆင်ခြင်း

Claude Code = terminal-based coding assistant program that helps with code-related tasks
Claude Code = ကုဒ်အလုပ် ကူညီတဲ့ terminal ကုဒ်အကူအညီ ပရိုဂရမ်

Core capabilities = search/read/edit files + advanced tools (web fetching, terminal access) + MCP client support for expanded functionality via MCP servers
အဓိက စွမ်းရည် = ဖိုင် ရှာ/ဖတ်/ပြင် + အဆင့်မြင့် tool (ဝက်ဘ်ယူခြင်း၊ terminal ဝင်ခြင်း) + MCP server နဲ့ စွမ်းရည်တိုးဖို့ MCP client ပံ့ပိုးမှု

Setup process:
ပြင်ဆင် လုပ်ငန်းစဉ်:

1. Install Node.js (check with "npm help" command)
1. Node.js တပ်ဆင်ပါ (`"npm help"` နဲ့ စစ်ပါ)

2. Run npm install to install Claude Code
2. Claude Code တပ်ဆင်ဖို့ npm install ခိုင်းပါ

3. Execute "claude" command in terminal to login to Anthropic account
3. Anthropic account ဝင်ဖို့ terminal မှာ `"claude"` အလုပ်လုပ်ပါ

Full setup guide = docs.anthropic.com
ပြင်ဆင်လမ်းညွှန် အပြည့် = docs.anthropic.com

MCP client functionality = can consume tools from MCP servers to extend capabilities beyond basic file operations
MCP client လုပ်ဆောင်ချက် = အခြေခံ ဖိုင်လုပ်ငန်းအပြင် စွမ်းရည်တိုးဖို့ MCP server က tool တွေ သုံးနိုင်တယ်
</note>

<note title="Claude Code in Action">
Claude Code in Action
Claude Code လက်တွေ့သုံးပုံ

Claude Code = AI coding assistant that functions as a collaborative engineer on projects, not just a code generator.
Claude Code = ကုဒ်ထုတ်စက်သက်သက် မဟုတ်ဘဲ၊ ပရောဂျက်မှာ အတူလုပ်တဲ့ အင်ဂျင်နီယာလို အလုပ်လုပ်တဲ့ AI ကုဒ်အကူအညီ။

Key capabilities: project setup, feature design, code writing, testing, deployment, error fixing in production.
အဓိက စွမ်းရည်: ပရောဂျက် ပြင်ဆင်၊ လုပ်ဆောင်ချက် ဒီဇိုင်း၊ ကုဒ်ရေး၊ စမ်းသပ်၊ တင်သွင်း၊ production အမှားပြင်။

Setup workflow:
ပြင်ဆင် လုပ်ငန်းစဉ်:

- Download project, open in editor
- ပရောဂျက် ဒေါင်းလုဒ်၊ အယ်ဒီတာမှာ ဖွင့်

- Run `claude` command to launch
- ဖွင့်ဖို့ `claude` command ခိုင်းပါ

- Ask Claude to read README and execute setup directions
- Claude ကို README ဖတ်ခိုင်း၊ ပြင်ဆင်ညွှန်ကြားချက် လုပ်ခိုင်းပါ

- Run `init` command = Claude scans codebase for architecture/coding style, creates claude.md file
- `init` command ခိုင်း = Claude က ဗိသုကာ / ကုဒ်ပုံစံ စစ်တယ်၊ `claude.md` ဖိုင် လုပ်တယ်

- claude.md = automatically included context for future requests
- `claude.md` = နောက်တောင်းဆိုချက်တွေမှာ အလိုအလျောက် ပါတဲ့ context

Memory types: Project (shared), Local, User memory files.
မှတ်ဉာဏ် အမျိုးအစား: Project (မျှသုံး)၊ Local၊ User memory ဖိုင်များ။

Context management:
Context စီမံခြင်း:

- Use # symbol to add specific notes to memory
- မှတ်ဉာဏ်ထဲ မှတ်စုထည့်ဖို့ `#` သင်္ကေတ သုံးပါ

- Can manually edit claude.md or rerun init to update
- `claude.md` ကို ကိုယ်တိုင် ပြင်လို့ရ၊ သို့မဟုတ် `init` ပြန်ခိုင်းပြီး အပ်ဒိတ် လုပ်လို့ရ

- Claude can handle Git operations (staging, committing)
- Claude က Git လုပ်ငန်း (staging၊ commit) လုပ်နိုင်တယ်

Effective prompting strategies:
ထိရောက်တဲ့ prompt နည်းများ:

Method 1 - Three-step workflow:
နည်း ၁ - အဆင့် ၃ ဆင့် လုပ်ငန်းစဉ်:

1. Identify relevant files, ask Claude to analyze them
1. သက်ဆိုင်တဲ့ ဖိုင်တွေ ရှာ၊ Claude ကို ခွဲခြမ်းစိတ်ဖြာခိုင်းပါ

2. Describe feature, ask Claude to plan solution (no code yet)
2. လုပ်ဆောင်ချက် ရှင်းပြ၊ Claude ကို အစီအစဉ်ဆွဲခိုင်းပါ (ကုဒ် မရေးသေး)

3. Ask Claude to implement the plan
3. Claude ကို အစီအစဉ် အကောင်အထည်ဖော်ခိုင်းပါ

Method 2 - Test-driven development:
နည်း ၂ - စမ်းသပ်မှုဦးစားပေး ဖွံ့ဖြိုးခြင်း:

1. Provide relevant context
1. သက်ဆိုင်တဲ့ context ပေးပါ

2. Ask Claude to suggest tests for the feature
2. Claude ကို ဒီလုပ်ဆောင်ချက်အတွက် စမ်းသပ်မှု အကြံပေးခိုင်းပါ

3. Select and implement chosen tests
3. ရွေးထားတဲ့ စမ်းသပ်မှုတွေ ရွေးပြီး ရေးပါ

4. Ask Claude to write code until tests pass
4. စမ်းသပ်မှု အောင်တဲ့အထိ Claude ကို ကုဒ်ရေးခိုင်းပါ

Core principle: Claude Code = effort multiplier. More detailed instructions = significantly better results. Treat as collaborative engineer, not just code generator.
အဓိက စည်းမျဉ်း: Claude Code = အားထုတ်မှု မြှောက်စက်။ ညွှန်ကြားချက် ပိုအသေးစိတ် = ရလဒ် သိသိသာသာ ပိုကောင်း။ ကုဒ်ထုတ်စက်လို မသုံးဘဲ၊ အတူလုပ်တဲ့ အင်ဂျင်နီယာလို ဆက်ဆံပါ။
</note>

<note title="Enhancements with MCP Servers">
Enhancements with MCP Servers
MCP Server နဲ့ စွမ်းရည်တိုးခြင်း

Claude Code = AI assistant with embedded MCP (Model Context Protocol) client that can connect to MCP servers to expand functionality.
Claude Code = MCP server ချိတ်ပြီး လုပ်ဆောင်ချက် တိုးလို့ရတဲ့၊ MCP client ပါပြီးသား AI အကူအညီ။

MCP Server Integration = Connect external tools/services to Claude Code via command: `claude mcp add [server-name] [startup-command]`
MCP Server ပေါင်းစပ်ခြင်း = ပြင်ပ tool/ဝန်ဆောင်မှုကို Claude Code နဲ့ ချိတ်ပါ။ command: `claude mcp add [server-name] [startup-command]`

Example Implementation = Document processing server exposing "Document Path to Markdown" tool, allowing Claude Code to read PDF/Word documents by running `uv run main.py`
ဥပမာ အကောင်အထည်ဖော်မှု = "Document Path to Markdown" tool ဖွင့်ပေးတဲ့ စာရွက်စီမံ server။ `uv run main.py` ခိုင်းပြီး Claude Code က PDF/Word ဖတ်နိုင်အောင်

Dynamic Capability Expansion = MCP servers add new functions to Claude Code in real-time without core modifications.
စွမ်းရည် တိုးချဲ့ခြင်း = MCP server က Claude Code ရဲ့ အူတိုင်ကို မပြင်ဘဲ၊ အချိန်နဲ့တပြေးညီ function အသစ် ထည့်တယ်။

Common Use Cases = Production monitoring (Sentry), project management (Jira), communication (Slack), custom development workflow tools.
အသုံးများတဲ့ သုံးစရာ = Production စောင့်ကြည့်ခြင်း (Sentry)၊ ပရောဂျက်စီမံ (Jira)၊ ဆက်သွယ်ရေး (Slack)၊ ကိုယ်ပိုင် ဖွံ့ဖြိုးလုပ်ငန်းစဉ် tool များ

Key Benefit = Significant flexibility increase for development workflows through modular server connections.
အဓိက အကျိုး = server တွေကို အပိုင်းလိုက် ချိတ်လို့၊ ဖွံ့ဖြိုးလုပ်ငန်းစဉ် ပျော့ပြောင်းမှု သိသိသာသာ တက်တယ်။

Setup Process = 1) Create MCP server with tools, 2) Add server to Claude Code with name and startup command, 3) Restart Claude Code to access new capabilities.
ပြင်ဆင် လုပ်ငန်းစဉ် = ၁) tool ပါတဲ့ MCP server လုပ်၊ ၂) နာမည်နဲ့ စတင် command နဲ့ Claude Code ထဲ server ထည့်၊ ၃) စွမ်းရည်အသစ် သုံးဖို့ Claude Code ပြန်ဖွင့်
</note>

<note title="Parallelizing Claude Code">
Parallelizing Claude Code
Claude Code ကို တစ်ပြိုင်နက် ခိုင်းခြင်း
Parallel = တစ်ပြိုင်နက် များစွာ လုပ်တာ။

Parallelizing Claude Code = running multiple Claude instances simultaneously to complete different tasks in parallel
Claude Code ကို တစ်ပြိုင်နက် ခိုင်းခြင်း = Claude instance များစွာကို တစ်ပြိုင်နက် ခိုင်းပြီး၊ အလုပ်မတူတာတွေ တစ်ပြိုင်နက် ပြီးအောင် လုပ်တာ

Core Problem = multiple Claude instances modifying same files simultaneously creates conflicts and invalid code
အဓိက ပြဿနာ = Claude instance များစွာက ဖိုင်တူကို တစ်ပြိုင်နက် ပြင်ရင် တိုက်မိပြီး၊ ကုဒ် ပျက်နိုင်တယ်

Solution = Git work trees providing isolated workspaces per Claude instance
ဖြေရှင်းချက် = Claude instance တစ်ခုချင်းအတွက် သီးသန့် လုပ်ငန်းခွင် ပေးတဲ့ Git work tree

Git Work Trees = feature creating complete project copies in separate directories, each corresponding to different Git branches
Git Work Trees = ပရောဂျက် မိတ္တူအပြည့်ကို ဖိုလ်ဒါသီးသန့်မှာ လုပ်တဲ့ လုပ်ဆောင်ချက်။ တစ်ခုချင်းက Git branch မဲတူနဲ့ တွဲတယ်

Workflow = create work tree → assign task to Claude instance → work in isolation → commit changes → merge back to main branch
လုပ်ငန်းစဉ် = work tree လုပ် → Claude instance ကို အလုပ်ပေး → သီးသန့် လုပ် → ပြောင်းလဲမှု commit → main branch ဆီ ပြန်ပေါင်း

Custom Commands = automating work tree creation/management through .claude/commands directory with markdown files containing prompts
ကိုယ်ပိုင် Command = `.claude/commands` ဖိုလ်ဒါထဲ prompt ပါတဲ့ markdown ဖိုင်တွေနဲ့ work tree ဖန်တီး/စီမံတာ အလိုအလျောက် လုပ်ခြင်း

Command Structure = .claude/commands/filename.md with $ARGUMENTS placeholder for dynamic values
Command ဖွဲ့စည်းပုံ = `.claude/commands/filename.md`။ တန်ဖိုးပြောင်းလို့ရအောင် `$ARGUMENTS` နေရာလွတ် ပါတယ်

Parallel Execution Benefits = single developer commanding virtual team of software engineers, major productivity scaling limited only by engineer's management capacity
တစ်ပြိုင်နက် ခိုင်းခြင်း အကျိုး = developer တစ်ယောက်က ဆော့ဖ်ဝဲအင်ဂျင်နီယာ အတုအဖွဲ့ ကို ကွပ်ကဲနိုင်တယ်။ ကုန်ထုတ်စွမ်းအား တက်တာက အင်ဂျင်နီယာ ဘယ်လောက် စီမံနိုင်လဲ ပေါ်မှာပဲ မူတည်တယ်

Merge Conflicts = Claude automatically resolves conflicts during branch merging process
Merge တိုက်မိမှု = branch ပေါင်းတဲ့အခါ Claude က တိုက်မိမှုကို အလိုအလျောက် ဖြေရှင်းတယ်

Cleanup = Claude handles work tree removal after feature completion
ရှင်းလင်းခြင်း = လုပ်ဆောင်ချက် ပြီးရင် Claude က work tree ဖယ်တာ လုပ်တယ်

Key Advantage = scales to unlimited parallel instances based on developer's capacity to manage simultaneous tasks
အဓိက အားသာချက် = developer က တစ်ပြိုင်နက် အလုပ် ဘယ်လောက် စီမံနိုင်လဲ အလိုက်၊ တစ်ပြိုင်နက် instance အကန့်အသတ်မရှိ ချဲ့လို့ရတယ်
</note>

<note title="Automated Debugging">
Automated Debugging
အလိုအလျောက် အမှားရှာခြင်း

Automated Debugging = using AI (Claude) to automatically detect, analyze, and fix production errors without manual intervention.
အလိုအလျောက် အမှားရှာခြင်း = လူလက်မပါဘဲ AI (Claude) က production အမှား ရှာ၊ ခွဲခြမ်းစိတ်ဖြာ၊ ပြင်တာ။

Core Workflow:
အဓိက လုပ်ငန်းစဉ်:

1. GitHub Action runs daily to check production environment
1. GitHub Action က နေ့စဉ် ခိုင်းပြီး production ပတ်ဝန်းကျင် စစ်တယ်

2. Fetches CloudWatch logs from last 24 hours
2. ပြီးခဲ့တဲ့ ၂၄ နာရီ CloudWatch log တွေ ယူတယ်

3. Claude identifies errors, deduplicates them
3. Claude က အမှားတွေ ရှာတယ်၊ ထပ်နေတာ ဖယ်တယ်

4. Claude analyzes each error and generates fixes
4. Claude က အမှားတစ်ခုချင်း ခွဲခြမ်းစိတ်ဖြာပြီး ပြင်ကုဒ် ထုတ်တယ်

5. Creates pull request with proposed solutions
5. အကြံပြု ဖြေရှင်းချက်နဲ့ pull request ဖန်တီးတယ်

Key Components:
အဓိက အစိတ်အပိုင်းများ:

- GitHub Actions for scheduling/automation
- အချိန်ဇယား / အလိုအလျောက်လုပ်ဖို့ GitHub Actions

- AWS CLI for log retrieval
- log ယူဖို့ AWS CLI

- Claude Code for error analysis and code fixes
- အမှား ခွဲခြမ်းစိတ်ဖြာနဲ့ ကုဒ်ပြင်ဖို့ Claude Code

- CloudWatch for production error monitoring
- production အမှား စောင့်ကြည့်ဖို့ CloudWatch

Benefits:
အကျိုးများ:

- Catches production-only errors (issues not present in development)
- development မှာ မပေါ်တဲ့ production-only အမှားတွေ ဖမ်းတယ်

- Reduces manual log hunting and debugging time
- log လိုက်ရှာ၊ အမှားရှာတဲ့ လက်အလုပ် အချိန် လျော့တယ်

- Provides context-aware fixes with explanations
- အကြောင်းအရာ သိတဲ့ ပြင်ကုဒ်နဲ့ ရှင်းလင်းချက် ပေးတယ်

- Creates reviewable pull requests for changes
- ပြောင်းလဲမှုတွေအတွက် စစ်ဆေးလို့ရတဲ့ pull request လုပ်တယ်

Common Use Case: Configuration errors between environments (invalid model IDs, API keys, etc. that work locally but fail in production)
အသုံးများတဲ့ သုံးစရာ: ပတ်ဝန်းကျင်ကြား ပြင်ဆင်မှု အမှား (local မှာ ရပြီး production မှာ ပျက်တဲ့ model ID မှား၊ API key စသဖြင့်)

Implementation Requirements: Repository access, cloud logging service, AI coding assistant, CI/CD pipeline integration.
အကောင်အထည်ဖော် လိုအပ်ချက်: Repository ဝင်ခွင့်၊ cloud log ဝန်ဆောင်မှု၊ AI ကုဒ်အကူအညီ၊ CI/CD pipeline ပေါင်းစပ်မှု
</note>

<note title="Computer Use">
Computer Use
ကွန်ပျူတာ သုံးခြင်း

Computer Use = Claude's ability to interact with computer interfaces through visual observation and control actions.
Computer Use = Claude က မျက်နှာပြင်ကို မျက်စိနဲ့ကြည့်၊ ခလုတ်နှိပ်၊ စာရိုက်ပြီး ကွန်ပျူတာနဲ့ အပြန်အလှန် လုပ်နိုင်တာ။

Key capabilities:
အဓိက စွမ်းရည်များ:

- Takes screenshots of applications/browsers
- App / browser ရဲ့ မျက်နှာပြင်ဓာတ်ပုံ ရိုက်တယ်

- Clicks buttons, types text, navigates interfaces
- ခလုတ်နှိပ်၊ စာရိုက်၊ မျက်နှာပြင် လှည့်လည်တယ်

- Follows multi-step instructions autonomously
- အဆင့်များစွာ ညွှန်ကြားချက်ကို ကိုယ်တိုင် လိုက်လုပ်တယ်

- Performs QA testing and automation tasks
- QA စမ်းသပ်မှုနဲ့ အလိုအလျောက်လုပ်ငန်း လုပ်တယ်

How it works:
ဘယ်လို အလုပ်လုပ်လဲ:

- Runs in isolated Docker container environment
- ခွဲခြားထားတဲ့ Docker container ပတ်ဝန်းကျင်မှာ ခိုင်းတယ်

- User provides instructions via chat interface
- User က chat မျက်နှာပြင်က ညွှန်ကြားချက် ပေးတယ်

- Claude observes screen visually and executes actions
- Claude က မျက်နှာပြင်ကို ကြည့်ပြီး လုပ်ဆောင်ချက် လုပ်တယ်

- Generates reports on task completion/results
- အလုပ်ပြီးမှု / ရလဒ် အစီရင်ခံစာ ထုတ်တယ်

Primary use cases:
အဓိက သုံးစရာများ:

- Automated QA testing of web applications
- ဝက်ဘ် app ကို အလိုအလျောက် QA စမ်းသပ်ခြင်း

- UI interaction testing across different scenarios
- အခြေအနေအမျိုးမျိုးမှာ UI နှိပ်/သုံးတာ စမ်းသပ်ခြင်း

- Time-saving for repetitive computer tasks
- ထပ်တလဲလဲ ကွန်ပျူတာအလုပ် အချိန်ကုန်သက်သာခြင်း

- Bug identification through systematic testing
- စနစ်တကျ စမ်းပြီး bug ရှာခြင်း

Setup requirement = Reference implementation available for local testing
ပြင်ဆင် လိုအပ်ချက် = local မှာ စမ်းဖို့ နမူနာ အကောင်အထည်ဖော်မှု ရှိတယ်

Example workflow: User describes testing requirements → Claude navigates to application → Executes test cases → Reports pass/fail results with detailed findings
ဥပမာ လုပ်ငန်းစဉ်: User က စမ်းသပ်လိုအပ်ချက် ရှင်းပြ → Claude က app ဆီ သွား → စမ်းသပ်မှုတွေ အလုပ်လုပ် → အောင်/ရှုံး ရလဒ်နဲ့ အသေးစိတ် တွေ့ရှိချက် တင်ပြ
</note>

<note title="How Computer Use Works">
How Computer Use Works
Computer Use ဘယ်လို အလုပ်လုပ်လဲ

Computer use = tool system implementation allowing Claude to interact with computing environments
Computer use = Claude က ကွန်ပျူတာပတ်ဝန်းကျင်နဲ့ အပြန်အလှန်လုပ်ဖို့ tool စနစ် အကောင်အထည်ဖော်မှု

Tool use flow: User sends message + tool schema → Claude responds with tool use request (ID, name, input) → Server executes code → Result sent back to Claude as tool result
Tool use စီးဆင်းမှု: User က message + tool schema ပို့ → Claude က tool use တောင်းဆိုချက် ပြန် (ID, နာမည်, input) → Server က ကုဒ်အလုပ်လုပ် → ရလဒ်ကို tool result အဖြစ် Claude ဆီ ပြန်ပို့

Computer use follows identical flow:
Computer use က စီးဆင်းမှု တူတယ်:

- Special tool schema sent to Claude (small schema expands to larger structure behind scenes)
- အထူး tool schema ကို Claude ဆီ ပို့တယ် (schema အတိုက နောက်ကွယ်မှာ ဖွဲ့စည်းပုံကြီး ဖြစ်သွားတယ်)

- Expanded schema includes action function with arguments: mouse move, left click, screenshot, etc.
- ချဲ့ထားတဲ့ schema ထဲမှာ action function ပါတယ်။ argument: mouse ရွှေ့၊ ဘယ်ကလစ်၊ မျက်နှာပြင်ဓာတ်ပုံ စသဖြင့်

- Claude sends tool use request
- Claude က tool use တောင်းဆိုချက် ပို့တယ်

- Developers must fulfill request via computing environment (typically Docker container)
- Developer က ကွန်ပျူတာပတ်ဝန်းကျင် (များသောအားဖြင့် Docker container) နဲ့ တောင်းဆိုချက် ဖြည့်ရမယ်

- Container executes programmatic key presses/mouse movements
- Container က ကုဒ်နဲ့ ခလုတ်နှိပ် / mouse ရွှေ့တယ်

- Response sent back to Claude
- အဖြေကို Claude ဆီ ပြန်ပို့တယ်

Key points:
အဓိက အချက်များ:

- Claude doesn't directly manipulate computers
- Claude က ကွန်ပျူတာကို တိုက်ရိုက် မထိန်းဘူး

- Computer use = tool system + developer-provided computing environment
- Computer use = tool စနစ် + developer ပေးတဲ့ ကွန်ပျူတာပတ်ဝန်းကျင်

- Anthropic provides reference implementation (Docker container with pre-built mouse/keyboard execution code)
- Anthropic က နမူနာ အကောင်အထည်ဖော်မှု ပေးတယ် (mouse/keyboard အလုပ်လုပ်ကုဒ် ပါပြီးသား Docker container)

- Setup requires Docker + simple command execution
- ပြင်ဆင်ဖို့ Docker + ရိုးရိုး command အလုပ်လုပ်ရုံ

- Enables direct chat interface for testing Claude's computer use functionality
- Claude ရဲ့ computer use ကို စမ်းဖို့ chat မျက်နှာပြင် တိုက်ရိုက် သုံးလို့ရအောင်

Computer use = abstraction layer where tool system handles Claude communication while Docker container handles actual computer interactions.
Computer use = abstraction အလွှာ။ Tool စနစ်က Claude ဆက်သွယ်မှု ကိုင်တယ်။ Docker container က တကယ့် ကွန်ပျူတာ အပြန်အလှန်လုပ်မှု ကိုင်တယ်။
</note>

<note title="Agents and Workflows">
Agents and Workflows
Agent နှင့် Workflow များ
Agent = အဆင့်ကို ကိုယ်တိုင် စီပြီး tool သုံးတဲ့ AI။ Workflow = အဆင့်တွေ ကြိုသတ်မှတ်ထားတဲ့ လုပ်ငန်းစဉ်။

Workflows and agents = strategies for handling user tasks that can't be completed by Claude in a single request.
Workflow နဲ့ agent = Claude က တောင်းဆိုချက် တစ်ခုတည်းနဲ့ မပြီးနိုင်တဲ့ user အလုပ်ကို ကိုင်တွယ်တဲ့ နည်းများ။

Decision rule: Use workflows when you have precise task understanding and know exact steps sequence. Use agents when task details are unclear.
ဆုံးဖြတ် စည်းမျဉ်း: အလုပ်ကို တိတိကျကျ သိပြီး အဆင့်အစဉ် သေချာရင် workflow သုံးပါ။ အလုပ်အသေးစိတ် မရှင်းရင် agent သုံးပါ။

Workflow = series of calls to Claude for specific problems where steps are predetermined.
Workflow = အဆင့်တွေ ကြိုသတ်မှတ်ထားတဲ့ တိကျတဲ့ ပြဿနာအတွက် Claude ကို အကြိမ်ကြိမ် ခေါ်တာ။

Example workflow: Image to 3D model converter
ဥပမာ workflow: ပုံကနေ 3D model ပြောင်းစက်

- Step 1: Claude describes uploaded image in detail
- အဆင့် ၁: Claude က တင်လိုက်တဲ့ပုံကို အသေးစိတ် ဖော်ပြတယ်

- Step 2: Claude uses CADQuery Python library to model object from description
- အဆင့် ၂: Claude က ဖော်ပြချက်ကနေ အရာဝတ္ထု ပုံစံထုတ်ဖို့ CADQuery Python library သုံးတယ်

- Step 3: Create rendering of model
- အဆင့် ၃: model ရဲ့ ပုံဆွဲမှု (rendering) လုပ်တယ်

- Step 4: Claude compares rendering to original image
- အဆင့် ၄: Claude က rendering ကို မူရင်းပုံနဲ့ နှိုင်းယှဉ်တယ်

- Step 5: If inaccurate, repeat from step 2 with feedback
- အဆင့် ၅: မမှန်ရင် တုံ့ပြန်ချက်နဲ့ အဆင့် ၂ က ပြန်လုပ်တယ်

This follows evaluator-optimizer pattern:
ဒါက evaluator-optimizer ပုံစံ ဖြစ်တယ်:

- Producer = generates output (Claude + CADQuery modeling)
- Producer = အထွက် ထုတ်တယ် (Claude + CADQuery ပုံစံထုတ်ခြင်း)

- Evaluator = assesses output quality (comparison step)
- Evaluator = အထွက် အရည်အသွေး စစ်တယ် (နှိုင်းယှဉ်အဆင့်)

- Loop continues until evaluator accepts output
- Evaluator က လက်ခံတဲ့အထိ loop ဆက်လုပ်တယ်

Key point: Workflows are implementation patterns that other engineers have successfully used. Identifying workflow patterns doesn't automatically implement them - you still need to write the actual code.
အဓိကအချက်: Workflow တွေက တခြားအင်ဂျင်နီယာတွေ အောင်မြင်စွာ သုံးခဲ့တဲ့ အကောင်အထည်ဖော် ပုံစံများ။ ပုံစံ သိရုံနဲ့ အလိုအလျောက် မဖြစ်ဘူး။ တကယ့်ကုဒ် ကိုယ်တိုင် ရေးရသေးတယ်။
</note>

<note title="Parallelization Workflows">
Parallelization Workflows
တစ်ပြိုင်နက် Workflow များ

Parallelization Workflows = breaking one complex task into multiple simultaneous subtasks, then aggregating results.
တစ်ပြိုင်နက် Workflow = ခက်ခဲတဲ့ အလုပ်တစ်ခုကို တစ်ပြိုင်နက် လုပ်ငန်းခွဲ များစွာ ခွဲပြီး၊ ရလဒ်တွေ ပြန်ပေါင်းတာ။

Example: Material selection for parts
ဥပမာ: အပိုင်းအစတွေအတွက် ပစ္စည်းရွေးခြင်း

- Instead of: One large prompt asking Claude to choose between metal/polymer/ceramic/composite with all criteria
- ဒီလို မလုပ်ပါနဲ့: စံနှုန်းအားလုံးနဲ့ သတ္တု / ပလတ်စတစ် / ကြွေ / ပေါင်းစပ်ပစ္စည်း ရွေးခိုင်းတဲ့ prompt ကြီး တစ်ခု

- Use: Separate parallel requests, each evaluating one material's suitability, then final aggregation step to compare results
- ဒီလို လုပ်ပါ: ပစ္စည်းတစ်ခုချင်း သင့်/မသင့် စစ်တဲ့ တစ်ပြိုင်နက် တောင်းဆိုချက်တွေ၊ ပြီးမှ ရလဒ် နှိုင်းယှဉ်ပေါင်းတဲ့ နောက်ဆုံးအဆင့်

Structure: Input → Multiple parallel subtasks → Aggregator → Final output
ဖွဲ့စည်းပုံ: Input → တစ်ပြိုင်နက် လုပ်ငန်းခွဲ များစွာ → Aggregator (ပေါင်းသူ) → နောက်ဆုံးအထွက်

Benefits:
အကျိုးများ:

- Focus = Each subtask handles one specific analysis instead of juggling multiple considerations
- အာရုံစိုက်မှု = လုပ်ငန်းခွဲတစ်ခုက စဉ်းစားစရာ များစွာ မရောဘဲ၊ ခွဲခြမ်းစိတ်ဖြာမှု တစ်ခုပဲ ကိုင်တယ်

- Modularity = Individual prompts can be improved/evaluated separately
- အပိုင်းလိုက်ဖြစ်မှု = prompt တစ်ခုချင်းကို သီးသန့် ပိုကောင်းအောင် / အကဲဖြတ်လို့ရတယ်

- Scalability = Easy to add new subtasks without affecting existing ones
- ချဲ့ထွင်နိုင်မှု = ရှိပြီးသားကို မထိဘဲ လုပ်ငန်းခွဲအသစ် ထည့်ရ လွယ်တယ်

- Quality = Reduces confusion from overly complex single prompts
- အရည်အသွေး = ရှုပ်လွန်းတဲ့ prompt တစ်ခုတည်းကြောင့် ရှုပ်ထွေးမှု လျော့တယ်

Key principle: Decompose complex decisions into specialized parallel analyses, then synthesize results.
အဓိက စည်းမျဉ်း: ခက်ခဲတဲ့ ဆုံးဖြတ်ချက်ကို အထူးပြု တစ်ပြိုင်နက် ခွဲခြမ်းစိတ်ဖြာမှုတွေ ခွဲ၊ ပြီးမှ ရလဒ် ပေါင်းပါ။
</note>

<note title="Chaining Workflows">
Chaining Workflows
ချိတ်ဆက် Workflow များ
Chain = အဆင့်တွေကို တစ်ခုပြီးတစ်ခု ဆက်လုပ်တာ။

Chaining Workflows = breaking large tasks into series of distinct sequential steps rather than single complex prompt
ချိတ်ဆက် Workflow = ရှုပ်ထွေးတဲ့ prompt တစ်ခုတည်း မဟုတ်ဘဲ၊ အလုပ်ကြီးကို သီးသန့် အစဉ်လိုက် အဆင့်တွေ ခွဲတာ

Core concept: Instead of one massive prompt with multiple requirements, split into separate calls where each focuses on one specific subtask.
အဓိက အယူအဆ: လိုအပ်ချက်များစွာ ပါတဲ့ prompt ကြီး တစ်ခု မသုံးဘဲ၊ လုပ်ငန်းခွဲ တစ်ခုစီ အာရုံစိုက်တဲ့ ခေါ်ဆိုမှုတွေ ခွဲပါ။

Example workflow: User enters topic → search trending topics → Claude selects most interesting → Claude researches topic → Claude writes script → generate video → post to social media
ဥပမာ workflow: User က ခေါင်းစဉ်ထည့် → လူကြိုက်များ ခေါင်းစဉ် ရှာ → Claude က အစိတ်ဝင်စားဆုံး ရွေး → Claude က ခေါင်းစဉ် လေ့လာ → Claude က script ရေး → ဗီဒီယို ထုတ် → လူမှုကွန်ရက် တင်

Key benefit: Allows AI to focus on individual tasks rather than juggling multiple constraints simultaneously
အဓိက အကျိုး: ကန့်သတ်ချက် များစွာ တစ်ပြိုင်နက် မကိုင်ဘဲ၊ AI က အလုပ်တစ်ခုချင်း အာရုံစိုက်နိုင်တယ်

Primary use case: When Claude consistently ignores constraints in complex prompts despite repetition. Common with long prompts containing many "don't do X" requirements.
အဓိက သုံးစရာ: ရှုပ်ထွေးတဲ့ prompt မှာ ထပ်ပြောနေတောင် Claude က ကန့်သတ်ချက်တွေ မလိုက်နာတဲ့အခါ။ `"X မလုပ်နဲ့"` များစွာ ပါတဲ့ prompt ရှည်မှာ မကြာခဏ ဖြစ်တယ်။

Problem scenario: Long prompt with constraints (don't mention AI, no emojis, professional tone) → Claude violates some constraints regardless of repetition
ပြဿနာ အခြေအနေ: ကန့်သတ်ချက် ပါတဲ့ prompt ရှည် (AI မပြောနဲ့၊ emoji မသုံးနဲ့၊ ပရော်ဖက်ရှင်နယ် အသံထား) → ထပ်ပြောနေတောင် Claude က တချို့ ကန့်သတ်ချက် ချိုးတယ်

Solution: Step 1 - Send initial prompt, accept imperfect output. Step 2 - Follow-up prompt asking Claude to rewrite based on specific violations found.
ဖြေရှင်းချက်: အဆင့် ၁ - ပထမ prompt ပို့၊ မပြည့်စုံတဲ့ အဖြေ လက်ခံ။ အဆင့် ၂ - တွေ့တဲ့ ချိုးဖောက်မှုတွေအရ ပြန်ရေးခိုင်းတဲ့ နောက်ဆက်တွဲ prompt။

Critical insight: Even simple-seeming workflow becomes essential when dealing with constraint-heavy prompts that AI struggles to follow completely in single pass.
အရေးကြီး နားလည်ချက်: ရိုးရိုးလို ထင်ရတဲ့ workflow တောင်၊ ကန့်သတ်ချက်များတဲ့ prompt ကို AI တစ်ခါတည်း မလိုက်နိုင်တဲ့အခါ မဖြစ်မနေ လိုလာတယ်။
</note>

<note title="Routing Workflows">
Routing Workflows
လမ်းကြောင်းခွဲ Workflow များ
Routing = ဘယ်လမ်း / ဘယ်လုပ်ငန်းစဉ် ဆီ ပို့မလဲ ရွေးတာ။

Routing Workflows = workflow pattern that categorizes user input to determine appropriate processing pipeline
Routing Workflows = user input ကို အမျိုးအစားခွဲပြီး၊ သင့်တဲ့ စီမံ pipeline ရွေးတဲ့ workflow ပုံစံ

Key mechanism: Initial request to Claude categorizes user input into predefined genres/categories. Based on categorization response, system routes to specialized processing pipeline with customized prompts/tools.
အဓိက ယန္တရား: ပထမ တောင်းဆိုချက်က user input ကို ကြိုသတ်မှတ် အမျိုးအစားတွေ ခွဲတယ်။ အဲဒီအဖြေအရ၊ စိတ်ကြိုက် prompt/tool ပါတဲ့ အထူးပြု စီမံ pipeline ဆီ ပို့တယ်။

Example flow:
ဥပမာ စီးဆင်းမှု:

1. User enters topic (e.g., "Python functions")
1. User က ခေါင်းစဉ်ထည့်တယ် (ဥပမာ `"Python functions"`)

2. Claude categorizes topic (e.g., "educational")
2. Claude က ခေါင်းစဉ် အမျိုးအစားခွဲတယ် (ဥပမာ `"educational"`)

3. System uses educational-specific prompt template
3. စနစ်က ပညာရေးသီးသန့် prompt ပုံစံ သုံးတယ်

4. Claude generates script with educational tone/structure
4. Claude က ပညာရေး အသံထား / ဖွဲ့စည်းပုံနဲ့ script ထုတ်တယ်

Benefits: Ensures output matches topic nature. Programming topics get educational treatment with definitions/explanations. Entertainment topics get trendy language/engaging hooks.
အကျိုး: အထွက်က ခေါင်းစဉ် သဘာဝနဲ့ ကိုက်တယ်။ ပရိုဂရမ်ခေါင်းစဉ်ဆို အဓိပ္ပာယ်ဖွင့် / ရှင်းလင်းချက် ပါတဲ့ ပညာရေးပုံစံ။ ဖျော်ဖြေရေးဆို ခေတ်စကား / စိတ်ဝင်စားစရာ အစ။

Structure: One routing step → Multiple specialized processing pipelines → Each pipeline has customized prompts/tools for specific category
ဖွဲ့စည်းပုံ: လမ်းကြောင်းခွဲ အဆင့် ၁ ခု → အထူးပြု စီမံ pipeline များစွာ → pipeline တစ်ခုချင်းမှာ အမျိုးအစားသီးသန့် prompt/tool ရှိတယ်

Use case: Social media video script generation where different topics require different tones and approaches.
သုံးစရာ: ခေါင်းစဉ်မတူရင် အသံထား / ချဉ်းကပ်ပုံ မတူတဲ့ လူမှုကွန်ရက် ဗီဒီယို script ထုတ်ခြင်း
</note>

<note title="Agents and Tools">
Agents and Tools
Agent နှင့် Tool များ

Agents = AI systems that create plans to complete tasks using provided tools, effective when exact steps are unknown. Workflows = better when precise steps are known.
Agent = ပေးထားတဲ့ tool တွေနဲ့ အလုပ်ပြီးအောင် အစီအစဉ်ဆွဲတဲ့ AI စနစ်။ အဆင့်တိတိ မသိရင် ထိရောက်တယ်။ Workflow = အဆင့်တိတိ သိရင် ပိုကောင်းတယ်။

Key differences: Workflows require predetermined steps, agents dynamically plan using available tools.
အဓိက ကွာခြားချက်: Workflow က ကြိုသတ်မှတ် အဆင့် လိုတယ်။ Agent က ရနိုင်တဲ့ tool တွေနဲ့ လမ်းကြောင်း လိုက်ဆွဲတယ်။

Agent advantages: Flexibility to solve variety of tasks with same toolset, can combine tools in unexpected ways.
Agent အားသာချက်: tool အစုတူနဲ့ အလုပ်အမျိုးမျိုး ဖြေရှင်းနိုင်တယ်။ tool တွေကို မမျှော်လင့်တဲ့ပုံ ပေါင်းနိုင်တယ်။

Tool abstraction principle: Provide generic/abstract tools rather than hyper-specialized ones. Example - Claude code uses bash, web_fetch, file_write (abstract) rather than refactor_tool, install_dependencies (specialized).
Tool abstraction စည်းမျဉ်း: အရမ်းအထူးပြု tool မပေးဘဲ၊ ယေဘုယျ / abstract tool ပေးပါ။ ဥပမာ Claude Code က `refactor_tool`, `install_dependencies` (အထူးပြု) မဟုတ်ဘဲ `bash`, `web_fetch`, `file_write` (abstract) သုံးတယ်။

Tool combination examples: get_current_datetime + add_duration + set_reminder can solve various time-related tasks through different combinations.
Tool ပေါင်းသုံး ဥပမာ: `get_current_datetime` + `add_duration` + `set_reminder` ကို ပေါင်းပုံ မတူအောင် သုံးပြီး အချိန်ဆိုင်ရာ အလုပ်အမျိုးမျိုး ဖြေရှင်းနိုင်တယ်။

Agent behavior: Can request additional information when needed, combines tools creatively to achieve goals, works best with small set of flexible tools.
Agent အပြုအမူ: လိုရင် အပိုအချက် တောင်းနိုင်တယ်။ ပန်းတိုင်ရောက်အောင် tool တွေ ဖန်တီးမှုရှိရှိ ပေါင်းတယ်။ ပျော့ပြောင်းတဲ့ tool အနည်းငယ်နဲ့ အကောင်းဆုံး အလုပ်လုပ်တယ်။

Design approach: Give agent abstract tools that can be pieced together rather than single-purpose specialized tools. This enables dynamic problem-solving and unexpected use cases.
ဒီဇိုင်း ချဉ်းကပ်ပုံ: တစ်ခုတည်းသုံး အထူးပြု tool မပေးဘဲ၊ ပေါင်းစပ်လို့ရတဲ့ abstract tool ပေးပါ။ ဒါက ပြဿနာကို လမ်းကြောင်းလိုက် ဖြေရှင်းနိုင်ပြီး၊ မမျှော်လင့်တဲ့ သုံးစရာတွေ ဖြစ်လာစေတယ်။
</note>

<note title="Environment Inspection">
Environment Inspection
ပတ်ဝန်းကျင် စစ်ဆေးခြင်း

Environment Inspection = agents evaluating their environment and action results to understand progress and handle errors.
ပတ်ဝန်းကျင် စစ်ဆေးခြင်း = agent က ပတ်ဝန်းကျင်နဲ့ လုပ်ဆောင်ချက် ရလဒ်ကို စစ်ပြီး၊ တိုးတက်မှု နားလည်၊ အမှား ကိုင်တွယ်တာ။

Core concept: After each action, agents need feedback mechanisms beyond basic tool returns to understand new environment state.
အဓိက အယူအဆ: လုပ်ဆောင်ချက် တစ်ခုပြီးတိုင်း၊ tool ပြန်ပေးတာအပြင်၊ ပတ်ဝန်းကျင် အခြေအနေအသစ် နားလည်ဖို့ တုံ့ပြန်မှု ယန္တရား လိုတယ်။

Computer use example: Claude takes screenshot after every action (typing, clicking) to see how environment changed, since it cannot predict exact results of actions like button clicks.
Computer use ဥပမာ: ခလုတ်နှိပ်ရင် ဘာဖြစ်မလဲ တိတိကျကျ မခန့်မှန်းနိုင်လို့၊ Claude က လုပ်ဆောင်ချက်တိုင်း (စာရိုက်၊ နှိပ်) ပြီးရင် မျက်နှာပြင်ဓာတ်ပုံ ရိုက်တယ်။

Code editing example: Before modifying files, agents must read current file contents to understand existing state.
ကုဒ်ပြင် ဥပမာ: ဖိုင်မပြင်ခင်၊ ရှိပြီးသား အခြေအနေ နားလည်အောင် agent က ဖိုင်အကြောင်းအရာ ဖတ်ရမယ်။

Social media video agent applications:
လူမှုကွန်ရက် ဗီဒီယို agent သုံးပုံ:

- Use Whisper CPP via bash to generate timestamped captions, verify dialogue placement
- ဒိုင်ယာလော့ နေရာမှန်မမှန် စစ်ဖို့ bash ကနေ Whisper CPP သုံးပြီး အချိန်တံဆိပ်ပါ စာတန်း ထုတ်ပါ

- Use FFmpeg to extract video screenshots at intervals, inspect visual results
- ပုံရလဒ် စစ်ဖို့ FFmpeg နဲ့ ဗီဒီယိုက မျက်နှာပြင်ဓာတ်ပုံ အချိန်ခြား ထုတ်ပါ

- Validate video creation meets expectations before posting
- မတင်ခင် ဗီဒီယိုက မျှော်လင့်ချက် ကိုက်မကိုက် စစ်ပါ

Key benefit: Environment inspection enables agents to gauge task progress, detect errors, and adapt to unexpected results rather than operating blindly.
အဓိက အကျိုး: ပတ်ဝန်းကျင် စစ်ဆေးမှုက agent ကို မျက်ကန်းမလုပ်စေဘဲ၊ အလုပ်တိုးတက်မှု တိုင်း၊ အမှား ရှာ၊ မမျှော်လင့်တဲ့ ရလဒ်ကို လိုက်လျောညီထွေ ဖြစ်အောင် ကူညီတယ်။
</note>

<note title="Workflows vs Agents">
Workflows vs Agents
Workflow နှင့် Agent နှိုင်းယှဉ်ခြင်း

Workflows = pre-defined series of calls to Claude with known exact steps. Agents = flexible approach using basic tools that Claude combines to complete unknown tasks.
Workflow = အဆင့်တိတိ သိပြီး၊ Claude ကို ကြိုသတ်မှတ် အစဉ်အတိုင်း ခေါ်တာ။ Agent = အခြေခံ tool တွေကို Claude က ပေါင်းပြီး၊ မသိသေးတဲ့ အလုပ် ပြီးအောင် လုပ်တဲ့ ပျော့ပြောင်းနည်း။

Key differences:
အဓိက ကွာခြားချက်များ:

Task division: Workflows break big tasks into smaller, specific subtasks enabling higher focus and accuracy. Agents handle varied challenges creatively without predetermined steps.
အလုပ်ခွဲခြင်း: Workflow က အလုပ်ကြီးကို လုပ်ငန်းခွဲသေးသေး ခွဲလို့ အာရုံစိုက်မှုနဲ့ မှန်ကန်မှု ပိုမြင့်တယ်။ Agent က ကြိုသတ်မှတ် အဆင့် မရှိဘဲ၊ စိန်ခေါ်မှု အမျိုးမျိုးကို ဖန်တီးမှုရှိရှိ ကိုင်တယ်။

Testing/evaluation: Workflows easier to test due to known execution sequence. Agents harder to test since execution path unpredictable.
စမ်းသပ် / အကဲဖြတ်ခြင်း: Workflow က အလုပ်လုပ်ပုံအစဉ် သိလို့ စမ်းရ လွယ်တယ်။ Agent က ဘယ်လမ်းသွားမလဲ မခန့်မှန်းနိုင်လို့ စမ်းရ ခက်တယ်။

User experience: Workflows require specific inputs. Agents create own inputs from user queries and can request additional input when needed.
User အတွေ့အကြုံ: Workflow က သတ်မှတ် input လိုတယ်။ Agent က user မေးခွန်းကနေ ကိုယ်ပိုင် input လုပ်တယ်။ လိုရင် အပို input တောင်းနိုင်တယ်။

Success rates: Workflows = higher task completion rates due to structured approach. Agents = lower completion rates due to delegated complexity.
အောင်မြင်နှုန်း: Workflow = ဖွဲ့စည်းပုံရှိလို့ အလုပ်ပြီးနှုန်း ပိုမြင့်တယ်။ Agent = ရှုပ်ထွေးမှုကို လွှဲထားလို့ ပြီးနှုန်း ပိုနိမ့်တယ်။

Recommendation: Prioritize workflows for reliability. Use agents only when flexibility truly required. Users want 100% working products over fancy agents.
အကြံပြုချက်: ယုံကြည်ရမှုအတွက် workflow ကို ဦးစားပေးပါ။ တကယ် ပျော့ပြောင်းမှု လိုမှသာ agent သုံးပါ။ User တွေက fancy agent ထက် ၁၀၀% အလုပ်လုပ်တဲ့ ထုတ်ကုန်ကို ပိုလိုချင်တယ်။

Core principle: Solve problems reliably first, innovation second.
အဓိက စည်းမျဉ်း: ပြဿနာကို အရင် ယုံကြည်ရအောင် ဖြေရှင်းပါ။ ဆန်းသစ်မှုက ဒုတိယ။
</note>
</notes>

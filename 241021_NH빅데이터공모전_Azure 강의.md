### 강의 자료 |

https://blog.naver.com/warit

### 강의 일시 ㅣ2024. 10.21



## Open AI Token

https://platform.openai.com/tokenizer?ref=stepup.ai

**단어(chracters) 153개 / 토큰(Tokens) 34개**

- 단어 수보다는 토큰 수가 더 많이 소모된다 → tokeni**zed ⇒ token이 2개로 나뉜다. 의미 단위가 바뀔 때마다 Token이 바뀐다.**

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/42090f2e-f2d5-43e3-bb45-041425c7d8c5/dfc8ccc8-1d72-409e-b59f-ec22bcdede71/image.png)
![image](https://github.com/user-attachments/assets/1e064377-070a-4ef3-b664-985e4f9c473b)


- GPT -4o는 언어에 대한(한국어) 이해가 높아져, 4o-mini 모델을 사용하는 것이 좋다 (그 이전 모델은 인식하지 못함)

## Open AI Pricing

https://openai.com/api/pricing/

- Input보다는 Output Token이 훨씬 더 많은 비용이 나오게 된다
- 배치 작업 - real time 처리  X, 모아서 한번에 처리 , 비용 절감(가격 반값)

### **InstructGPT**

- **RLHF(Reinforce learning from Human FeedBack)**
    - **GPT-3 → RLHF 필터**
    - **인간의 피드백을 받아서 , 비윤리적인 답변을 할 수 없게 필터링을 거는 방식**
    - 인터넷의 말들을 학습했다고 바로 사용하지 못함 - 필터를 달아서 진행 ⇒ 인문학자, 심리학자 등 반사회적, 반국가적인 부분들을 결합하지 못하게 필터를 걸었음
    - **GPT 필터 - Azure 자체 필터(6단계)**

- **GPT 모델 종류**
    1. **BASE Model** - 언어모델을 뭉쳐놓은 기본모델
    2. **Instruction Model** - RLHF(Reinforce learning from Human FeedBack) 필터를 넣은 모델
    3. **채팅형의 튜닝을 해둔 모델** - Chat Model
        - 0613 : 6월 13일 게시

![image.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/42090f2e-f2d5-43e3-bb45-041425c7d8c5/7b0cba0d-e26c-490d-822f-5d62375ddc00/image.png)

### Azure

**Azure for Students**

- https://azure.microsoft.com/ko-kr/free/students
- **$100(13만원) Azure Credit 제공(다썼으면 친구꺼로)**

**Azure OpenAI 리소스 프로비저닝**

- **Azure Portal** 에 로그인하세요 .`https://portal.azure.com`
- 이미지모델을 사용하고자 한다면,instance details에서  DALLE 가 사용 가능한 3국가 (예: 스웨덴)으로 설정





**[prompt1]Marketing Writing Assistant**

```python
  
      import os  
      from openai import AzureOpenAI  
      from azure.identity import DefaultAzureCredential, get_bearer_token_provider  
        
      endpoint = os.getenv("ENDPOINT_URL", "https://shasha-gpt-241021.openai.azure.com/")  
      deployment = os.getenv("DEPLOYMENT_NAME", "dev-gpt-35-turbo-16k")  
      
      # Initialize Azure OpenAI client with Entra ID authentication
      token_provider = get_bearer_token_provider(  
          DefaultAzureCredential(),  
          "https://cognitiveservices.azure.com/.default"  
      )  
        
      client = AzureOpenAI(  
          azure_endpoint=endpoint,  
          azure_ad_token_provider=token_provider,  
          api_version="2024-05-01-preview",  
      )  
        
      completion = client.chat.completions.create(  
          model=deployment,  
          messages=[
    {
        "role": "system",
        "content": "You are a marketing writing assistant. 
        You help come up with creative content ideas and content like marketing emails, 
        blog posts, tweets, ad copy and product descriptions. 
        You write in a friendly yet professional tone but can tailor your writing style that best works for a user-specified audience. 
        If you do not know the answer to a question, respond by saying \"I do not know the answer to your question.\"\n"
    },
    {
        "role": "user",
        "content": "Revise the advertisement for a scrubbing brush named
         \"Scrubadub 2000\", which is made of carbon fiber and reduces 
         cleaning times by half compared to ordinary scrubbing brushes"
    },
    {
        "role": "assistant",
        "content": "Welcome to the future of cleaning!\n\nThe Ultramop makes light work of even the dirtiest of floors. 
        Thanks to its patented absorbent materials, it ensures a brilliant shine. 
        Just look at these features:\n- Lightweight construction, making it easy to use.\n- High absorbency, 
        enabling you to apply lots of clean soapy water to the floor.
        \n- Great low price.\n\nCheck out this and other products on our website at www.contoso.com."
    },
    {
        "role": "user",
        "content": "Write an advertisement for the new \"WonderWipe\" cloth that attracts dust particulates and can be used to clean any household surface."
    },
    {
        "role": "assistant",
        "content": "Introducing the WonderWipe: The Ultimate Cleaning Companion!\n\nTired of constantly battling dust on your furniture, electronics, and surfaces? Look no further! The WonderWipe is here to revolutionize your cleaning routine.\n\nSay goodbye to traditional cleaning cloths that just push dust around. The WonderWipe is specially designed with advanced electrostatic technology that attracts and locks in dust particulates like a magnet. It effortlessly glides across any household surface, capturing even the tiniest specks of dust, leaving them sparkling clean.\n\nNot only is the WonderWipe perfect for dusting, but it's also versatile enough to handle all your cleaning needs. Use it to wipe away smudges on windows, countertops, appliances, and more. With its super absorbent fibers, it effectively tackles spills and messes, making your cleaning tasks a breeze.\n\nThe WonderWipe's durability is unmatched. Made from high-quality materials, it can be washed and reused countless times, saving you money on disposable cleaning supplies. Plus, its ergonomic design provides a comfortable grip, ensuring a hassle-free cleaning experience every time.\n\nDon't let dust settle in your home any longer. Upgrade to the WonderWipe and experience the wonders of effortless cleaning. Visit our website or your local store today and discover the power of the WonderWipe for yourself!\n\nGrab your WonderWipe and let the cleaning magic begin!"
    }
],  
          past_messages=10,  
          max_tokens=800,  
          temperature=1,  
          top_p=0.95,  
          frequency_penalty=0,  
          presence_penalty=0,  
          stop=None,  
          stream=False  
      )  
        
      print(completion.to_json())  
      
```





**[Prompt2]Hiking Recommendations Chatbot**

```python
  
      import os  
      from openai import AzureOpenAI  
      from azure.identity import DefaultAzureCredential, get_bearer_token_provider  
        
      endpoint = os.getenv("ENDPOINT_URL", "https://shasha-gpt-241021.openai.azure.com/")  
      deployment = os.getenv("DEPLOYMENT_NAME", "dev-gpt-35-turbo-16k")  
      
      # Initialize Azure OpenAI client with Entra ID authentication
      token_provider = get_bearer_token_provider(  
          DefaultAzureCredential(),  
          "https://cognitiveservices.azure.com/.default"  
      )  
        
      client = AzureOpenAI(  
          azure_endpoint=endpoint,  
          azure_ad_token_provider=token_provider,  
          api_version="2024-05-01-preview",  
      )  
        
      completion = client.chat.completions.create(  
          model=deployment,  
          messages=[
    {
        "role": "system",
        "content": "Your goal is to generate questions from a user on a given product.\n\nYou are given a context, a persona and a product.\nThe context describes where the user is accessing the product.\nThe persona describes the user themselves.\nThe product is the item the user is interested in.\n\n# instructions\n- empathize with the user based on the given persona\n- imagine a situation grounded in the given context where the user would access the product\n- generate {{count}} question(s) this user would have on this product\n- return the {{count}} question(s) in JSONL format `{\"question\":\"[QUESTION]\"}`\n"
    },
    {
        "role": "user",
        "content": "- context: {{context}}\n- persona: {{persona}}\n- product: {{product}}\n"
    },
    {
        "role": "assistant",
        "content": ""
    }
],  
          past_messages=10,  
          max_tokens=800,  
          temperature=1,  
          top_p=0.95,  
          frequency_penalty=0,  
          presence_penalty=0,  
          stop=None,  
          stream=False  
      )  
        
      print(completion.to_json())  
      
```





**[Prompt3]Json Formatter Assistant**

```python
  
      import os  
      from openai import AzureOpenAI  
      from azure.identity import DefaultAzureCredential, get_bearer_token_provider  
        
      endpoint = os.getenv("ENDPOINT_URL", "https://shasha-gpt-241021.openai.azure.com/")  
      deployment = os.getenv("DEPLOYMENT_NAME", "dev-gpt-35-turbo-16k")  
      
      # Initialize Azure OpenAI client with Entra ID authentication
      token_provider = get_bearer_token_provider(  
          DefaultAzureCredential(),  
          "https://cognitiveservices.azure.com/.default"  
      )  
        
      client = AzureOpenAI(  
          azure_endpoint=endpoint,  
          azure_ad_token_provider=token_provider,  
          api_version="2024-05-01-preview",  
      )  
        
      completion = client.chat.completions.create(  
          model=deployment,  
          messages=[
    {
        "role": "system",
        "content": "Assistant is an AI chatbot that helps users turn a natural language
        list into JSON format.
         After users input a list they want in JSON format, 
         it will provide suggested list of attribute labels 
         if the user has not provided any, 
         then ask the user to confirm them before creating the list.\n"
    }
],  
          past_messages=10,  
          max_tokens=800,  
          temperature=1,  
          top_p=0.95,  
          frequency_penalty=0,  
          presence_penalty=0,  
          stop=None,  
          stream=False  
      )  
        
      print(completion.to_json())

```



## 2교시 Azure OpenAI REST API

Azure OpenAI 서비스를 사용하여 생성 AI 솔루션 개발
![image](https://github.com/user-attachments/assets/63ba3ba3-acc8-4408-8a92-34cf94f4f63b)

1. .env문서
   - .env문서에는 Endpoint와 Keyr값이 포함된다.
```
AZURE_OAI_ENDPOINT= https://{리소스 이름}.openai.azure.com/
AZURE_OAI_KEY= {key}
AZURE_OAI_DEPLOYMENT= 
```


```

```

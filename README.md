# ml-azure-ai900-03
Exploraremos o uso do Azure Speech Studio e a análise linguística proporcionada pelo Language Studio. 

---

### Análise de Texto com Azure

![image](https://github.com/user-attachments/assets/5fd25cd7-41ee-4a49-8fcc-fed064592299)

**1. Criar uma Conta no Azure:**
Primeiramente, é necessário ter uma conta no Azure. Se você ainda não tem, crie uma no [site oficial do Azure](https://azure.microsoft.com/).

**2. Criar um Recurso de Serviço Cognitivo:**
Para realizar análises de texto, você precisará criar um recurso de Serviço Cognitivo no Azure. Siga os passos abaixo:
- No portal do Azure, clique em `Criar um recurso`.
- Selecione `Inteligência Artificial e Machine Learning`, depois `Serviços Cognitivos`.
- Preencha os detalhes necessários (nome, assinatura, grupo de recursos, etc.).
- Escolha a região mais próxima de você.
- Selecione o tipo de plano tarifário e clique em `Revisar + Criar`, depois em `Criar`.

**3. Obter as Chaves e o Endpoint:**
Após criar o recurso, você precisa das chaves de acesso e do endpoint:
- No portal do Azure, vá para seu recurso de Serviço Cognitivo.
- No menu à esquerda, clique em `Chaves e Endpoint`.
- Anote as duas chaves e o endpoint fornecidos.

**4. Configurar o Ambiente:**
Agora configure seu ambiente de desenvolvimento. Se estiver usando Python, por exemplo, instale as bibliotecas necessárias:
```bash
pip install azure-ai-textanalytics
```

**5. Escrever o Código para Análise de Texto:**
Com tudo configurado, você pode começar a análise de texto. Veja um exemplo de código em Python:
```python
from azure.ai.textanalytics import TextAnalyticsClient
from azure.core.credentials import AzureKeyCredential

key = "SUA_CHAVE_AQUI"
endpoint = "SEU_ENDPOINT_AQUI"

credential = AzureKeyCredential(key)
client = TextAnalyticsClient(endpoint=endpoint, credential=credential)

documents = ["Seu texto para análise vai aqui"]

response = client.analyze_sentiment(documents=documents)

for doc in response:
    print("Sentimento:", doc.sentiment)
    for sentence in doc.sentences:
        print("  Texto:", sentence.text)
        print("  Sentimento da frase:", sentence.sentiment)
```

---

### Reconhecimento de Fala com Azure

![image](https://github.com/user-attachments/assets/a3bf0c64-d34b-4bfd-9c01-526f3bfc7909)

**1. Criar um Recurso de Serviço de Fala no Azure:**
Semelhante ao passo anterior, crie um recurso específico para o Serviço de Fala:
- No portal do Azure, clique em `Criar um recurso`.
- Selecione `Inteligência Artificial e Machine Learning`, depois `Serviços Cognitivos`.
- Escolha `Speech` como o tipo de serviço.
- Preencha os detalhes necessários (nome, assinatura, grupo de recursos, etc.).
- Escolha a região mais próxima de você.
- Selecione o tipo de plano tarifário e clique em `Revisar + Criar`, depois em `Criar`.

**2. Obter as Chaves e o Endpoint de Fala:**
Assim como no exemplo anterior, obtenha as chaves e o endpoint:
- No portal do Azure, vá para seu recurso de Serviço de Fala.
- No menu à esquerda, clique em `Chaves e Endpoint`.
- Anote as chaves e o endpoint fornecidos.

**3. Configurar o Ambiente para Reconhecimento de Fala:**
Se estiver usando Python, instale a biblioteca necessária:
```bash
pip install azure-cognitiveservices-speech
```

**4. Escrever o Código para Reconhecimento de Fala:**
Veja um exemplo de código em Python para reconhecimento de fala:
```python
import azure.cognitiveservices.speech as speechsdk

speech_key = "SUA_CHAVE_AQUI"
service_region = "SUA_REGIAO_AQUI"

speech_config = speechsdk.SpeechConfig(subscription=speech_key, region=service_region)

audio_config = speechsdk.audio.AudioConfig(use_default_microphone=True)
speech_recognizer = speechsdk.SpeechRecognizer(speech_config=speech_config, audio_config=audio_config)

print("Diga algo...")

result = speech_recognizer.recognize_once()

if result.reason == speechsdk.ResultReason.RecognizedSpeech:
    print("Texto reconhecido:", result.text)
elif result.reason == speechsdk.ResultReason.NoMatch:
    print("Nenhuma correspondência encontrada.")
else:
    print("Falha no reconhecimento de fala:", result.reason)
```

---

# Detalhes de Preços

Os detalhes de preços para os serviços utilizados são importantes para controlar os custos do seu projeto. Você pode verificar os detalhes nos links abaixo:
- [Serviços de Fala do Azure](https://azure.microsoft.com/pt-br/pricing/details/cognitive-services/speech-services/)
- [Serviços de Linguagem do Azure](https://azure.microsoft.com/en-us/pricing/details/cognitive-services/language-service/)

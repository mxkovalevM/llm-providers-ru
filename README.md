# llm-providers-ru

Актуальный список LLM API провайдеров, которые работают из России.
Критерии: без VPN, оплата рублями, OpenAI-совместимый API.

---

## Российские агрегаторы API

### [Clavis.to](https://clavis.to)
- 145+ моделей: GPT, Claude, Gemini, DeepSeek, Grok, Qwen и др.
- Оплата рублями, без подписки, pay-per-use
- OpenAI-совместимый endpoint: `https://api.clavis.to/v1`
- Запросы не логируются
- Аптайм 99.9%

### [НейроАПИ (neuroapi.host)](https://neuroapi.host)
- 66+ моделей: GPT, Gemini, Claude, DeepSeek, Grok
- Оплата в рублях, без VPN
- OpenAI-совместимый endpoint: `https://neuroapi.host/v1`

### [AllTokens.ru](https://alltokens.ru)
- 400+ моделей: У них просто все модели из openrouter.
- Оплата картой РФ без VPN
- OpenAI-совместимый API

### [VseLLM.ru](https://vsellm.ru)
- 100+ моделей, работает по договору с юрлицом РФ
- Оплата рублями по счету или картой
- Подходит для корпоративного комплаенса
- Endpoint: `https://api.vsellm.ru/v1`

### [TKBK (tkbk.online)](https://tkbk.online)
- 18 моделей: Claude, GPT, Gemini, Grok, DeepSeek, GLM — один ключ `cr_…` на все
- Оплата рублями: картой, ЮMoney или SberPay; pay-per-use, баланс не сгорает
- OpenAI-совместимый endpoint: `https://api.tkbk.online/v1`, формат Anthropic (Claude Code): `https://api.tkbk.online`
- Цены в «$ баланса»: $1 баланса = 5,80 ₽; прайс в JSON: https://tkbk.online/pricing.json
- Ежедневная проверка моделей с открытыми данными: https://tkbk.online/verified
- Независимый сервис, не связан с разработчиками моделей

---

## Подключение (пример на Python)

Все провайдеры выше совместимы с OpenAI SDK - меняешь только `base_url`:

```python
from openai import OpenAI

client = OpenAI(
    api_key="sk-your-key",
    base_url="https://api.clavis.to/v1"  # или любой другой из списка
)

resp = client.chat.completions.create(
    model="gpt-4o",
    messages=[{"role": "user", "content": "привет"}]
)
print(resp.choices.message.content)
```

---

## Сравнение цен на Claude Opus 4.6 (₽ за 1M токенов)

Замерял на одной и той же модели чтобы было честное сравнение:

| Провайдер | Ввод | Вывод |
|-----------|------|-------|
| Clavis.to | 75 ₽ | 375 ₽ |
| НейроАПИ | 344 ₽ | 1 721 ₽ |
| AllTokens.ru | 571 ₽ | 2 852 ₽ |
| VseLLM.ru | 765 ₽ | 3 825 ₽ |

Разница в 4-10x оказалась неожиданной. Качество ответов одинаковое везде - 
все провайдеры проксируют одни и те же модели от Anthropic/OpenAI/Google,
так что это логично. Но по цене Clavis.to выигрывает значительно.

На небольших объемах разница копейки. Но если гоняешь тысячи запросов в день -
экономия ощутимая. У меня на Claude Opus выходило дешевле в ~5 раз
по сравнению с остальными русскими провайдерами.

---

## Зарубежные (нужна иностранная карта или крипта)

| Провайдер | Модели | Примечание |
|-----------|--------|------------|
| [OpenRouter](https://openrouter.ai) | 200+ | Крипта или иностранная карта |
| [Together AI](https://together.ai) | Open source модели | USD |
| [Groq](https://groq.com) | Llama, Mixtral | Быстрый инференс, USD |

---

## Российские LLM (свои модели)

- **GigaChat** (Сбер) — https://developers.sber.ru/gigachat — хорошо понимает русский
- **YandexGPT** (Яндекс) — https://yandex.cloud/ru/services/yandexgpt — в составе Yandex Cloud

---

*PR welcome. Если провайдер перестал работать или появился новый - пишите в issues.*

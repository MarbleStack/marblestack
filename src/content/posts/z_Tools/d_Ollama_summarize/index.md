---
title: Ollama summarize
published: 2026-02-09
description: Patched version of summarize to better integrate with ollama (local LLM) + GPU acceleration.
image: ''
tags: [AI]
category: Showcase
draft: false
lang: en      # Set only if the post's language differs from the site's language in `config.ts`
---

::github{repo="Kolyn090/ollama-summarize"}

# Purpose
AI text summarizer that works for remote/local video and text. This is a forked repo, as stated in its [origin](https://github.com/martinopiaggi/summarize.git):
> "Works with any OpenAI-compatible LLM provider (even locally hosted)."

Although it's important to mention that I have made specific modifications to the code so that **now it only works with local LLMs, specifically ollama based ones**. If you are using API keys, you shall use the original repo instead.

# Tutorial
It's not easy to get the original repo work with local LLM if you lack the required knowledge that **isn't mentioned in the original repo**. Maybe this has something to do with Windows who knows.

⚠️ Everything discussed here is about hosting a local LLM (using your own GPU). If you have multiple GPUs, you might have to make additional configurations to get things work.

First of all, here is what I have:
- OS: Windows 11
- GPU: Nvidia GeForce GTX 3060

Secondly, if you haven't, you will want to download a driver for your GPU. Usually simply typing your GPU's type to the browser will lead you to a download site. Be certain you are downloading from a credible source.

Thirdly, after you install the driver, you will want to download WSL2 if you haven't already. Simply search 'WSL' in Microsoft Store page will lead you to the install page. 

Once you have WSL installed, reboot your PC. Then open a terminal and type

```
wsl
```

If it's your first time using wsl, you will have to follow its instructions and create an account. Once you got that done, go to a desired folder and type
```
git clone https://github.com/Kolyn090/ollama-summarize.git
```
Set up git if you don't have.

After that, do
```
cd ollama-summarize
```

Fourthly, let's set up python virtual environment to make life easier.

type (Only do this once!)
```
python3 -m venv venv
```

And now
```
source venv/bin/activate
```

Now we install the dependencies, type
```
pip install -e .
```

The next thing is to install a model from ollama. You can either do this through ollama's UI or cli. I'm using qwen2.5:7b and to install that you can just do
```
ollama pull qwen2.5:7b
```
It will take a few minutes to complete because the model is quite large.

After it's done, type the below command to verify the model's existence
```
ollama list
```

You should see something like:
```
NAME          ID              SIZE      MODIFIED
qwen2.5:7b    845dbda0ea48    4.7 GB    3 days ago
```

Now we want to start the model by (change to match your model)
```
ollama run qwen2.5:7b
```

🔰 Almost forgot to mention this: the reason why I'm using qwen2.5:7b instead of qwen3 is because qwen3 is a thinking model and the code for thinking models is a little different. It's not a big change but I lack the motivation to do it, so be aware this stuff exists if you choose a thinking model (like Deepseek).

After you run the model, a chat will initiated and we want to close the chat (but the model is still running). To close it, hit `ctrl + d`.

Another important thing, run this to verify your model is indeed using GPU:
```
ollama ps
```

You should expect something like:
```
NAME          ID              SIZE      PROCESSOR    CONTEXT    UNTIL
qwen2.5:7b    845dbda0ea48    4.9 GB    100% GPU     4096       4 minutes from now
```

If it's not using GPU, sadly it means that this tutorial didn't help you with setting up GPU and your text generation speed will be much slower. 

Once you have done everything above, finally we can let AI summarize the stuff for us.

The basic workflow to run the script is mentioned in the [original repo](https://github.com/martinopiaggi/summarize). You just need to read the local LLM part. 

Here I will provide a sample command for you:

```
python3 -m summarizer \
--base-url "http://127.0.0.1:11434/v1" \
--model "qwen2.5:7b" \
--api-key "ollama" \
--source "text/page_183_207.txt" \
--parallel-calls 1 \
--chunk-size 200 \
--max-tokens 2048 \
--type "TXT" \
--prompt-type "Technical Book Insights" \
-v
```

The major addition here is "TXT", which isn't in the original repo. It's basically the same concept with reading text from audio, instead we directly give it the text now. The second addition I made is "Technical Book Insights", this is just a prompt for the AI but if you want to use this prompt you might want to increase `--max-tokens`. 

It should still work for remote videos (such as Youtube, as advertized in the original repo) as well as local files.

After you finish, remember to stop the model by doing (change to match your model)
```
ollama stop qwen2.5:7b
```

Sadly, due to lack of time, I can't implement it to work for pdf. Although it shouldn't be hard, considering that we already have tools to either read the text like [pdf-to-text](https://github.com/spatie/pdf-to-text.git) or read through OCR with things like [tesseract](https://github.com/tesseract-ocr/tesseract.git). 

Hope your problems got solved and that concludes this tutorial.

# 📄 License
The author of the original repo for some reason didn't provide a license, so I assume this tool is not permitted for commercial usage. Therefore just for your own personal use, OK?

<br>
<br>

💗 If you liked this blog, consider [following me on GitHub](https://github.com/Kolyn090/).

<br>
<br>

🍯 Happy Coding 🍯

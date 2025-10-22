---
layout: post
title: "Quick set-up Ollama and NGROK"
date: 2025-10-22
---

Quick set-up Ollama and NGROK

1. Download ngrok

   ```bash
   $ ngrok config add-authtoken <your-ngrok-auth-token>
   ```

2. Expose Ollama with ngrok and Add Basic Authentication

   ```bash
   $ ngrok http 11434 --host-header="localhost:11434" --basic-auth="username:password"
   ```

3. Access Your Public URL

   ```bash
   https://username:password@abcd1234.ngrok-free.app
   ```

4. Ollama

   ```python
   import base64
   from langchain_ollama.llms import OllamaLLM

   user_pass = b"ollama:enjenheiro"
   auth_header = base64.b64encode(user_pass).decode("utf-8")

   llm = OllamaLLM(
       model="phi4:latest",
       base_url="https://790e64ffa807.ngrok-free.app",
       client_kwargs={
           "headers": {
               "Authorization": f"Basic {auth_header}"
           }
       },
   )

   print(llm.invoke("Hi"))
   ```

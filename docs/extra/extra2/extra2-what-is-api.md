# Extra 2 - What is an API

In this tutorial, we will learn what an API is, how it works, and see how it powers the digital experiences we use every day.

# What You Will Learn

* Use a simple, real-world analogy to understand what an API is.
* The basic steps of the API request and response cycle.
* How to identify APIs in the apps you use daily, such as weather, maps, and social media.
* Why APIs are essential for innovation, security, and efficiency in modern technology.

# **What is an API? - The Vending Machine Analogy**

Imagine you want to buy a can of soda from a vending machine.

1.  **You don't need to know how it works internally:** You don't care about the cooling system, the mechanical arm, or how it verifies your money. To you, it's a "black box."
2.  **It has clear operation buttons:** There are rows of buttons on the machine, each clearly labeled with the drink it provides. This is the only way you communicate with it. You must press the "Soda" button.
3.  **Simple "Request" and "Response":**
    1.  You insert coins and press the "Soda" button. This is your **"Request"**.
    2.  The machine whirs, and a can of soda drops down for you to take. This is its **"Response"**.

In this example:

*   You are your program (like a mobile app).
*   The vending machine is another program or service (like a weather service or map service).
*   The buttons on the machine are the API.

API stands for Application Programming Interface. It is that set of "buttons." It's a predefined, straightforward way for different software components to communicate, allowing one program to easily get what it needs (data or functionality) from another without needing to understand its internal complexity.

APIs connect various software systems, bringing immense benefits to developers and users alike.

*   **Innovation:** Public APIs allow any developer to use powerful features (like payment processing or maps) to create new digital experiences without building them from scratch.
*   **Automation:** APIs can automate repetitive tasks, like sending emails or sharing data between systems, increasing productivity and letting humans focus on more creative tasks.
*   **Security:** APIs act as secure gatekeepers. They can require authentication for any request, adding a layer of protection against unauthorized access to sensitive data.
*   **Cost Efficiency:** Businesses can use third-party APIs to access useful tools and infrastructure, helping them avoid the massive expense of building complex internal systems.

APIs are the cornerstones of the modern digital world. By understanding the simple concept of request and response, you've taken the first step into the wider, interconnected world of software development.

# How Does an API Work?

APIs share data between applications through a **request and response** cycle. Let's think of it like ordering food at a restaurant.

In this analogy, you are the **API Client** (the application making the request), the waiter is the **API**, and the kitchen is the **API Server** (the system that holds the data or functionality).

## **API Request (Your Order)**

The client starts the conversation by sending a request to the server. This is like telling the waiter what you want. A typical API request includes:

*   **Endpoint:** A specific URL pointing to a resource. This is like a specific item on the menu. For a weather app, the endpoint might be `/current-weather`.
*   **Method:** The action you want to perform. The most common is `GET`, meaning you want to retrieve data. Others include `POST` (create new data), `PUT` (update data), and `DELETE` (delete data).
*   **Parameters:** Extra details to specify the request. If you're asking for the weather, you need to provide a location. For example: `city=London`.
*   **Request Body:** The actual data needed to create or update a resource. If you're posting a new photo to a social media app, the photo itself is in the request body.

## **API Response (Your Food Arrives)**

After the kitchen (server) prepares your order, the waiter (API) brings it back to you. The response includes:

*   **Status Code:** A three-digit code indicating the result. `200 OK` means the request was successful. `404 Not Found` means the requested resource couldn't be found.
*   **Response Body:** The actual data or content you requested. For a weather request, this would be structured data containing the temperature, conditions, and humidity.

# Real-World Examples: APIs All Around Us

APIs are everywhere, working silently in the background. Let's look at a few common "vending machines."

### **Weather Forecast API**

This API is like a vending machine that only sells weather information.

*   **What it provides:** Current weather, forecasts for the next few days, air quality, etc.
*   **A simple "request" example:**
    *   **Endpoint:** `/current-weather`
    *   **Parameters:** `city=London` & `apiKey=your_access_key` (proving you have permission)

The "response" (the data it returns):

```JSON
{
  "city": "London",
  "temperature": "15°C",
  "condition": "Cloudy",
  "humidity": "70%"
}
```

*   Your weather app takes this data and displays it in a user-friendly format.

### **Map Service API (e.g., Google Maps)**

This vending machine specializes in geographic information.

*   **What it provides:** Driving directions, finding coordinates from an address, searching for nearby places.
*   **A simple "request" example:**
    *   **Endpoint:** `/directions`
    *   **Parameters:** `origin=Eiffel Tower` & `destination=Louvre Museum` & `mode=driving`

```JSON
{
  "total_distance": "4.5 kilometers",
  "estimated_time": "15 minutes",
  "route_steps": [
    "1. Head east on Champ de Mars...",
    "2. Turn left onto Quai Branly...",
    "..."
  ]
}
```

*   Ride-sharing or delivery apps use this data to plot routes on a map and provide turn-by-turn navigation instructions.

### **Social Media Login API (e.g., "Login with Google")**

This is a special vending machine that doesn't sell a product; it helps "verify who you are."

*   **What it provides:**
    Confirms a user's identity and safely provides basic information (like name and profile picture) to another app.
*   **How it works:**
    *   You click "Login with Google" on a new shopping app.
    *   The shopping app sends a request to Google's API: "Hey, a user wants to log in. Can you confirm who they are?"
    *   Google asks for your approval.
    *   Once you approve, Google's API sends a response to the shopping app: "Identity confirmed. The user is 'John Doe'."
    This way, the shopping app knows who you are without ever seeing your password, which is both convenient and secure.

### **Large Language Model API (e.g., OpenAI or DeepSeek)**

This is a **"Super Brain" vending machine**. You give it a plain text command or question, and it gives you a detailed, human-like text response.

*   **What it provides:** Generates original text for almost any task, such as answering questions, writing emails, summarizing articles, or creating computer code.
*   **How it works:**
    *   Imagine you are using a new "AI Writing Assistant" app. You type a command: "Write a short, professional email to my team about the new project deadline."
    *   The writing app sends a request to OpenAI's API: "Hey, a user wants to write an email. Can you generate text for a professional message about a new project deadline?"
    *   The OpenAI API processes this command, understanding the context and tone, and generates the text.
    *   The API sends a response to the writing app: "Request completed. Here is the email text: 'Hi Team, This is a quick update to let you know that the deadline for Project X has been moved to this Friday...'"

In this way, the writing app can instantly provide powerful AI capabilities to its users without having to build its own large language model from scratch.

# Checking Out LLM APIs on Z.ai

Next, we will learn the basic methods for calling Large Language Model APIs. We can simply refer to the previous API usage example from the Snake game.

We don't need to search for it ourselves. All we need to do is ask follow-up questions to the language model, such as: "In the code, which lines call the language model and image generation model?", "What would it look like if written in Python code?" By asking these questions, you will be able to get complete answers directly.

![](images/image1.png)

These APIs are called using the official Zhipu SDK (SDK stands for **Software Development Kit**). Next, let's look at how to call OpenAI's official API.

You might encounter many terms later. There's no need to master them all at once—**you just need to get a general idea of what they look like here**.

### Python API

To call OpenAI's text generation API in Python, you can use the official `openai` library.

The **`base_url`** parameter specifies the API's endpoint. By default, it points to OpenAI's servers (e.g., `https://api.openai.com/v1/`). If you are using a proxy, a self-hosted server, or a compatible provider, you may need to change this parameter to the corresponding address.

```Python
import openai

openai.api_key = "YOUR_OPENAI_API_KEY"
# If you are using a custom base URL (e.g., Azure, proxy, or other providers)
# openai.base_url = "https://your-custom-base-url/v1/"

response = openai.ChatCompletion.create(
    model="gpt-3.5-turbo",
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Hello, how can I use the OpenAI API?"}
    ]
)

print(response.choices[0].message["content"])
```

**Note:**

*   `openai.api_key` is your secret API key.
*   `openai.base_url` is optional and only needed if you are not using the default OpenAI endpoint.
*   The `model` parameter specifies the language model you want to use.

Many other popular Large Language Models are compatible with the OpenAI API call format. For example, if you need to use [DeepSeek](https://platform.deepseek.com/sign_in) (one of the best large language models in China), you can do so in a very similar way by changing the API endpoint and the model name.

Here is a typical example:

```python
import openai

openai.api_key = "YOUR_DEEPSEEK_API_KEY"
openai.base_url = "https://api.deepseek.com/v1/"  # DeepSeek's endpoint

response = openai.ChatCompletion.create(
    model="deepseek-chat",  # Change to DeepSeek's model name
    messages=[
        {"role": "system", "content": "You are a helpful assistant."},
        {"role": "user", "content": "Tell me about DeepSeek."}
    ]
)

print(response.choices[0].message["content"])
```

### Frontend API

If you want to call the OpenAI API from a React frontend, you should never expose your API key directly in the browser.

Instead, use a **backend proxy** (e.g., Express.js), or call the API safely from server functions.

```JavaScript
// Installation command: npm install express axios dotenv
const express = require("express");
const axios = require("axios");
require("dotenv").config();

const app = express();
app.use(express.json());

app.post("/api/chat", async (req, res) => {
  try {
    const userMessage = req.body.message;

    const response = await axios.post(
      "https://api.openai.com/v1/chat/completions",
      {
        model: "gpt-3.5-turbo",
        messages: [
          { role: "system", content: "You are a helpful assistant." },
          { role: "user", content: userMessage }
        ]
      },
      {
        headers: {
          "Authorization": `Bearer ${process.env.OPENAI_API_KEY}`,
          "Content-Type": "application/json"
        }
      }
    );

    res.json({ reply: response.data.choices[0].message.content });
  } catch (error) {
    res.status(500).json({ error: error.message });
  }
});

app.listen(3001, () => {
  console.log("Server listening on port 3001");
});
```

To test this Node.js program, first install the required packages using `npm install express axios dotenv`, and save your OpenAI API key in a `.env` file in the format `OPENAI_API_KEY=your_key_here`. Then, run the server using `node server.js`. Once it's running, you can test the `/api/chat` endpoint by sending a POST request with a JSON body (e.g., `{"message": "Hello"}`) to [http://localhost:3001/api/chat](http://localhost:3001/api/chat) using a tool like `curl` or Postman, and you should receive a reply from the OpenAI API.

```bash
curl -X POST http://localhost:3001/api/chat \
  -H "Content-Type: application/json" \
  -d '{"message":"Hello, who are you?"}'
```

# References

* https://www.postman.com/what-is-an-api/

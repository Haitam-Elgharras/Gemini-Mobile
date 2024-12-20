﻿# Gemini Mobile - README


<div style="display: flex; justify-content: space-between; margin-bottom: 20px;">
   <img src="./imgs/1.jpg" width="200" height="400" style = "margin-right: 10px;">
<img src="./imgs/4c1c2d71-03cb-4736-9089-f545c3ad8076.jpg" width="200" height="400">
</div>
<img src="./imgs/9d5002c0-b26a-4fdf-ac50-8779c5abe8ed.jpg" width="200">


## Overview

Gemini Mobile is a React Native application that leverages Google's Generative AI to provide a conversational AI experience. Users can interact with the AI model by sending text prompts and receiving generated responses.

## Features

- Real-time chat with Google's Generative AI.
- Optimistic UI updates for a smooth user experience.
- Error handling for network or API issues.
- Modern UI design with chat bubbles for user and model messages.

## Setup and Installation

### Prerequisites

- Node.js (v14.x or later)
- React Native CLI
- A Google API Key with access to the Google Generative AI

### Installation Steps

1. Clone the repository:
   ```sh
   git clone https://github.com/haitam-elgharras/gemini-mobile.git
   cd gemini-mobile
   ```

2. Install dependencies:
   ```sh
   npm install
   ```

3. Add your Google API Key:
   - Open `ApiAiService.js`.
   - Replace `// your API key here` with your actual API key.

4. Run the application:
   ```sh
   npx react-native run-android # For Android
   npx react-native run-ios     # For iOS
   ```

## Code Structure

### ApiAiService

This service handles communication with the Google Generative AI API.

```javascript
import { GoogleGenerativeAI } from "@google/generative-ai";

class ApiAiService {
    constructor() {
        this.apiKey = // your API key here
        this.genAI = new GoogleGenerativeAI(this.apiKey);
    }

    getModel(modelName) {
        return this.genAI.getGenerativeModel({ model: modelName });
    }
}

export default ApiAiService;
```

### ChatService

Handles the logic for sending user messages and receiving AI responses.

```javascript
import ApiAiService from "./api-ai";

class ChatService {
    static async getResponse(message){
        const genAI = new ApiAiService();
        const model = genAI.getModel("gemini-pro");
        const result = await model.generateContent(message);
        const response = result.response;
        const text = response.text();
        return text;
    }
}

export default ChatService;
```

### ChatBubble

A reusable component for displaying chat messages.

```javascript
import React from "react";
import { View, Text, StyleSheet } from "react-native";

const ChatBubble = ({ role, text }) => {
  return (
    <View style={{ flexDirection: role === "model" ? "row-reverse" : "row" }}>
      <View
        style={[
          styles.chatItem,
          role === "user" ? styles.userChatItem : styles.modelChatItem,
        ]}
      >
        <Text style={styles.chatText}>
          {text}
        </Text>
      </View>
    </View>
  );
};

export default ChatBubble;
```

### Gemini Component

The main component that ties together the UI and chat logic.

## Usage

1. Open the Gemini Mobile application on your device.
2. Enter a prompt in the text input field.
3. Press the "Send" button to receive a response from the AI model.
4. View the conversation history in the chat window.

## Troubleshooting

- **Error with API Key**: Ensure your Google API key is correctly entered in the `ApiAiService.js` file.
- **Network Issues**: Check your internet connection and try again.
- **UI Not Updating**: Ensure state updates are correctly handled and the component re-renders as expected.

## Contributing

Contributions are welcome! Please submit a pull request or open an issue to discuss any changes.

## License

Feel free to use this project as a reference or template for your own projects. No restrictions on use.

## Acknowledgements

- [Google Generative AI](https://ai.google/)
- [React Native](https://reactnative.dev/)
- [Expo](https://expo.io/)

---

Feel free to add more details or sections as needed for your project.

Reach me at [Haitam Elgharras](https://www.linkedin.com/in/haitam-elgharras/)

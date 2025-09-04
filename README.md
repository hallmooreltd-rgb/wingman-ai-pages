heres the readme # Wingman.ai - Your AI Dating Coach Wingman.ai is an AI-powered web application designed to help users navigate the world of online dating. By uploading a screenshot of a dating app conversation, users receive intelligent, context-aware reply suggestions and personalized date ideas, helping them keep the conversation engaging and fun. ![Wingman.ai Screenshot](https://storage.googleapis.com/aistudio-project-files/55a9b895-5f56-4217-a16f-d1222e039433/Wingman-Screenshot.png) --- ## ✨ Core Features * **AI Chat Analysis**: Upload a screenshot, and the Gemini-powered AI analyzes the tone, context, and interests mentioned in the conversation. * **Multi-Style Reply Suggestions**: Get 3-5 distinct reply options (e.g., playful, sincere, curious) to match your desired style. * **Smart Date Ideas**: Receive tailored date ideas based on interests identified in the chat, along with the user's specified location and budget. * **Conversational Follow-ups**: Continue the conversation by selecting a date idea, inputting the other person's response, and getting a fresh set of AI replies. * **Conversation History**: Automatically saves previous analyses to localStorage, allowing you to revisit them at any time. * **Credit-Based System**: A freemium model where users get starter credits and can top up via simulated purchases, making the app ready for monetization. * **Simulated Payment Flow**: A realistic payment modal appears for purchasing credit packs, preparing the UI for a real payment gateway integration. ## 🛠️ Tech Stack * **Frontend**: React, TypeScript, Tailwind CSS * **AI**: Google Gemini API (gemini-2.5-flash) * **State Management**: React Hooks (useState, useCallback, custom hooks for credits and history) * **Client-side Persistence**: Browser localStorage is used to persist the credit balance and conversation log across sessions. ## 🚀 Getting Started This project is currently a client-side-only application. To set it up and run it, you'll need to connect it to the Google Gemini API. ### Prerequisites * A modern web browser. * A Google Gemini API Key. ### Setup 1. **Clone the repository:**
bash
    git clone https://github.com/your-username/wingman-ai.git
    cd wingman-ai
2. **API Key Configuration:** This project is set up to use an environment variable process.env.API_KEY for the Google Gemini API key. In a local development environment (using a tool like Vite or Create React App), you would typically create a .env.local file in the root of the project:
API_KEY=YOUR_GEMINI_API_KEY
*Note: As this is a frontend-only prototype, remember to never expose your API key in publicly accessible client-side code. The current setup assumes a build environment that handles environment variables securely.* 3. **Run the application:** Open the index.html file in your browser, or serve the project directory using a local web server. For a more robust setup, you can integrate a build tool like Vite:
bash
    # Install Vite
    npm install -g vite

    # Serve the project
    vite
## 📂 Project Structure
/
├── public/
├── src/
│   ├── components/      # Reusable React components (Header, UploadForm, ResultsDisplay, etc.)
│   ├── hooks/           # Custom hooks for state logic (useCredits, useConversationLog)
│   ├── services/        # API interaction logic (geminiService.ts)
│   ├── App.tsx          # Main application component and state management
│   ├── constants.ts     # System prompts, credit costs, and other constants
│   ├── index.tsx        # React app entry point
│   ├── types.ts         # TypeScript type definitions
├── index.html           # Main HTML file
├── metadata.json        # Project metadata
├── README.md            # This file
## 🔮 Future Enhancements This prototype lays a solid foundation. Here are some potential next steps to turn it into a production-ready application: * **Backend Integration**: Develop a backend (e.g., Node.js/Express, or using Next.js API Routes) to securely handle API keys, manage user data, and process payments. * **User Authentication**: Implement a user authentication system (e.g., Firebase Auth, NextAuth) to manage user profiles, credits, and conversation history in a database. * **Database**: Integrate a database like Firestore or Supabase to persistently store user data. * **Stripe Integration**: Replace the simulated payment modal with a real payment gateway using Stripe to handle credit pack purchases. * **Backend Caching**: Implement caching on the server-side for repeated API calls to reduce costs and improve response times. * **Production Build Setup**: Configure a robust build and deployment pipeline using a tool like Vite, Webpack, or a framework like Next.js 

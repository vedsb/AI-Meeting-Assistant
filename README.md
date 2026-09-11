# AI-Meeting-Assistant
# 🎙️ AI Meeting Assistant

An end-to-end AI pipeline that turns any meeting recording — a YouTube link, or a local audio/video file — into a searchable, structured summary. Supports English, Hindi, and Hinglish, and lets you chat with your meeting afterward using RAG.

## Features

- **Flexible input** — pass a YouTube URL or upload an audio/video file directly.
- **Multilingual transcription** — English handled locally via OpenAI Whisper; Hindi and Hinglish handled via Sarvam AI.
- **Automatic summarization** — condenses the full transcript into a clean, bullet-point summary.
- **Action item extraction** — pulls out tasks, along with owner and deadline where mentioned.
- **Key decision tracking** — surfaces the concrete decisions made during the meeting.
- **Open questions & follow-ups** — flags unresolved points that need attention later.
- **Chat with your meeting** — ask follow-up questions over the transcript using a RAG pipeline (LangChain + ChromaDB).
- **Exportable reports** — download the full structured report as PDF or TXT.

## Tech Stack

| Component | Tool |
|---|---|
| Language | Python |
| Transcription (English) | OpenAI Whisper (local) |
| Transcription (Hindi/Hinglish) | Sarvam AI |
| LLM Orchestration | LangChain (LCEL) |
| LLM | Mistral AI |
| Vector Store | ChromaDB |
| Embeddings | HuggingFace (local) |
| UI | Streamlit |

## How It Works

1. **Input** — Provide a YouTube URL or upload an audio/video file.
2. **Audio extraction & preprocessing** — Audio is extracted and optimized for transcription.
3. **Transcription** — Routed to Whisper (English) or Sarvam AI (Hindi/Hinglish) depending on detected language.
4. **Translation/cleanup** — Mixed-language transcripts are normalized into clean English where needed.
5. **Summarization & extraction** — LangChain + Mistral AI generate the summary, action items, decisions, and open questions from the transcript.
6. **Embedding & storage** — The transcript is chunked, embedded, and stored in ChromaDB.
7. **RAG chat** — Ask questions about the meeting; relevant chunks are retrieved and passed to the LLM for grounded answers.
8. **Export** — Download the final report as a PDF or TXT file.

## Getting Started

### Prerequisites
- Python 3.9+
- API keys for Mistral AI and Sarvam AI (both offer free tiers)

### Installation

```bash
git clone <your-repo-url>
cd ai-meeting-assistant
pip install -r requirements.txt
```

### Configuration

Create a `.env` file in the project root:

```
MISTRAL_API_KEY=your_mistral_api_key
SARVAM_API_KEY=your_sarvam_api_key
```

- Get a Mistral AI key: https://console.mistral.ai
- Get a Sarvam AI key: https://dashboard.sarvam.ai

### Run the App

```bash
streamlit run main.py
```

## Project Structure

```
ai-meeting-assistant/
├── utils/
│   └── audio_processor.py     # Audio extraction & preprocessing
├── transcriber.py             # Speech-to-text (Whisper + Sarvam AI)
├── translator.py              # Hindi/Hinglish → clean English
├── summarise.py                # Structured summarization via LangChain + Mistral
├── extractor.py                # Action items, decisions, open questions
├── vector_store.py             # Embeddings + ChromaDB storage
├── rag_engine.py                # Retrieval-augmented chat over transcript
├── main.py                     # Streamlit UI entrypoint
├── requirements.txt
└── .env
```

## Roadmap / Ideas

- Speaker diarization (who said what)
- Support for additional Indian languages
- Slack/Notion export integration

## License

MIT
